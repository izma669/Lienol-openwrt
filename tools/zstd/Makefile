include $(TOPDIR)/rules.mk

PKG_NAME:=zstd
PKG_VERSION:=1.5.0

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/facebook/zstd/releases/download/v$(PKG_VERSION)
PKG_HASH:=5194fbfa781fcf45b98c5e849651aa7b3b0a008c6b72d4a0db760f3002291e94

PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE
PKG_CPE_ID:=cpe:/a:facebook:zstandard

CMAKE_SOURCE_SUBDIR:=build/cmake
HOST_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_HOST_OPTIONS += \
	-DBUILD_TESTING=OFF \
	-DCMAKE_C_COMPILER_LAUNCHER="" \
	-DCMAKE_C_COMPILER=$(HOSTCC_NOCACHE) \
	-DZSTD_LEGACY_SUPPORT=OFF

$(eval $(call HostBuild))
