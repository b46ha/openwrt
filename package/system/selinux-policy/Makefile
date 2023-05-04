#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=selinux-policy
PKG_SOURCE_PROTO:=git

PKG_SOURCE_URL:=https://github.com/tidalf/selinux-policy.git
PKG_SOURCE_DATE:=2023-04-29
PKG_SOURCE_VERSION:=2b190268648bf0124eb4493eadc304089f4de33c
# use 'make package/selinux-policy-myfork/check V=s' to generate, or 'skip'
PKG_MIRROR_HASH:=skip

PKG_SOURCE_URL:=https://github.com/tidalf/selinux-policy.git
PKG_BUILD_DEPENDS:=secilc/host policycoreutils/host

PKG_MAINTAINER:=Tid <tidalf@ematome.com>
PKG_CPE_ID:=cpe:/a:defensec:selinux-policy
PKG_LICENSE:=Unlicense
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/selinux-policy
	SECTION:=system
	CATEGORY:=Base system
	TITLE:=SELinux security policy for OpenWrt
	URL:=https://github.com/tidalf/selinux-policy.git
	PKGARCH:=all
endef

define Package/selinux-policy/description
	Basic SELinux Security Policy designed specifically for
	OpenWrt and written in Common Intermediate Language.
endef

define Build/Compile
	$(call Build/Compile/Default,policy)
endef

define Package/selinux-policy/conffiles
/etc/selinux/config
endef

define Package/selinux-policy/install
	$(INSTALL_DIR) $(1)/etc/selinux/$(PKG_NAME)/contexts/files/
	$(INSTALL_DIR) $(1)/etc/selinux/$(PKG_NAME)/policy/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/customizable_types $(1)/etc/selinux/$(PKG_NAME)/contexts/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/file_contexts.subs_dist $(1)/etc/selinux/$(PKG_NAME)/contexts/files/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/file_contexts $(1)/etc/selinux/$(PKG_NAME)/contexts/files/
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/policy.* $(1)/etc/selinux/$(PKG_NAME)/policy/
	$(INSTALL_DATA) ./files/selinux-config $(1)/etc/selinux/config
endef

$(eval $(call BuildPackage,selinux-policy))
