#
# Copyright (C) 2019 IOPSYS
#

include $(TOPDIR)/rules.mk

PKG_NAME:=uspd
PKG_VERSION:=1.0.3

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=19ac73922e57d10c13e1bc2eb5ac653953804087
PKG_SOURCE_URL:=https://dev.iopsys.eu/iopsys/uspd.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=IOPSYS Dev <dev@iopsys.eu>

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/uspd
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=USP ubus backend
  DEPENDS:=+libubox +ubus +libbbfdm
endef

define Package/uspd/description
 Ubus based backend for TR-369/USP which can be used by other USP agents
 running on top of it.
endef

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/usr/include \
	-D_GNU_SOURCE

#define Build/Prepare
#        $(CP) -rf ./uspd/* $(PKG_BUILD_DIR)/
#endef

define Package/uspd/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_BIN) ./files/uspd.init $(1)/etc/init.d/uspd
	$(INSTALL_CONF) ./files/uspd.config $(1)/etc/config/uspd
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/uspd $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,uspd))