# Build Centos 7 based container for building OpendTect with gcc9
#
FROM centos:7 AS base_gcc1050
LABEL description="Wayne Mogg <wayne.mogg@gmail.com>"
LABEL maintainer="Wayne Mogg <wayne.mogg@gmail.com>"
RUN	sed -i s/mirror.centos.org/vault.centos.org/g /etc/yum.repos.d/CentOS-*.repo && \
	sed -i s/^#.*baseurl=http/baseurl=http/g /etc/yum.repos.d/CentOS-*.repo && \
	sed -i s/^mirrorlist=http/#mirrorlist=http/g /etc/yum.repos.d/CentOS-*.repo
RUN	ulimit -n 1024 && \
	yum -y update && \
	yum -y groupinstall 'Development Tools' && \
	yum -y install cmake tcsh redhat-lsb-core gmp-devel mpfr-devel libmpc-devel && \
	yum -y install 	"mesa-libGL-devel" \
			"mesa-libGLU-devel" \
			"fontconfig-devel" \
			"freetype-devel" \
			"zlib-devel" \
			"libXcomposite-devel" \
			"libXcursor-devel" \
			"libXrender-devel" \
			"libXtst-devel" \
			"alsa-lib" \
			"libXrandr" \
			"libXrandr-devel" \
			"libxkbcommon-devel" \
			"libxkbcommon-x11-devel" \
			"centos-release-scl" \
			"libXinerama-devel" \
			"https://rpms.remirepo.net/enterprise/remi-release-7.rpm" \
			"epel-release" && \
	yum -y install	"p7zip" \
			"p7zip-plugins" && \
	yum -y install --enablerepo=remi-php80 php php-cli && \
	yum clean all && \
	rm -rf /var/cache/yum

RUN	alternatives	--install /usr/local/bin/cmake cmake /Build/qt/Tools/CMake/bin/cmake 30 \
			--slave /usr/local/bin/ctest ctest /Build/qt/Tools/CMake/bin/ctest \
			--slave /usr/local/bin/cpack cpack /Build/qt/Tools/CMake/bin/cpack \
			--slave /usr/local/bin/ccmake ccmake /Build/qt/Tools/CMake/bin/ccmake \
			--family cmake

WORKDIR /opt
COPY inst_gcc_1050.tar.bz2 .
RUN tar -jxf inst_gcc_1050.tar.bz2 && rm inst_gcc_1050.tar.bz2

ENV TZ=Australia/Brisbane
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
ENV PATH=/opt/inst1050/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LD_LIBRARY_PATH=/opt/inst1050/lib64:/opt/inst1050/lib
ENV CC=/opt/inst1050/bin/gcc-10.5
ENV CXX=/opt/inst1050/bin/g++-10.5
