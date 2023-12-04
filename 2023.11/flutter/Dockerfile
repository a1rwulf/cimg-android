# vim:set ft=dockerfile:

FROM cimg/android:2023.11.1-ndk

LABEL maintainer="Community & Partner Engineering Team <community-partner@circleci.com>"

ARG flutter_version=3.16.2

ENV FLUTTER_HOME=/home/circleci/flutter \
    FLUTTER_VERSION=$flutter_version
ENV FLUTTER_ROOT=$FLUTTER_HOME

ENV PATH ${PATH}:${FLUTTER_HOME}/bin:${FLUTTER_HOME}/bin/cache/dart-sdk/bin

RUN mkdir -p ${FLUTTER_HOME} && git clone --depth 1 --branch ${FLUTTER_VERSION} https://github.com/flutter/flutter.git ${FLUTTER_HOME}

# Despite working, the flutter doctor --android-licenses command returns a non-zero exit code (141)
# so we need to ignore the exit code for now.
# RUN yes "y" | flutter doctor --android-licenses
RUN flutter precache


# Disable the change of the default shell from the base image
# See:
# Change default shell for RUN from Dash to Bash
# SHELL ["/bin/bash", "-exo", "pipefail", "-c"]
# Using pipefail breaks usage of yes which we need to accept all android licenses
SHELL ["/bin/bash", "-c"]

RUN yes | flutter doctor --android-licenses

# ARG USERNAME=a1rwulf
# ARG USER_UID=1000
# ARG USER_GID=$USER_UID

# # Create the user
# RUN groupadd --gid $USER_GID $USERNAME \
#     && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
#     #
#     # [Optional] Add sudo support. Omit if you don't need to install software after connecting.
#     && apt-get update \
#     && apt-get install -y sudo \
#     && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
#     && chmod 0440 /etc/sudoers.d/$USERNAME

# # ********************************************************
# # * Anything else you want to do like clean up goes here *
# # ********************************************************

# # [Optional] Set the default user. Omit if you want to keep the default as root.
# USER $USERNAME