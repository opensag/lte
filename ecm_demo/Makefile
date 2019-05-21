include $(TOPDIR)/rules.mk

# Name, version and release number
# The name and version of your package are used to define the variable to point to the build directory of your package: $(PKG_BUILD_DIR)
PKG_NAME:=ecm_demo
PKG_VERSION:=1.0.104
PKG_RELEASE:=1

# Source settings (i.e. where to find the source codes)
# This is a custom variable, used below
SOURCE_DIR:=./src

include $(INCLUDE_DIR)/package.mk

# Package definition; instructs on how and where our package will appear in the overall configuration menu ('make menuconfig')
define Package/ecm_demo
        SECTION:=base
        CATEGORY:=LTE Modules
        TITLE:=lte led control
endef

# Package description; a more verbose description on what our package does
define Package/ecm_demo/description
        A simple "LTE ECM" -application.
endef

# Package preparation instructions; create the build directory and copy the source code.
# The last command is necessary to ensure our preparation instructions remain compatible with the patching system.
define Build/Prepare
        mkdir -p $(PKG_BUILD_DIR)
        cp $(SOURCE_DIR)/* $(PKG_BUILD_DIR)
        $(Build/Patch)
endef

# Package build instructions; invoke the target-specific compiler to first compile the source file, and then to link the file into the final executable
define Build/Compile
        $(TARGET_CC) $(TARGET_CFLAGS) -c ecm_demo_atctl.c ecm_demo_msg.c ecm_demo_ttydev.c ecm_demo_aux.c ecm_demo_autocfg.c
	$(TARGET_AR) -crvs libecmcall.a ecm_demo_atctl.o ecm_demo_msg.o ecm_demo_ttydev.o ecm_demo_aux.o ecm_demo_autocfg.o
        $(TARGET_CC) $(TARGET_LDFLAGS) ecm_demo_main.c -g -v -static -L ./ libecmcall.a -o ECM_DEMO -lpthread -ldl -lrt
        $(TARGET_CC) $(TARGET_LDFLAGS) ecm_demo_mainauto.c -g -v -static -L ./ libecmcall.a -o ECM_DEMO_AUTO -lpthread -ldl -lrt
        rm -rf *.o
endef

# Package install instructions; create a directory inside the package to hold our executable, and then copy the executable we built previously into the folder
define Package/ecm_demo/install
        $(INSTALL_DIR) $(1)/usr/bin
        $(INSTALL_BIN) $(PKG_BUILD_DIR)/ECM_DEMO $(1)/usr/bin
        $(INSTALL_BIN) $(PKG_BUILD_DIR)/ECM_DEMO_AUTO $(1)/usr/bin
        $(INSTALL_DIR) $(1)/etc/init.d
        $(INSTALL_BIN) ./files/ecmdemo $(1)/etc/init.d/ecmdemo
endef

# This command is always the last, it uses the definitions and variables we give above in order to get the job done
$(eval	$(call	BuildPackage,ecm_demo))
