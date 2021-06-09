#
# File: https://github.com/infra-helpers/docker-images-nodejs/tree/master/ubuntu2004
#
FROM docker.io/ubuntu:20.04

LABEL authors="Denis Arnaud <denis.arnaud_github at m4x dot org>"
LABEL version="0.1"

# Environment
ENV container docker
ENV HOME /root
ENV LANGUAGE en_US:en
ENV LANG en_US.UTF-8
ENV LC_ALL $LANG

# Update the system
RUN echo "Europe/Paris" > /etc/timezone
RUN echo 'APT::Get::Assume-Yes "true";' > /etc/apt/apt.conf.d/90-yes

RUN apt-get -qq update && \
    apt-get -y upgrade && apt-get -y autoremove && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends \
    apt-utils apt-transport-https \
    ca-certificates locales locales-all tzdata \
    zip unzip gzip bzip2 xz-utils tar unrar p7zip-full \
    procps htop \
    curl wget netcat net-tools

# Generate the locales
RUN locale-gen $LANG && update-locale LANG=$LANG LANGUAGE=$LANGUAGE LC_ALL=$LC_ALL

# Configure the time-zone
RUN dpkg-reconfigure -f noninteractive tzdata

# Basic and C++ packages
RUN apt-get -y install less htop screen \
	git keychain gawk jq \
	bash-completion vim-nox emacs-nox apt-utils keyutils ftp \
	zlib1g-dev libbz2-dev \
	lsb-release libgmp-dev \
	gcc g++ cppcheck clang cmake manpages patch pkg-config \
	m4 autoconf automake libtool libltdl-dev build-essential \
	libreadline-dev libncurses5-dev \
	libzmqpp-dev libssl-dev libffi-dev \
	swig graphviz \
	sqlite3 mysql-client postgresql-client \
	doxygen ghostscript texlive-latex-recommended

# NodeJS
RUN curl -fsSL https://deb.nodesource.com/setup_16.x | bash
RUN apt-get -y install nodejs
RUN npm install -g npm@7.16.0
RUN npm install -g newman
RUN npm install -g newman-reporter-csv

# Cleaning
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set up the packaging environment for the `build` user
ADD resources/bashrc $HOME/.bashrc
ADD resources/gitconfig $HOME/.gitconfig
ADD resources/vimrc $HOME/.vimrc
RUN chmod 640 $HOME/.bashrc $HOME/.gitconfig $HOME/.vimrc

#
WORKDIR $HOME

# Git prompt
RUN git clone https://github.com/magicmonty/bash-git-prompt.git ~/.bash-git-prompt --depth=1


# Entry point
CMD ["/bin/bash"]

