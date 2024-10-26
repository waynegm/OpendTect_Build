GITHUB_USER = waynegm

ifeq ($(user),)
# USER retrieved from env, UID from shell.
USER ?= $(strip $(if $(USER),$(USER),nodummy))
UID ?= $(strip $(if $(shell id -u),$(shell id -u),4000))
GID ?= $(strip $(if $(shell id -g),$(shell id -g),4000))
else
# allow override by adding user= and/ or uid=  (lowercase!).
# uid= defaults to 0 if user= set (i.e. root).
USER = $(user)
UID = $(strip $(if $(uid),$(uid),0))
GID = $(strip $(if $(gid),$(gid),0))
endif

HDFDIR = /Build/bin/depends/hdf5/1.12.0
HDFOPT = -DHDF5_ROOT=$(HDFDIR)
LHDFOPT = -DHDF5_ROOT=$(CURDIR)/Build/loc_bin/HDF%/1.12.0
LOCAL64DIR = /Build/bin/local_64
LOCAL64OPT = -DGDAL_LIBRARY=$(LOCAL64DIR)/lib/libgdal.so -DGDAL_INCLUDE_DIR=$(LOCAL64DIR)/include -DGDAL_CONFIG=$(LOCAL64DIR)/bin/gdal-config
LOCAL66DIR = /Build/bin/local_66
LOCAL66OPT = -DGDAL_LIBRARY=$(LOCAL66DIR)/lib/libgdal.so -DGDAL_INCLUDE_DIR=$(LOCAL66DIR)/include -DGDAL_CONFIG=$(LOCAL66DIR)/bin/gdal-config -DPYTHON_EXECUTABLE=/opt/seismic/OpendTect_6/Python/bin/python
#LOCALPYTHON = -DPYTHON_EXECUTABLE=/opt/seismic/OpendTectPro_6/Python/bin/python
LOCALPYTHON = -DPython_ROOT_DIR=/opt/seismic/OpendTectPro_6/Python -DOD_USEODPYBIND=ON
QT596DIR = /Build/bin/qt5.9.6/5.9.6/gcc_64
QT5150DIR = /Build/qt/5.15.2/gcc_64
LQT5150DIR = $(CURDIR)/Build/qt/5.15.2/gcc_64
QT596OPTS = -DDESIRED_QT_VERSION=5 -DCMAKE_PREFIX_PATH=$(QT596DIR)/lib/cmake
QT5150OPTS = -DDESIRED_QT_VERSION=5 -DCMAKE_PREFIX_PATH=$(QT5150DIR)/lib/cmake
OSG363DIR = /Build/bin/depends/osg/osg-3.6.3
OSG365DIR = /Build/bin/depends/osg/osg-3.6.5
LOSG365DIR = $(CURDIR)/Build/loc_bin/osg-3.6.5
OSG363OPT = -DOSG_DIR:PATH=$(OSG363DIR)
OSG365OPT = -DOSG_DIR:PATH=$(OSG365DIR)
LOSG365OPT = -DOSG_DIR:PATH=$(LOSG365DIR)
PROJOPT = -DPROJ_DIR:PATH=/Build/bin/proj9/inst-9.0.0 -DSQLITE_DIR:PATH=/Build/bin/sqlite/inst-3.38
GLOPT = -DOpenGL_GL_PREFERENCE=LEGACY
ZOPT = -DZLIB_INCLUDE_DIR=$(DEPS)/zlib/inst-1.2.13_rhel7_1050/include -DZLIB_LIBRARY=$(DEPS)/zlib/inst-1.2.13_rhel7_1050/lib/libz.so
CMK_OSG365 = cd /Build/src/OpenSceneGraph-OpenSceneGraph-3.6.5;cmake -DCMAKE_INSTALL_PREFIX:PATH=$(OSG365DIR) .;make -j3 all install
LCMK_OSG365 = cd Build/loc_bld/OpenSceneGraph-OpenSceneGraph-3.6.5;cmake -DCMAKE_INSTALL_PREFIX:PATH=$(LOSG365DIR) .;make -j3 all install
UNPACK_QT596 = cd /Build/src;./qt-opensource-linux-x64-5.9.6.run --verbose --script qt596-noninteractive.qs -platform minimal
DEPS = /Build/bin/depends
ODGCC9 = $(GLOPT) -DOSG_DIR:PATH=$(DEPS)/osg/inst-365_rhel7_950 -DHDF5_ROOT=$(DEPS)/hdf5/inst-1.14.0_rhel7_950 -DPROJ_DIR:PATH=$(DEPS)/proj9/inst-9.3.0_rhel7_950 -DSQLite3_ROOT:PATH=$(DEPS)/sqlite/inst-3.44.0_rhel7_950
ODGCC10 = $(GLOPT) -DOSG_DIR:PATH=$(DEPS)/osg/inst-365_rhel7_1050 -DHDF5_ROOT=$(DEPS)/hdf5/inst-1.14.3_rhel7_1050 -DPROJ_DIR:PATH=$(DEPS)/proj9/inst-9.3.0_rhel7_1050 -DSQLite3_ROOT:PATH=$(DEPS)/sqlite/inst-3.44.2_rhel7_1050
RSYNC = rsync -a $(CURDIR)/Build/src/$(BRANCH) $(CURDIR)/Build/bld/
LRSYNC = rsync -a $(CURDIR)/Build/src/$(BRANCH) $(CURDIR)/Build/loc_bld/


