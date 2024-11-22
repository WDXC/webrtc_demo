cmake_minimum_required(VERSION 3.22)
project(MyProject)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_IGNORE_PATH "/usr/lib;/usr/lib64;/lib;/lib64")
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
set(CMAKE_C_COMPILER /home/moyun/mine/depot_tools/webrtc_checkout/src/third_party/llvm-build/Release+Asserts/bin/clang)
set(CMAKE_CXX_COMPILER /home/moyun/mine/depot_tools/webrtc_checkout/src/third_party/llvm-build/Release+Asserts/bin/clang++)
set(CMAKE_LINKER /home/moyun/mine/depot_tools/webrtc_checkout/src/third_party/llvm-build/Release+Asserts/bin/llvm-ar)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++ -fno-rtti -g -Wno-deprecated-declarations -Wunused-command-line-argument -v -Wl,--allow-shlib-undefined")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -B/home/moyun/mine/depot_tools/webrtc_checkout/src/build/linux/debian_sid_amd64-sysroot/usr/lib/x86_64-linux-gnu")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -B/home/moyun/mine/depot_tools/webrtc_checkout/src/build/linux/debian_sid_amd64-sysroot/usr/lib/gcc/x86_64-linux-gnu/7/")
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --force_fieldtrials=WebRTC-FooFeature/Enabled/")



#set(CMAKE_SYSROOT /home/moyun/mine/depot_tools/webrtc_checkout/src/build/linux/debian_sid_amd64-sysroot/usr/lib/gcc/x86_64-linux-gnu/7/)

# shortcut path
set(WEBRTC_SOURCE "/home/moyun/mine/depot_tools/webrtc_checkout/src")
set(LOCAL_SRC /home/moyun/mine/webrtc/src/samples/peerconnection/client)

set(CMAKE_SYSROOT ${WEBRTC_SOURCE}/tools/clang/translation_unit/test_files/sysroot)
#set(CMAKE_VERBOSE_MAKEFILE ON)
#add_definitions(-D_USE_MATH_DEFINES -D_GNU_SOURCE )
add_definitions(
    -DUSE_UDEV
    -DUSE_AURA=1
    -DUSE_GLIB=1
    -DUSE_NSS_CERTS=1
    -DUSE_X11=1
    -D_FILE_OFFSET_BITS=64
    -D_LARGEFILE_SOURCE
    -D_LARGEFILE64_SOURCE
    -D_GNU_SOURCE
    -DCR_CLANG_REVISION=\"n356235-f7f1abdb-1\"
    -D__STDC_CONSTANT_MACROS
    -D__STDC_FORMAT_MACROS
    -D_LIBCPP_ABI_UNSTABLE
    -D_LIBCPP_DISABLE_VISIBILITY_ANNOTATIONS
    -D_LIBCXXABI_DISABLE_VISIBILITY_ANNOTATIONS
    -D_LIBCPP_ENABLE_NODISCARD
    -D_LIBCPP_DEBUG=0
    -DCR_LIBCXX_REVISION=375504
    -DCR_SYSROOT_HASH=d6879d611f3dcf3da8dd92e080029394aa30bc42
    -D_DEBUG
    -DDYNAMIC_ANNOTATIONS_ENABLED=1
    -DWEBRTC_ENABLE_PROTOBUF=1
    -DWEBRTC_INCLUDE_INTERNAL_AUDIO_DEVICE
    -DRTC_ENABLE_VP9
    -DHAVE_SCTP
    -DWEBRTC_NON_STATIC_TRACE_EVENT_HANDLERS=1
    -DWEBRTC_POSIX
    -DWEBRTC_LINUX
    -DABSL_ALLOCATOR_NOTHROW=1
    -DABSL_FLAGS_STRIP_NAMES=0
    -DHAVE_WEBRTC_VIDEO
)

