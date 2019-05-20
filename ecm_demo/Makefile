include $(TOPDIR)/rules.mk

PKG_NAME:=ecm_demo
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)
PKG_CONFIG_DEPENDS:=+ libpthread

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/ecm_demo
  SECTION:=base
  CATEGORY:=LTE Modules
  DEPENDS:=+libpthread
  TITLE:= lte led control
endef

define Package/ecm_demo/description
  4G LTE lED CONTROL
endef

TARGET_LDFLAGS:= -lpthread  

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Package/ecm_demo/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ECM_DEMO $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ECM_DEMO_AUTO $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/ecmdemo $(1)/etc/init.d/ecmdemo
endef


$(eval $(call BuildPackage,ecm_demo))
