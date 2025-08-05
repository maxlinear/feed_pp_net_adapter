#
# Copyright (C) 2020-2024 MaxLinear, Inc.
# Copyright (C) 2016 Intel Corporation
# Copyright (C) 2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=pp_net_adapter
PKG_VERSION:=1.0.20
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_PROJECT:=maxlinear
PKG_SOURCE_NAME:=pp_net_adapter
CONFIG_UGW_PKG_SOURCE_URL:=https://github.com
PKG_SOURCE_URL:=$(CONFIG_UGW_PKG_SOURCE_URL)/$(PKG_PROJECT)/$(PKG_SOURCE_NAME).git
PKG_MIRROR_HASH:=56e9809d8ba18e9f47c4884e717511788718e4a9b1899d486224badbb3706546
PKG_SOURCE_VERSION:=$(PKG_VERSION)
PKG_MAINTAINER:=MaxLinear
PKG_LICENSE:=GPL-2.0

PKG_BUILD_PARALLEL:=1
PKG_IS_KERNEL_MODULE=y
PKG_DEFAULT_CUSTOM_SOURCE_DIR:=$(TOPDIR)/pp_net_adapter/

-include $(INCLUDE_DIR)/package-version-override.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/pp_net_adapter
  SUBMENU:=MaxLinear
  TITLE:=Packet Processor Network Adapter
  DEPENDS:= +TARGET_intel_x86_lgm:kmod-packet_learn \
	    +TARGET_intel_x86_lgm:kmod-gwdpa-dpm
  MAINTAINER:=MaxLinear
  FILES:= $(PKG_BUILD_DIR)/pp_net_adapter.ko
  AUTOLOAD:=$(call AutoLoad,00,learning pp_net_adapter)
  MENU:=1
endef

define KernelPackage/pp_net_adapter/description
  Packet Processor Network Adapter
endef

define KernelPackage/pp_net_adapter/config
  $(call Package/kmod-pp_net_adapter/override_version)
  $(call Package/kmod-pp_net_adapter/override_source_path)
endef

define Build/Compile
	$(KERNEL_MAKE) M="$(PKG_BUILD_DIR)" modules
endef

define Build/Clean
	if [ -d $(PKG_BUILD_DIR) ]; then \
		$(MAKE) -C $(PKG_BUILD_DIR) KERNEL_DIR=$(LINUX_DIR) clean; \
		$(RM) -r $(PKG_BUILD_DIR)/ipkg-$(BOARD); \
	fi
endef

$(eval $(call KernelPackage,pp_net_adapter))
