FROM centos:6.9
MAINTAINER Michael Sarahan <msarahan@continuum.io>

# Set the locale
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN mkdir -p bin && \
  LATEST_RELEASE=$(curl -L -s -H 'Accept: application/json' https://github.com/concourse/concourse/releases/latest) && \
  LATEST_VERSION=$(echo $LATEST_RELEASE | sed -e 's/.*"tag_name":"\([^"]*\)".*/\1/') && \
  ARTIFACT_URL="https://github.com/concourse/concourse/releases/download/$LATEST_VERSION/fly_linux_amd64" && \
  curl -L ${ARTIFACT_URL} -o bin/fly && chmod +x bin/fly

RUN yum install -y \
  libX11 libX11.i686 \
  libXau libXau.i686 \
  libXcb libXcb.i686 \
  libXdmcp libXdcmp.i686 \
  libXext libXext.i686 \
  libXrender libXrender.i686 \
  libXt libXt.i686 \
  mesa-libGL mesa-libGL.i686 \
  mesa-libGLU mesa-libGLU.i686 \
  openssh-clients \
  patch \
  rsync \
  util-linux \
  wget \
  xorg-x11-server-Xvfb \
  && yum clean all

WORKDIR /build_scripts
COPY install_miniconda.sh /build_scripts
RUN ./install_miniconda.sh

ENV PATH="/opt/conda/bin:${PATH}"

CMD [ "/bin/bash" ]
