FROM httpd:alpine

# Configure Debian version and architecture
ENV DEBIAN_MIRROR=https://cdimage.debian.org
ENV DEBIAN_VERSION=stretch
ENV DEBIAN_ARCH=amd64

# Update the system
RUN apk update
RUN apk upgrade

# Get dependencies
RUN apk add wget --no-cache

# Setup the environment
RUN mkdir /usr/local/apache2/htdocs/opensdcp/
RUN mkdir /usr/local/apache2/htdocs/opensdcp/debian
RUN mkdir /usr/local/apache2/htdocs/opensdcp/debian/9
RUN mkdir /usr/local/apache2/htdocs/opensdcp/debian/9/pxelinux
WORKDIR /usr/local/apache2/htdocs/opensdcp/debian/9/pxelinux

# Get pxelinux
RUN wget $DEBIAN_MIRROR/debian/dists/$DEBIAN_VERSION/main/installer-$DEBIAN_ARCH/current/images/netboot/debian-installer/$DEBIAN_ARCH/pxelinux.0
RUN wget $DEBIAN_MIRROR/debian/dists/$DEBIAN_VERSION/main/installer-$DEBIAN_ARCH/current/images/netboot/debian-installer/$DEBIAN_ARCH/bootnetx64.efi
RUN wget -r -nH --no-parent --cut-dirs=10 --reject="index.html*" $DEBIAN_MIRROR/debian/dists/$DEBIAN_VERSION/main/installer-$DEBIAN_ARCH/current/images/netboot/debian-installer/$DEBIAN_ARCH/boot-screens/
RUN wget -r -nH --no-parent --cut-dirs=10 --reject="index.html*" $DEBIAN_MIRROR/debian/dists/$DEBIAN_VERSION/main/installer-$DEBIAN_ARCH/current/images/netboot/debian-installer/$DEBIAN_ARCH/grub/

# Serve pxelinux
EXPOSE 80