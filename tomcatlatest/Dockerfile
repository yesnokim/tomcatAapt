FROM tomcat

MAINTAINER yesnokim <yesnokim@gmail.com>

ENV ANDROID_SDK_URL="https://dl.google.com/android/android-sdk_r24.4.1-linux.tgz" \
    ANDROID_BUILD_TOOLS_VERSION=23.0.3 \
    MAVEN_HOME="/usr/share/maven" \
    ANDROID_HOME="/opt/android-sdk-linux"

ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/$ANDROID_BUILD_TOOLS_VERSION:$MAVEN_HOME/bin

RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y curl libstdc++6:i386 libgcc1:i386 zlib1g:i386 libncurses5:i386 && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Installs Android SDK
RUN curl -sL ${ANDROID_SDK_URL} | tar xz -C /opt && \
    echo y | android update sdk -a -u -t platform-tools,build-tools-${ANDROID_BUILD_TOOLS_VERSION} && \
    rm -rf $ANDROID_HOME/tools/* && \
    chmod a+x -R $ANDROID_HOME && \
chown -R root:root $ANDROID_HOME
