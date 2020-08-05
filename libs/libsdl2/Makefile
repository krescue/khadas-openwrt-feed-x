include $(TOPDIR)/rules.mk

PKG_NAME:=SDL2
PKG_VERSION:=2.0.12
PKG_RELEASE:=1

#http://www.libsdl.org/release/SDL2-2.0.12.tar.gz

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.libsdl.org/release/
PKG_MD5SUM:=e52086d1b508fa0b76c52ee30b55bec4

PKG_FIXUP:=libtool
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libsdl2
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Simple DirectMedia Layer
  URL:=http://www.libsdl.org
  DEPENDS:=+DirectFB +zlib +libpthread
endef

define Package/libsdl2/description
 SDL is a library that allows programs portable low level access to a video
 framebuffer, audio output, mouse, and keyboard.
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--enable-libc 
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include $(1)/usr/lib/pkgconfig
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/SDL* \
		$(1)/usr/include/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libSDL*.{a,so*} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig


	$(INSTALL_DIR) $(1)/usr/share/aclocal
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/aclocal/* \
		$(1)/usr/share/aclocal/

	$(INSTALL_DIR) $(1)/host/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/sdl-config \
		$(1)/host/bin

	$(SED) 's,^\(exec_prefix\|prefix\)=.*,\1=\"$(STAGING_DIR)/usr/\",g' \
		$(1)/host/bin/sdl-config
endef

define Package/libsdl2/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libSDL*.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libsdl2))

