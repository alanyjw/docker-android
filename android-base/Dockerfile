FROM java:8-jdk

# Fix Hash Sum Mismatch causing from httpredir.debian.org
RUN sed -i s/httpredir.debian.org/cdn-fastly.deb.debian.org/g /etc/apt/sources.list

# Need some 32 bit libs for aapt and adb
RUN dpkg --add-architecture i386 \
    && apt-get update && apt-get install -y --no-install-recommends \
        net-tools:i386 \
        libstdc++6:i386 \
        zlib1g:i386 \
    && rm -rf /var/lib/apt/lists/*

# Environment variables
ENV TERM=dumb \
    GRADLE_USER_HOME=/var/cache/gradle \
    ANDROID_HOME=/usr/local/android-sdk-linux \
    PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

# Install Android SDK
RUN curl -L http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz \
| tar --no-same-owner -xzC /usr/local/; \
echo y \
| $ANDROID_HOME/tools/android update sdk --force --all --no-ui --filter \
tools,\
platform-tools,\
extra-android-m2repository,\
extra-google-m2repository
