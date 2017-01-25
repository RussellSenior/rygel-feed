#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=vala
PKG_VERSION:=0.35.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNOME/vala/0.35/
PKG_MD5SUM:=2d61184a2b483fe82f6f588271cd95575ed039e830a4d80d46774124b2e2b982

PKG_BUILD_DEPENDS:=glib2/host vala/host
HOST_BUILD_DEPENDS:=glib2/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

TARGET_LDFLAGS+=\
        -Wl,-rpath-link=$(STAGING_DIR)/usr/lib

define Package/vala
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=C-sharp like language for the GObject system
  URL:=http://live.gnome.org/Vala
endef

define Package/vala/description
Vala is a C-sharp like language for the GObject system. This package contains
the Vala-to-C compiler.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

VALA_VER := 0.35.3

define Build/InstallDev
	$(INSTALL_DIR) \
		$(1)/usr/share/vala-$(VALA_VER)/vapi \
		$(1)/usr/lib \
		$(1)/usr/share/pkgconfig \
		$(1)/usr/bin

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/vala-$(VALA_VER)/vapi/* \
		$(1)/usr/share/vala-$(VALA_VER)/vapi

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/libvala-$(VALA_VER).{so*,la} \
		$(1)/usr/lib

	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/{vala,vala-$(VALA_VER),valac,valac-$(VALA_VER),vapicheck,vapicheck-$(VALA_VER),vapigen,vapigen-$(VALA_VER),vala-gen-introspect,vala-gen-introspect-$(VALA_VER)} \
		$(1)/usr/bin

	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/pkgconfig/*.pc \
		$(1)/usr/share/pkgconfig
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,vala))
