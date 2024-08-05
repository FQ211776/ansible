FROM archlinux:base-devel

# Actualizar el sistema e instalar paquetes básicos
RUN pacman -Syu --noconfirm && \
    pacman -S --noconfirm \
    bash-completion \
    bc \
    curl \
    diffutils \
    findutils \
    glibc \
    gnupg \
    inetutils \
    keyutils \
    less \
    lsof \
    man-db \
    man-pages \
    mlocate \
    mtr \
    ncurses \
    nss-mdns \
    openssh \
    pigz \
    pinentry \
    procps-ng \
    rsync \
    shadow \
    sudo \
    tcpdump \
    time \
    traceroute \
    tree \
    tzdata \
    unzip \
    util-linux \
    util-linux-libs \
    vte-common \
    wget \
    words \
    xorg-xauth \
    zip \       
    git \
    vim \
    zsh \
    python \
    python-pip \
    ansible \
    go \
    && rm -rf /var/cache/pacman/pkg/*

# Crear un usuario no-root
ARG USERNAME=dev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Cambiar al usuario no-root
USER $USERNAME

# Configurar el directorio de trabajo
WORKDIR /home/$USERNAME

# Instalar yay (AUR helper)
RUN git clone https://aur.archlinux.org/paru-bin.git \
    && cd paru-bin \
    && makepkg -si --noconfirm \
    && cd .. \
    && rm -rf paru-bin

# Limpiar caché de pacman
RUN sudo pacman -Scc --noconfirm