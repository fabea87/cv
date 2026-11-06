# Trimmed TeX Live (XeLaTeX + latexmk) image for building the CVs, pushed to
# ghcr.io/fabea87/cv-texlive by .github/workflows/docker-image.yml and used by
# build.yml via xu-cheng/latex-action's docker_image input.
#
# Why: the full texlive-alpine scheme that latex-action defaults to weighs in
# at ~4 GB and takes minutes to pull on every CI run; this image downloads
# ~110 MB of TeX Live packages (~400 MB installed) and pulls in tens of
# seconds.
#
# The package list is the union of CV.tex / CV-cn.tex \usepackage requirements.
# Names were verified against the CTAN tlpdb (note: the tabto CTAN package
# ships as tabto-ltx); tlmgr resolves their transitive dependencies
# automatically. TeX Live ships musl-native binaries (x86_64-linuxmusl), so
# plain Alpine works without gcompat.
FROM alpine:3.22

ENV PATH="/opt/texlive/bin/x86_64-linuxmusl:${PATH}"

# bash/perl: latexmk; git: latex-action's entrypoint runs `git config
# --system --add safe.directory`; fontconfig: latex-action's extra_fonts runs fc-cache for
# family-name font lookups (Noto Serif CJK SC); file: install-tl's platform
# detection; curl/tar/xz: fetching and unpacking the installer; poppler-utils:
# pdffonts, used by the post_compile font verification (recent ubuntu-latest
# images no longer preinstall it on the host).
RUN apk --no-cache add \
        bash \
        curl \
        file \
        fontconfig \
        git \
        perl \
        poppler-utils \
        tar \
        xz

COPY texlive.profile /tmp/texlive.profile
RUN set -eux; \
    curl -fsSL https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz \
        -o /tmp/install-tl-unx.tar.gz; \
    curl -fsSL https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz.sha512 \
        -o /tmp/install-tl-unx.tar.gz.sha512; \
    ( cd /tmp && sha512sum -c install-tl-unx.tar.gz.sha512 ); \
    tar -xzf /tmp/install-tl-unx.tar.gz -C /tmp; \
    # mirror.ctan.org rotates across mirrors on every request, and any single
    # mirror can be flaky, so retry the network-bound installer steps.
    retry() { i=1; while [ "$i" -le 5 ]; do if "$@"; then return 0; fi; \
        echo "attempt $i of '$*' failed, retrying in 5s"; i=$((i+1)); sleep 5; done; return 1; }; \
    retry env TEXLIVE_INSTALL_ENV_NOCHECK=1 /tmp/install-tl-*/install-tl \
        -scheme scheme-basic -profile /tmp/texlive.profile; \
    retry tlmgr install \
        fontspec xecjk csquotes babel-english microtype datetime fmtcount \
        tabto-ltx hyperref geometry enumitem needspace setspace xcolor \
        fontawesome5 academicons fancyhdr lastpage booktabs latexmk lm; \
    ln -s /opt/texlive/texmf-var/fonts/conf/texlive-fontconfig.conf \
        /etc/fonts/conf.d/09-texlive.conf; \
    fc-cache -fv; \
    rm -rf /tmp/install-tl-unx.tar.gz* /tmp/install-tl-* /tmp/texlive.profile

CMD ["/bin/bash"]
