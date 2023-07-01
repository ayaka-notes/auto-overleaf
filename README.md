# auto-overleaf
自动定时构建Overleaf的Docker镜像，发布到Gitlab。

- 镜像公开地址：https://gitlab.com/overleaf-open/overleaf/container_registry/
- 包含的类型：amd64的原始镜像、arm64的原始镜像以及带有texlive2023的完整镜像
- 由于Gitlab在国内还是速度比较快的，所以非常推荐使用。带有texlive2023的镜像自动修复了环境变量不一致的问题，支持xelatex等编译，非常方便


