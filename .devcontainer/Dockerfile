FROM pytorch/pytorch:2.0.1-cuda11.7-cudnn8-devel
#FROM pytorch/pytorch:1.11.0-cuda11.3-cudnn8-devel
# ベースイメージによってはdocker build時にGPGエラーが発生して途中で止まる。
# その場合、<https://zenn.dev/takakurasato/scraps/d3e0ee6132a5c5>を参考にして解決する。
#RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/3bf863cc.pub
#RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub

ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y \
    git wget libgl1-mesa-glx libglib2.0-0 \
    sudo \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Add user
ARG USERNAME=developer
ARG GROUPNAME=localuser
ARG UID=1000
ARG GID=1000
ARG PASSWORD=pass
RUN groupadd -g $GID $GROUPNAME && \
    useradd -m -s /bin/bash -u $UID -g $GID -G sudo $USERNAME && \
    echo $USERNAME:$PASSWORD | chpasswd && \
    echo "$USERNAME   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER $USERNAME

RUN pip install jupyter black flake8 mypy numpy pandas matplotlib scikit-learn opencv-python torchinfo torchsummary timm torchtyping tensorboard torch_tb_profiler torcheval seaborn