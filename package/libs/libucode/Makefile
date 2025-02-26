include $(TOPDIR)/rules.mk

PKG_NAME:=libucode
PKG_VERSION:=2023-01-01
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/openwrt/libucode.git
PKG_SOURCE_VERSION:=master
PKG_MIRROR_HASH:=skip

include $(INCLUDE_DIR)/package.mk

define Package/libucode
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=libucode - 轻量级模板引擎库
  DEPENDS:=+libubox
endef

define Package/libucode/description
  libucode 是一个轻量级的模板引擎库，用于动态生成内容。
  它通常与 uhttpd 一起使用，为 OpenWrt 提供动态网页支持。
endef

define Build/Configure
    true
endef

define Build/Compile
    $(MAKE) -C $(PKG_BUILD_DIR) \
        CC="$(TARGET_CC)" \
        CFLAGS="$(TARGET_CFLAGS)" \
        LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/libucode/install
    $(INSTALL_DIR) $(1)/usr/lib
    $(INSTALL_BIN) $(PKG_BUILD_DIR)/libucode.so $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libucode))