project(dosbox)
cmake_minimum_required(VERSION 3.14)


find_package(SDL)
include_directories(include . ${SDL_INCLUDE_DIRS})
add_definitions(-Dmain=SDL_main -DPSP_FW_VERSION=660)

add_library(CPU OBJECT src/cpu/callback.cpp src/cpu/cpu.cpp src/cpu/flags.cpp src/cpu/modrm.cpp src/cpu/core_full.cpp
                src/cpu/paging.cpp src/cpu/core_normal.cpp src/cpu/core_simple.cpp src/cpu/core_prefetch.cpp 
                src/cpu/core_dyn_x86.cpp src/cpu/core_dynrec.cpp)


add_library(DEBUG OBJECT src/debug/debug.cpp src/debug/debug_gui.cpp src/debug/debug_disasm.cpp src/debug/debug_win32.cpp )

add_library(DOS OBJECT src/dos/dos.cpp src/dos/dos_devices.cpp src/dos/dos_execute.cpp src/dos/dos_files.cpp src/dos/dos_ioctl.cpp src/dos/dos_memory.cpp
                src/dos/dos_misc.cpp src/dos/dos_classes.cpp src/dos/dos_programs.cpp src/dos/dos_tables.cpp src/dos/drives.cpp src/dos/drive_virtual.cpp
                src/dos/drive_local.cpp src/dos/drive_cache.cpp src/dos/drive_fat.cpp src/dos/drive_iso.cpp src/dos/dos_mscdex.cpp src/dos/dos_keyboard_layout.cpp
                src/dos/cdrom.cpp src/dos/cdrom_ioctl_win32.cpp src/dos/cdrom_aspi_win32.cpp src/dos/cdrom_ioctl_linux.cpp src/dos/cdrom_image.cpp src/dos/cdrom_ioctl_os2.cpp)



add_library(FPU OBJECT src/fpu/fpu.cpp)


add_library(GUI OBJECT src/gui/sdl_mapper.cpp src/gui/render.cpp src/gui/render_scalers.cpp src/gui/midi.cpp src/gui/sdl_gui.cpp)


    add_library(HARDWARE OBJECT src/hardware/adlib.cpp src/hardware/dma.cpp src/hardware/gameblaster.cpp src/hardware/hardware.cpp src/hardware/iohandler.cpp 
                         src/hardware/joystick.cpp src/hardware/keyboard.cpp src/hardware/memory.cpp src/hardware/mixer.cpp src/hardware/pcspeaker.cpp
                         src/hardware/pic.cpp src/hardware/sblaster.cpp src/hardware/tandy_sound.cpp src/hardware/timer.cpp
                         src/hardware/vga.cpp src/hardware/vga_attr.cpp src/hardware/vga_crtc.cpp src/hardware/vga_dac.cpp src/hardware/vga_draw.cpp src/hardware/vga_gfx.cpp
                         src/hardware/vga_other.cpp src/hardware/vga_memory.cpp src/hardware/vga_misc.cpp src/hardware/vga_seq.cpp src/hardware/vga_xga.cpp src/hardware/vga_s3.cpp 
                         src/hardware/vga_tseng.cpp src/hardware/vga_paradise.cpp src/hardware/cmos.cpp src/hardware/disney.cpp src/hardware/gus.cpp src/hardware/mpu401.cpp
                         src/hardware/ipx.cpp src/hardware/ipxserver.cpp src/hardware/dbopl.cpp)


add_library(MAME OBJECT src/hardware/mame/sn76496.cpp src/hardware/mame/saa1099.cpp )


add_library(serial OBJECT src/hardware/serialport/directserial.cpp src/hardware/serialport/libserial.cpp src/hardware/serialport/serialdummy.cpp src/hardware/serialport/serialport.cpp 
                   src/hardware/serialport/softmodem.cpp src/hardware/serialport/misc_util.cpp src/hardware/serialport/nullmodem.cpp)

add_library(ints OBJECT src/ints/mouse.cpp src/ints/xms.cpp src/ints/ems.cpp src/ints/int10.cpp src/ints/int10_char.cpp src/ints/int10_memory.cpp src/ints/int10_misc.cpp
                        src/ints/int10_modes.cpp src/ints/int10_vesa.cpp src/ints/int10_pal.cpp src/ints/int10_put_pixel.cpp src/ints/int10_video_state.cpp
                        src/ints/int10_vptable.cpp src/ints/bios.cpp src/ints/bios_disk.cpp src/ints/bios_keyboard.cpp )

    add_library(gui_tk OBJECT src/libs/gui_tk/gui_tk.cpp)

    add_library(misc OBJECT src/misc/cross.cpp src/misc/messages.cpp src/misc/programs.cpp src/misc/setup.cpp src/misc/support.cpp)

    add_library(shell OBJECT src/shell/shell.cpp src/shell/shell_batch.cpp src/shell/shell_cmds.cpp src/shell/shell_misc.cpp)

    add_library(DOSBOX OBJECT src/dosbox.cpp)

    add_executable(dosbox src/gui/sdlmain.cpp )
    target_link_libraries(dosbox LINK_PUBLIC DOSBOX CPU DEBUG DOS FPU GUI HARDWARE MAME serial ints gui_tk misc shell -lSDLmain ${SDL_LIBRARIES} -lGL -lpspdebug -lz -lpng -lpspgu -lpspaudio -lpspctrl -lpspirkeyb -lpspvfpu
                                            -lpspge -lpspdisplay -lpsppower -lpsphprm
    )

    create_pbp_file(
        TARGET dosbox
        ICON_PATH NULL
        BACKGROUND_PATH NULL
        PREVIEW_PATH NULL
        TITLE Dosbox 0.74-3
        BUILD_PRX
        )