CMAKE_PLUGIN_DEPS = mkdir -p /Build/bld/plugindeps; cd /Build/bld/plugindeps; cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/PluginDeps/Release -DOpendTect_DIR=/opt/seismic/OpendTect_7rc/7.0.0 $(ODGCC10) /Build/src/WMPlugin_Deps
CMAKE_PLUGIN_DEPSDEV = mkdir -p /Build/bld/plugindepsdev; cd /Build/bld/plugindepsdev; cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/PluginDeps/Debug -DOpendTect_DIR=/Build/bin/od7.0 $(ODGCC10) /Build/src/WMPlugin_Deps
CMAKE_BRANCH_PLUGIN66 = mkdir -p /Build/bld/plugin66; cd /Build/bld/plugin66;cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/ODPlugins/6.6.0 -DOpendTect_DIR=/opt/seismic/OpendTect_6/6.6.0 $(LOCAL66OPT) /Build/src/plugin66
CMAKE_BRANCH_PLUGIN66DEV = mkdir -p /Build/bld/plugin66dev;cd /Build/bld/plugin66dev;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odpro6.6 -DOpendTect_DIR=/Build/bin/odpro6.6 $(LOCAL66OPT) /Build/src/plugin66
CMAKE_BRANCH_PLUGIN = mkdir -p /Build/bld/plugin; cd /Build/bld/plugin;cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/ODPlugins/7.0.0 -DCMAKE_PREFIX_PATH:PATH=/Build/bin/PluginDeps/Release -DOpendTect_DIR=/opt/seismic/OpendTect_7rc/7.0.0 $(ODGCC10) -DWMDEPS_DIR=/Build/bin/PluginDeps/Release /Build/src/plugin
CMAKE_BRANCH_PLUGINDEV = mkdir -p /Build/bld/plugindev;cd /Build/bld/plugindev;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/ODPlugins/7.0.0 -DCMAKE_PREFIX_PATH:PATH=/Build/bin/PluginDeps/Debug -DOpendTect_DIR=/Build/bin/od7.0 $(ODGCC10) -DWMDEPS_DIR=/Build/bin/PluginDeps/Debug /Build/src/plugin
CMAKE_BRANCH_VSGK = cd /Build/src/VectorSet_GK_Processing;mkdir -p build;cd build; cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/ODPlugins/vsgk_6.6.0 -DOpendTect_DIR=/opt/seismic/OpendTect_6/6.6.0 ..

CMAKE_BRANCH_B2NDIO = mkdir -p /Build/bld/b2ndio; cd /Build/bld/b2ndio;cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/ODPlugins/7.0.0 -DOpendTect_DIR=/opt/seismic/OpendTect_7rc/7.0.0 $(ODGCC10) /Build/src/b2ndio
CMAKE_BRANCH_B2NDIODEV = mkdir -p /Build/bld/b2ndiodev;cd /Build/bld/b2ndiodev;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/ODPlugins/7.0.0 -DOpendTect_DIR=/Build/bin/od7.0 $(ODGCC10) /Build/src/b2ndio

CMAKE_BRANCH_ODCHARTS = mkdir -p /Build/bld/ODCharts;cd /Build/bld/ODCharts;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odmain -DOpendTect_DIR=/Build/bin/odmain -DQTDIR=/$(QT5150DIR)/ /Build/src/ODCharts

CMAKE_BRANCH_ODPYBINDDEV = mkdir -p /Build/bld/odpybinddev;cd /Build/bld/odpybinddev;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odmain -DOpendTect_DIR=/Build/src/odmain -DOD_BINARY_BASEDIR:PATH=/Build/bld/odmain_bld -DOD_USEODPYBIND=ON $(LOCALPYTHON) /Build/src/odpybind
CMAKE_BRANCH_ODPYBIND = mkdir -p /Build/bld/odpybind;cd /Build/bld/odpybind;cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odpybind -DOpendTect_DIR=/opt/seismic/OpendTect_6/6.6.0  -DOD_USEODPYBIND=ON  $(LOCALPYTHON) /Build/src/odpybind

