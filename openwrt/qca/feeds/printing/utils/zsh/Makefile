#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=zsh
PKG_VERSION:=5.0.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@SF/zsh
PKG_MD5SUM:=b8f2ad691acf58b3252225746480dcad

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/zsh
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=The Z shell
  DEPENDS:=+libncurses +librt
  URL:=http://www.zsh.org/
endef

define Package/zsh/description
        Zsh is a UNIX command interpreter (shell) usable as an interactive
        login  shell  and  as a shell script command processor. Of the standard
        shells, zsh most closely resembles ksh but includes many enhancements.
        Zsh has command line editing, builtin spelling correction, programmable
        command completion, shell functions (with autoloading), a history
        mechanism, and a host of other features.
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--bindir=/bin \
		--disable-etcdir \
		--disable-gdbm \
		--with-term-lib="ncurses" \
	)
	# Do not install these functions:
	$(SED) 's, Completion/AIX/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	$(SED) 's, Completion/BSD/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	$(SED) 's, Completion/Cygwin/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	$(SED) 's, Completion/Darwin/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	$(SED) 's, Completion/Debian/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	$(SED) 's, Completion/Mandriva/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	$(SED) 's, Completion/Redhat/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	$(SED) 's, Completion/Solaris/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	$(SED) 's, Completion/X/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	$(SED) 's, Completion/openSUSE/\*/\*,,g' $(PKG_BUILD_DIR)/config.modules
	# After mucking with 'config.modules', one must call
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)" prep
endef

define Package/zsh/postinst
#!/bin/sh
grep zsh $${IPKG_INSTROOT}/etc/shells || \
	echo "/bin/zsh" >> $${IPKG_INSTROOT}/etc/shells
endef

define Package/zsh/install
	$(INSTALL_DIR) $(1)/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/zsh $(1)/bin/
	$(INSTALL_DIR) $(1)/usr/share/zsh/$(PKG_VERSION)
	$(CP) $(PKG_INSTALL_DIR)/usr/share/zsh/$(PKG_VERSION)/* $(1)/usr/share/zsh/$(PKG_VERSION)/
endef

$(eval $(call BuildPackage,zsh))
