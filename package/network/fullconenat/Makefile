#
# Copyright (C) 2018 Chion Tang <tech@chionlab.moe>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=fullconenat
PKG_RELEASE:=2

PKG_SOURCE_DATE:=2021-12-09
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/llccd/netfilter-full-cone-nat.git
PKG_SOURCE_VERSION:=869f146044632610de2e55d64801983bd5f30e62
PKG_MIRROR_HASH:=06ad98da50f414586b0921d2b4c863e3a32c37bfa40b479cef5f53823ebf40f1

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/iptables-mod-fullconenat
  SUBMENU:=Firewall
  SECTION:=net
  CATEGORY:=Network
  TITLE:=FULLCONENAT iptables extension
  DEPENDS:=+iptables +kmod-ipt-fullconenat
  MAINTAINER:=Chion Tang <tech@chionlab.moe>
endef

define Package/iptables-mod-fullconenat/install
	$(INSTALL_DIR) $(1)/usr/lib/iptables
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libipt_FULLCONENAT.so $(1)/usr/lib/iptables
endef

define Package/ip6tables-mod-fullconenat
  SUBMENU:=Firewall
  SECTION:=net
  CATEGORY:=Network
  TITLE:=FULLCONENAT ip6tables extension
  DEPENDS:=ip6tables +kmod-nf-nat6 +kmod-ipt-fullconenat
  MAINTAINER:=Chion Tang <tech@chionlab.moe>
endef

define Package/ip6tables-mod-fullconenat/install
	$(INSTALL_DIR) $(1)/usr/lib/iptables
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libip6t_FULLCONENAT.so $(1)/usr/lib/iptables
endef

define KernelPackage/ipt-fullconenat
  SUBMENU:=Netfilter Extensions
  TITLE:=FULLCONENAT netfilter module
  DEPENDS:=+kmod-nf-ipt +kmod-nf-nat
  MAINTAINER:=Chion Tang <tech@chionlab.moe>
  KCONFIG:=  \
	CONFIG_NF_CONNTRACK_EVENTS=y \
	CONFIG_NF_CONNTRACK_CHAIN_EVENTS=y
  FILES:=$(PKG_BUILD_DIR)/xt_FULLCONENAT.ko
endef

include $(INCLUDE_DIR)/kernel-defaults.mk

define Build/Prepare
	$(call Build/Prepare/Default)
	$(CP) ./files/Makefile $(PKG_BUILD_DIR)/
endef

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C "$(LINUX_DIR)" \
        CROSS_COMPILE="$(TARGET_CROSS)" \
        ARCH="$(LINUX_KARCH)" \
        M="$(PKG_BUILD_DIR)" \
        EXTRA_CFLAGS="$(BUILDFLAGS)" \
        modules
	$(call Build/Compile/Default)
endef

$(eval $(call BuildPackage,iptables-mod-fullconenat))
$(eval $(call BuildPackage,ip6tables-mod-fullconenat))
$(eval $(call KernelPackage,ipt-fullconenat))
