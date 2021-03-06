include $(TOPDIR)/rules.mk

PKG_NAME:=UnblockNeteaseMusicGo
PKG_VERSION:=0.2.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/cnsilvan/UnblockNeteaseMusic.git
PKG_SOURCE_VERSION:=0c1c2f7ed9ae6277a10b1b1bba81101f552af509
PKG_MAINTAINER:=Silvan <cnsilvan@gmail.com>

PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/cnsilvan/UnblockNeteaseMusic
GO_PKG_LDFLAGS:=-s -w
GO_PKG_LDFLAGS_X:= \
	$(GO_PKG)/version.Version=$(PKG_VERSION)

export GO111MODULE=on
export GOPROXY=https://goproxy.io
# export GOPROXY=https://mirrors.aliyun.com/goproxy/

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Revive Netease Cloud Music (Golang)
	DEPENDS:=$(GO_ARCH_DEPENDS)
	URL:=https://github.com/cnsilvan/UnblockNeteaseMusic
	SUBMENU:=NeteaseMusic
endef

define Package/$(PKG_NAME)/description
Revive Netease Cloud Music (Golang)
endef

define Build/Prepare
	tar -zxvf $(DL_DIR)/$(PKG_SOURCE) -C $(BUILD_DIR)/$(PKG_NAME) --strip-components 1
endef

define Build/Configure

endef

define Build/Compile
	$(eval GO_PKG_BUILD_PKG:=$(GO_PKG))
	$(call GoPackage/Build/Configure)
	$(call GoPackage/Build/Compile)
	$(STAGING_DIR_HOST)/bin/upx --lzma --best $(GO_PKG_BUILD_BIN_DIR)/UnblockNeteaseMusic
	chmod +wx $(GO_PKG_BUILD_BIN_DIR)/UnblockNeteaseMusic
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/UnblockNeteaseMusic $(1)/usr/bin/UnblockNeteaseMusic
	$(INSTALL_DIR) $(1)/usr/share/UnblockNeteaseMusicGo
	$(CP) ./files/* $(1)/usr/share/UnblockNeteaseMusicGo/
	
endef
$(eval $(call GoBinPackage,$(PKG_NAME)))
$(eval $(call BuildPackage,$(PKG_NAME)))
