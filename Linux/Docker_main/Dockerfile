FROM rockylinux:8 AS opendtect-bld-main
LABEL description="Container for building OpendTect main branch"
RUN	dnf -y install tcsh bzip2 git glibc-devel epel-release && \
	/usr/bin/crb enable && \
	dnf -y --enablerepo=devel --enablerepo=powertools install \
		"cups-devel" \
		"libatomic" \
		"libX11-devel" \
		"libxkbfile" \
		"libxkbcommon-x11-devel" \
		"xcb-util-cursor-devel" \
		"xcb-util-devel" \
		"xcb-util-image-devel" \
		"xcb-util-keysyms-devel" \
		"xcb-util-renderutil-devel" \
		"xcb-util-wm-devel" \
		"fontconfig-devel" \
		"mesa-libGL-devel" \
		"mesa-libGLU-devel" \
		"libXrandr-devel" \
		"libXinerama-devel"
RUN	dnf -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm && \
	dnf -y module install php:remi-8.3 && \
	dnf -y --enablerepo=devel --enablerepo=powertools install \
		"alsa-lib" \
		"nss" \
		"nss-util" \
		"nspr" \
		"libXcomposite" \
		"libXdamage" \
		"libXtst" \
		"libXi" \
		"p7zip" \
		"p7zip-plugins" \
		"gcc-toolset-13" && \
	dnf -y clean all
RUN	dnf -y install \
		"gcc-toolset-13" \
		"cmake" \
		"ninja" && \
	dnf -y clean all


ENV TZ=Australia/Brisbane
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
