# docker build -t registry.gitlab.com/overleaf-open/overleaf/sharelatex:latest .

FROM registry.gitlab.com/overleaf-open/overleaf/sharelatex:latest

# 安装TexLive2023
# RUN tlmgr option repository https://cran.asia/tex/systems/texlive/tlnet/
RUN tlmgr update --self --all
RUN tlmgr install scheme-full

# 在现有的 PATH 值上添加新路径
ENV PATH="${PATH}:/usr/local/texlive/2023/bin/x86_64-linux"
