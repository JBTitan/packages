include $(TOPDIR)/rules.mk

PKG_NAME:=agent-proxy
PKG_VERSION:=1.96
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://git.kernel.org/pub/scm/utils/kernel/kgdb/agent-proxy.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/agent-proxy
  SECTION:=extra
  CATEGORY:=Network
  TITLE:=GDB network proxy tool
  URL:=https://git.kernel.org/cgit/utils/kernel/kgdb/agent-proxy.git/
endef

define Package/agent-proxy/description
  A kernel GDB proxy
endef

define Package/agent-proxy/install
        $(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
        $(INSTALL_BIN) $(PKG_BUILD_DIR)/agent-proxy $(1)/usr/sbin/
	$(INSTALL_BIN) ./files/agent-proxy.init $(1)/etc/init.d/agent-proxy
endef

define Package/agent-proxy/postinst
	#!/bin/sh
	# check if we are on real system
	if [ -z "$${IPKG_INSTROOT}" ]; then
	    echo "Enabling rc.d symlink for mrelay"
	    /etc/init.d/agent-proxy enable
	fi
	exit 0
endef

define Package/agent-proxy/prerm
        #!/bin/sh
	# check if we are on real system
	if [ -z "$${IPKG_INSTROOT}" ]; then
	     echo "Removing rc.d symlink for mrelay"
	     /etc/init.d/agent-proxy disable
	fi
	exit 0
endef

$(eval $(call BuildPackage,agent-proxy))
