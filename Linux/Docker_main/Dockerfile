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
		"p7zip-plugins" && \
	dnf -y clean all


WORKDIR /opt
COPY inst_gcc_1050.tar.bz2 .
RUN tar --no-same-owner -jxf inst_gcc_1050.tar.bz2 && rm inst_gcc_1050.tar.bz2
ENV TZ=Australia/Brisbane
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
ENV PATH=/opt/inst1050/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LD_LIBRARY_PATH=/opt/inst1050/lib64:/opt/inst1050/lib
ENV CC=/opt/inst1050/bin/gcc-10.5
ENV CXX=/opt/inst1050/bin/g++-10.5