# 包含头文件目录
include_directories(
    ${CMAKE_SOURCE_DIR}/src
    ${WEBRTC_SOURCE}/
    ${WEBRTC_SOURCE}/third_party/jsoncpp/source/include
    ${WEBRTC_SOURCE}/third_party/jsoncpp/generated
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/include/glib-2.0/
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/lib/x86_64-linux-gnu/glib-2.0/include
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/include/gtk-3.0/
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/include/cairo/
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/include/pango-1.0/
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/include/gdk-pixbuf-2.0/
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/include/graphene-1.0/
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/lib/x86_64-linux-gnu/graphene-1.0/include/
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/include/atk-1.0
    ${WEBRTC_SOURCE}/third_party/libvpx/source/libvpx/third_party/libyuv/include/
    ${WEBRTC_SOURCE}/third_party/crashpad/crashpad/compat/non_win/
    ${WEBRTC_SOURCE}/third_party/abseil-cpp
    ${WEBRTC_SOURCE}/third_party/llvm-build/Release+Asserts/lib/clang/10.0.0/include
    ${WEBRTC_SOURCE}/buildtools/third_party/libc++/trunk/include
    ${WEBRTC_SOURCE}/buildtools/third_party/libc++abi/trunk/include
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/include
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/include/x86_64-linux-gnu
    ${CMAKE_SYSROOT}/usr/local/include
    ${CMAKE_SYSROOT}/include
    ${CMAKE_SYSROOT}/usr/include

)

# 查找并链接库
link_directories(
    ${WEBRTC_SOURCE}/out/Debug_N64/obj
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/rtc_base
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/third_party/abseil-cpp/absl
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/buildtools/third_party/libc++/libc++
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/buildtools/third_party/libc++abi/libc++abi
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/third_party/jsoncpp/jsoncpp
    ${WEBRTC_SOURCE}/third_party/llvm-build/Release+Asserts/lib
    ${WEBRTC_SOURCE}/third_party/instrumented_libs/binaries/msan-chained-origins-noble-lib/
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/api
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/rtc_base/rtc_json
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/test/platform_video_capturer
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/test/video_test_common
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/lib/x86_64-linux-gnu
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/third_party/abseil-cpp
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/test
    ${WEBRTC_SOURCE}/out/Debug_N64/obj/system_wrappers
    ${WEBRTC_SOURCE}/build/linux/debian_sid_amd64-sysroot/usr/lib/gcc/x86_64-linux-gnu/7
    ${CMAKE_SYSROOT}/usr/lib/gcc/x86_64-linux-gnu/4.6/../../../../include/c++/4.6
    ${CMAKE_SYSROOT}/usr/lib/gcc/x86_64-linux-gnu/4.6/../../../../include/x86_64-linux-gnu/c++/4.6
    ${CMAKE_SYSROOT}/usr/lib/gcc/x86_64-linux-gnu/4.6/../../../../include/x86_64-unknown-linux-gnu/c++/4.6
    ${CMAKE_SYSROOT}/usr/lib/gcc/x86_64-linux-gnu/4.6/../../../../include/c++/4.6/backward
)


add_executable(run 
          ${LOCAL_SRC}/conductor.cc
          ${LOCAL_SRC}/defaults.cc
          ${LOCAL_SRC}/peer_connection_client.cc
          ${LOCAL_SRC}/linux/main.cc
          ${LOCAL_SRC}/linux/main_wnd.cc
    )

# 链接库
target_link_libraries(run PRIVATE
    -fuse-ld=lld
    webrtc
    gio-2.0
    jsoncpp
    glib-2.0
    gtk-3
    gdk-3
    cairo
    absl
    ffi
    vcm
    c++
    c++abi
    rtc_json
    gobject-2.0
    X11
    Xcomposite
    Xext
    Xrender
    c
    c_nonshared
    pango-1.0
    jingle_peerconnection_api
    field_trial
    rtc_base
    pangoft2-1.0
    pangocairo-1.0
    gmodule-2.0
    cairo-gobject
)


# 定义宏
target_compile_definitions(run PRIVATE
    WEBRTC_POSIX
    WEBRTC_LINUX
)

target_link_options(run PRIVATE -Wl,-rpath-link,${BPATH}/crtbegin.o)
target_link_options(run PRIVATE -Wl,-rpath-link,${BPATH}/libgcc.a)
target_link_options(run PRIVATE -Wl,-rpath-link,${BPATH}/libgcc_s.so)
