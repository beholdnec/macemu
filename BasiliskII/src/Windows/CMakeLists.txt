add_executable(build68k
    ../uae_cpu/build68k.c)

add_custom_command(
    OUTPUT ${CMAKE_CURRENT_SOURCE_DIR}/../uae_cpu/cpudefs.cpp
    COMMAND build68k >cpudefs.cpp
    DEPENDS ../uae_cpu/table68k
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../uae_cpu)

add_executable(gencpu
    ../uae_cpu/cpudefs.cpp
    ../uae_cpu/gencpu.c
    ../uae_cpu/readcpu.cpp)

add_custom_command(
    OUTPUT ${CMAKE_CURRENT_SOURCE_DIR}/../uae_cpu/cpustbl.cpp
    COMMAND gencpu
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../uae_cpu)

add_executable(BasiliskII
    clip_windows.cpp
    ether_windows.cpp
    extfs_windows.cpp
    main_windows.cpp
    posix_emu.cpp
    prefs_windows.cpp
    serial_windows.cpp
    sys_windows.cpp
    timer_windows.cpp
    user_strings_windows.cpp
    util_windows.cpp
    xpram_windows.cpp
    b2ether/packet32.cpp
    cdenable/cache.cpp
    cdenable/eject_nt.cpp
    cdenable/ntcd.cpp
    router/arp.cpp
    router/dump.cpp
    router/dynsockets.cpp
    router/ftp.cpp
    router/icmp.cpp
    router/iphelp.cpp
    router/ipsocket.cpp
    router/router.cpp
    router/tcp.cpp
    router/udp.cpp
    router/mib/interfaces.cpp
    router/mib/mibaccess.cpp
    ../adb.cpp
    ../audio.cpp
    ../cdrom.cpp
    ../disk.cpp
    ../emul_op.cpp
    ../ether.cpp
    ../extfs.cpp
    ../macos_util.cpp
    ../main.cpp
    ../prefs.cpp
    ../prefs_items.cpp
    ../rom_patches.cpp
    ../rsrc_patches.cpp
    ../scsi.cpp
    ../serial.cpp
    ../slot_rom.cpp
    ../sony.cpp
    ../timer.cpp
    ../user_strings.cpp
    ../video.cpp
    ../xpram.cpp
    ../CrossPlatform/sigsegv.cpp
    ../CrossPlatform/video_blit.cpp
    ../CrossPlatform/vm_alloc.cpp
    ../dummy/prefs_editor_dummy.cpp # TODO: Support GTK prefs editor under a build option
    ../dummy/scsi_dummy.cpp
    ../SDL/audio_sdl.cpp
    ../SDL/video_sdl.cpp
    ../slirp/bootp.c
    ../slirp/cksum.c
    ../slirp/debug.c
    ../slirp/if.c
    ../slirp/ip_icmp.c
    ../slirp/ip_input.c
    ../slirp/ip_output.c
    ../slirp/mbuf.c
    ../slirp/misc.c
    ../slirp/sbuf.c
    ../slirp/slirp.c
    ../slirp/socket.c
    ../slirp/tcp_input.c
    ../slirp/tcp_output.c
    ../slirp/tcp_subr.c
    ../slirp/tcp_timer.c
    ../slirp/tftp.c
    ../slirp/udp.c
    ../uae_cpu/basilisk_glue.cpp
    ../uae_cpu/cpudefs.cpp
    ../uae_cpu/cpuemu.cpp
    ../uae_cpu/cpustbl.cpp
    ../uae_cpu/newcpu.cpp
    ../uae_cpu/readcpu.cpp
    ../uae_cpu/fpu/fpu_ieee.cpp)

# TODO: Bring this back once we've found a good solution for GTK on Windows.
#add_executable(BasiliskIIGUI
#    prefs_editor_gtk.cpp)

set(SDL_INCLUDE_DIR "" CACHE STRING "Where to find SDL.h.")
set(SDL_LIBRARY_DIR "" CACHE STRING "Where to find SDL.lib.")

include_directories(. ${SDL_INCLUDE_DIR})
target_link_libraries(BasiliskII ${SDL_LIBRARY_DIR}/SDL.lib ${SDL_LIBRARY_DIR}/SDLmain.lib iphlpapi.lib ws2_32.lib)

add_definitions(
    -DDIRECT_ADDRESSING
    -DUNALIGNED_PROFITABLE
    -DFPU_IEEE
    -DHAVE_CONFIG_H
    -D_CRT_SECURE_NO_WARNINGS
    -D_UNICODE)