CMKODMAIN = mkdir -p /Build/bld/odmain_bld;cd /Build/bld/odmain_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odmain -DQTDIR=/$(QT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(ZOPT) $(ODGCC10) /Build/src/odmain
CMKODPROMAIN = mkdir -p /Build/bld/odpro_main_bld;cd /Build/bld/odpro_main_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odpro_main -DQTDIR=/$(QT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(ZOPT) $(ODGCC10) /Build/src/odmain
CMKDGBMAIN = mkdir -p /Build/bld/dgbmain_bld;cd /Build/bld/dgbmain_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odpro_main -DOD_BINARY_BASEDIR:PATH=/Build/bld/odpro_main_bld $(ODGCC10) $(LOCALPYTHON) -DQTDIR=/$(QT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(ZOPT) /Build/src/dgbmain
CMKOD7 = mkdir -p /Build/bld/od7.0_bld;cd /Build/bld/od7.0_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/od7.0 -DQTDIR=/$(QT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(ZOPT) $(ODGCC10) /Build/src/od7.0
CMKODPRO7 = mkdir -p /Build/bld/odpro7.0_bld;cd /Build/bld/odpro7.0_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odpro7.0 -DQTDIR=/$(QT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(ZOPT) $(ODGCC10) /Build/src/od7.0
CMKDGB7 = mkdir -p /Build/bld/dgb7.0_bld;cd /Build/bld/dgb7.0_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odpro7.0 -DOD_BINARY_BASEDIR:PATH=/Build/bld/odpro7.0_bld $(LOCALPYTHON) -DQTDIR=/$(QT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(ZOPT) $(ODGCC10) /Build/src/dgb7.0
CMKOD = mkdir -p /Build/bld/od$(BRANCH)_bld;cd /Build/bld/od$(BRANCH)_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/od$(BRANCH) $(GLOPT) $(OSG365OPT) -DQTDIR=/$(QT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(ZOPT) $(HDFOPT) /Build/src/od$(BRANCH)
CMKODPRO = mkdir -p /Build/bld/odpro$(BRANCH)_bld;cd /Build/bld/odpro$(BRANCH)_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odpro$(BRANCH) $(GLOPT) $(OSG365OPT) -DQTDIR=/$(QT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(ZOPT) $(HDFOPT) /Build/src/od$(BRANCH)
CMKDGB = mkdir -p /Build/bld/dgb$(BRANCH)_bld;cd /Build/bld/dgb$(BRANCH)_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=/Build/bin/odpro$(BRANCH)  -DOD_BINARY_BASEDIR:PATH=/Build/bld/odpro$(BRANCH)_bld $(GLOPT) $(OSG365OPT) -DQTDIR=/$(QT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(ZOPT) $(HDFOPT) /Build/src/dgb$(BRANCH)
LMK = mkdir -p $(CURDIR)/Build/loc_bld/$(BRANCH)_bld;cd $(CURDIR)/Build/loc_bld/$(BRANCH)_bld;cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX:PATH=$(CURDIR)/Build/loc_bin/$(BRANCH) $(GLOPT) $(LOSG365OPT) -DQTDIR=/$(LQT5150DIR)/ -DQt5_EXCLUDE_STATIC_DEPENDENCIES=ON $(LHDFOPT) $(CURDIR)/Build/src/$(BRANCH)

USERID = $(shell id -u):$(shell(id -g)
DOCKEROPTS = --rm --mount type=bind,src=${CURDIR}/..,dst=/Build --user $(UID):$(GID) --mount type=bind,src="/home/$(USER)",dst="/home/$(USER)" --workdir "/home/$(USER)" --volume="/etc/group:/etc/group:ro" --volume="/etc/passwd:/etc/passwd:ro" --volume="/etc/shadow:/etc/shadow:ro"
DOCKEROPTS_6.6 = $(DOCKEROPTS) --volume="/opt/seismic/OpendTect_6/6.6.0:/opt/seismic/OpendTect_6/6.6.0:ro" --volume="/opt/seismic/OpendTectPro_6/Python:/opt/seismic/OpendTectPro_6/Python:ro"
DOCKEROPTS_7 = $(DOCKEROPTS) --volume="/opt/seismic/OpendTect_7rc/7.0.0:/opt/seismic/OpendTect_7rc/7.0.0:ro" --volume="/opt/seismic/OpendTectPro_7/Python:/opt/seismic/OpendTectPro_7/Python:ro"


.PHONY: base base_shell osg qt596 osgqt596  6.4.4 6.5 master odtclone

base_gcc5.4:
	docker build -t base_gcc5.4 Docker_gcc5.4

base_gcc5.4_shell:
	docker run $(DOCKEROPTS) -it base_gcc5.4 /bin/bash

base_gcc9:
	docker build -t base_gcc9 Docker_gcc9

base_gcc9_shell:
	docker run $(DOCKEROPTS_7) -it base_gcc9

base_gcc1050:
	docker build -t base_gcc1050 Docker_gcc1050

base_gcc1050_shell:
	docker run $(DOCKEROPTS_7) -it base_gcc1050

testit:
	docker run $(DOCKEROPTS) base_gcc1050 /bin/bash -c "gcc-10.5 -v"

newdgb6.6:
	git clone --single-branch --depth 1 -b dgb6.6 https://github.com/OpendTect/dgb.git Build/src/dgb6.6

newdgb7.0:
	git clone --single-branch --depth 1 -b dgb7.0 https://github.com/OpendTect/dgb.git dgb7.0

newdgbmain:
	git clone --single-branch --depth 1 -b main https://github.com/OpendTect/dgb.git dgbmain

new6.6:
	git clone --single-branch --depth 1 -b od6.6 https://github.com/OpendTect/OpendTect.git Build/src/od6.6

new7.0:
	git clone --single-branch --depth 1 -b od7.0 https://github.com/OpendTect/OpendTect.git od7.0

newmain:
	git clone --single-branch --depth 1 -b main https://github.com/OpendTect/OpendTect.git odmain

newplugin:
	git clone --recursive --single-branch --depth 1 -b main https://github.com/waynegm/OpendTect-Plugins.git Build/src/plugin

newplugin66:
	git clone --recursive --single-branch --depth 1 -b 6.6 https://github.com/waynegm/OpendTect-Plugins.git Build/src/plugin66

cmkVSGK:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "$(CMAKE_BRANCH_VSGK)"

cmkplugin66:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "$(CMAKE_BRANCH_PLUGIN66)"

cmkplugin66dev:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "$(CMAKE_BRANCH_PLUGIN66DEV)"

cmkplugin:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "$(CMAKE_BRANCH_PLUGIN)"

cmkplugindev:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "$(CMAKE_BRANCH_PLUGINDEV)"

cmkb2ndio:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "$(CMAKE_BRANCH_B2NDIO)"

cmkb2ndiodev:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "$(CMAKE_BRANCH_B2NDIODEV)"

cmkplugindeps:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "$(CMAKE_PLUGIN_DEPS)"

cmkplugindepsdev:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "$(CMAKE_PLUGIN_DEPSDEV)"

cmkodcharts:
	docker run $(DOCKEROPTS) base_gcc5.4 /bin/bash -c "$(CMAKE_BRANCH_ODCHARTS)"

cmkodpybind:
	docker run $(DOCKEROPTS) base_gcc5.4 /bin/bash -c "$(CMAKE_BRANCH_ODPYBIND)"

cmkodpybinddev:
	docker run $(DOCKEROPTS) base_gcc5.4 /bin/bash -c "$(CMAKE_BRANCH_ODPYBINDDEV)"

cmkodmain:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/src/odmain; cmake --preset default ."

cmkodpromain:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/src/odmain; cmake --preset default-pro ."

cmkdgbmain:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "mkdir -p /Build/bld/dgbmain;cd /Build/bld/dgbmain; cmake --preset default-dgbmain /Build/src/dgbmain"

cmkod7:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/src/od7.0; cmake --preset default ."

cmkodpro7:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/src/od7.0; cmake --preset default-pro ."

cmkdgb7:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "mkdir -p /Build/bld/dgb7.0;cd /Build/bld/dgb7.0; cmake --preset default-dgb7 /Build/src/dgb7.0"

cmkod:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "$(CMKOD)"

cmkodpro:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "$(CMKODPRO)"

cmkdgb:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "$(CMKDGB)"

bld5:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "cd /Build/bld/$(BRANCH)_bld;make -j 14 install"

bld:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/bld/$(BRANCH);cmake --build .; cmake --install ."

rmkplugin66:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "cd /Build/bld/plugin66;make -j 14 install"

rmkplugin66dev:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "cd /Build/bld/plugin66dev;make -j 14 install"

rmkplugin:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/bld/plugin;make -j 14 install"

rmkplugindev:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/bld/plugindev;make -j 14 install"

rmkb2ndio:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/bld/b2ndio;make -j 14 install"

rmkb2ndiodev:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/bld/b2ndiodev;make -j 14 install"

rmkplugindeps:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/bld/plugindeps;make -j 14"

rmkplugindepsdev:
	docker run $(DOCKEROPTS_7) base_gcc1050 /bin/bash -c "cd /Build/bld/plugindepsdev;make -j 14"

rmkvsgk:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "cd /Build/src/VectorSet_GK_Processing/build;make -j 14 install"

bldcharts:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "cd /Build/bld/ODCharts;make -j 14 install"

bldodpybind:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "cd /Build/bld/odpybind;make -j 14 install"
bldodpybinddev:
	docker run $(DOCKEROPTS_6.6) base_gcc5.4 /bin/bash -c "cd /Build/bld/odpybinddev;make -j 14 install"

