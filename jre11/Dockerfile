FROM tomcat:8.5.41-jre11

MAINTAINER yesnokim <yesnokim@gmail.com>

ENV ANDROID_SDK_URL="https://dl.google.com/android/android-sdk_r24.4.1-linux.tgz" \
    ANDROID_BUILD_TOOLS_VERSION=23.0.3 \
    MAVEN_HOME="/usr/share/maven" \
    ANDROID_HOME="/opt/android-sdk-linux"

ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/$ANDROID_BUILD_TOOLS_VERSION:$MAVEN_HOME/bin

# Install android build dependancies
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y curl libstdc++6:i386 libgcc1:i386 zlib1g:i386 libncurses5:i386

# Install phantomJS
RUN wget -qO- -O /tmp/phantomjs.tar.bz2 https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
    tar xf /tmp/phantomjs.tar.bz2 -C /tmp && \
    mv /tmp/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin/phantomjs

# Install ffmpeg
RUN apt-get update && \
    apt-get install -y ffmpeg && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tomp/* /var/tmp/*

# Installs Android SDK
RUN curl -sL ${ANDROID_SDK_URL} | tar xz -C /opt && \
    echo y | android update sdk -a -u -t platform-tools,build-tools-${ANDROID_BUILD_TOOLS_VERSION} && \
    rm -rf $ANDROID_HOME/tools/* && \
    chmod a+x -R $ANDROID_HOME && \
chown -R root:root $ANDROID_HOME
