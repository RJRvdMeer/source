include $(TOPDIR)/rules.mk

PKG_NAME:=ubox
PKG_VERSION:=2016-08-17
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=$(LEDE_GIT)/project/ubox.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=34c597b8f478a4937fa041bf9da988990314ea85
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.xz
PKG_MIRROR_MD5SUM:=d200eef6356129451336e8bb2a204341d3873b5db211c2a4cfc6178fe4220f38
CMAKE_INSTALL:=1

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=

PKG_MAINTAINER:=John Crispin <john@phrozen.org>

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

TARGET_LDFLAGS += $(if $(CONFIG_USE_GLIBC),-lrt)

define Package/ubox
  SECTION:=base
  CATEGORY:=Base system
  DEPENDS:=+libubox +ubusd +ubus +libubus +libuci +USE_GLIBC:librt
  TITLE:=OpenWrt system helper toolbox
endef

define Package/ubox/install
	$(INSTALL_DIR) $(1)/sbin $(1)/usr/sbin $(1)/lib $(1)/usr/bin $(1)/etc/init.d

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/{kmodloader,validate_data} $(1)/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/getrandom $(1)/usr/bin/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/libvalidate.so $(1)/lib

	$(LN) ../../sbin/kmodloader $(1)/usr/sbin/rmmod
	$(LN) ../../sbin/kmodloader $(1)/usr/sbin/insmod
	$(LN) ../../sbin/kmodloader $(1)/usr/sbin/lsmod
	$(LN) ../../sbin/kmodloader $(1)/usr/sbin/modinfo
	$(LN) ../../sbin/kmodloader $(1)/usr/sbin/modprobe

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/{logd,logread} $(1)/sbin/
	$(INSTALL_BIN) ./files/log.init $(1)/etc/init.d/log
endef

$(eval $(call BuildPackage,ubox))
