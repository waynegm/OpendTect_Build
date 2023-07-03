# Build Centos 7 based container for building OpendTect with gcc9
#
FROM centos:7 AS base_gcc9
LABEL description="Wayne Mogg <wayne.mogg@gmail.com>"
LABEL maintainer="Wayne Mogg <wayne.mogg@gmail.com>"
RUN	yum -y update && \
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
			"libxkbcommon-x11-devel" && \
	yum -y install centos-release-scl && \
	yum clean all && \
	rm -rf /var/cache/yum

RUN	yum -y update && \
	yum -y install libXinerama-devel  && \
	yum clean all && \
	rm -rf /var/cache/yum

RUN	yum -y update && \
	alternatives	--install /usr/local/bin/cmake cmake /Build/qt/Tools/CMake/bin/cmake 30 \
			--slave /usr/local/bin/ctest ctest /Build/qt/Tools/CMake/bin/ctest \
			--slave /usr/local/bin/cpack cpack /Build/qt/Tools/CMake/bin/cpack \
			--slave /usr/local/bin/ccmake ccmake /Build/qt/Tools/CMake/bin/ccmake \
			--family cmake && \
	yum clean all && \
	rm -rf /var/cache/yum

WORKDIR /opt
COPY ../../bin/depends/inst_gcc_950.tar.bz2 .
RUN tar -jxf inst_gcc_950.tar.bz2 && rm inst_gcc_950.tar.bz2

ENV TZ=Australia/Brisbane
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
ENV PATH=/opt/inst950/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LD_LIBRARY_PATH=/opt/inst950/lib64:/opt/inst950/lib
ENV CC=/opt/inst950/bin/gcc-9.5
ENV CXX=/opt/inst950/bin/g++-9.5
