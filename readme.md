Build with  
CFLAGS=" -O2 -G0 `${PSPDEV}/psp/bin/sdl-config --cflags`" CXXFLAGS=" -O2 -G0 `${PSPDEV}/psp/bin/sdl-config --cflags`" LDFLAGS="-L${PSPSDK}/lib `${PSPDEV}/psp/bin/sdl-config --libs`" ./configure -host=psp --with-sdl-prefix=$(psp-config --psp-prefix)

PSP Does not support execlp / ftruncate 

execlp is in sdlmain for -editconf and launchcaptures function  

functions that are disabled for PSP are defined as NOT_PSP