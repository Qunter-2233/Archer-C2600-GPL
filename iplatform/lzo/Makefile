#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lzo
PKG_VERSION:=2.06
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
# PKG_SOURCE_URL:=http://www.oberhumer.com/opensource/lzo/download/
PKG_MD5SUM:=95380bd4081f85ef08c5209f4107e9f8

PKG_FIXUP:=libtool
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/liblzo
  SECTION:=libs
  CATEGORY:=TP-LINK iplatform apps
  TITLE:=A real-time data compression library
  URL:=http://www.oberhumer.com/opensource/lzo/
endef

define Package/liblzo/description
 LZO is a data compression library which is suitable for data de-/compression
 in real-time. This means it favours speed over compression ratio.
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--enable-shared \
		--enable-static \
	)
endef

TARGET_CFLAGS += $(FPIC)
MAKE_FLAGS += CFLAGS_O="$(TARGET_CFLAGS)"

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/include/lzo $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/liblzo2.{a,so*} $(1)/usr/lib/
endef

define Package/liblzo/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/liblzo2.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,liblzo))
