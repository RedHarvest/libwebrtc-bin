include ../../VERSION

BASE_DIR := $(CURDIR)/../..

include ../env.mk

TARGET_OS ?= macos
TARGET_CPU ?= x64

include ../common.mk

.PHONY: all
all: clean build package

.PHONY: package
package: common-package

.PHONY: copy
copy: common-copy

.PHONY: patch
patch: common-patch

.PHONY: build
build: patch
	cd $(SRC_DIR) && \
	gn gen $(BUILD_DIR) --args='$(CC_WRAPPER) target_os="mac" enable_stripping=true enable_dsyms=false is_debug=false treat_warnings_as_errors=false $(RTC_USE_H264) rtc_include_tests=false rtc_build_examples=false is_component_build=false use_rtti=true libcxx_abi_unstable=false' && \
	ninja -C $(BUILD_DIR) && \
	ninja -C $(BUILD_DIR) \
	  builtin_audio_decoder_factory \
	  default_task_queue_factory \
	  native_api \
	  default_codec_factory_objc \
	  peerconnection \
	  videocapture_objc
