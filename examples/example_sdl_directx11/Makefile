#
# Cross Platform Makefile
# Compatible with MSYS2/MINGW, Ubuntu 14.04.1 and Mac OS X
#
# You will need SDL2 (http://www.libsdl.org):
# Linux:
#   apt-get install libsdl2-dev
# Mac OS X:
#   brew install sdl2
# MSYS2:
#   pacman -S mingw-w64-i686-SDL2
#

#CXX = g++
#CXX = clang++

EXE = example_sdl_directx11
IMGUI_DIR = ../..
SOURCES = main.cpp
SOURCES += $(IMGUI_DIR)/imgui.cpp $(IMGUI_DIR)/imgui_demo.cpp $(IMGUI_DIR)/imgui_draw.cpp $(IMGUI_DIR)/imgui_tables.cpp $(IMGUI_DIR)/imgui_widgets.cpp
SOURCES += $(IMGUI_DIR)/backends/imgui_impl_sdl.cpp $(IMGUI_DIR)/backends/imgui_impl_dx11.cpp
OBJS = $(addsuffix .o, $(basename $(notdir $(SOURCES))))
UNAME_S := $(shell uname -s)
LINUX_GL_LIBS = -lGL

CXXFLAGS = -std=c++11 -I/usr/x86_64-w64-mingw32/include/SDL2 -I$(IMGUI_DIR) -I$(IMGUI_DIR)/backends -DUNICODE #-fno-threadsafe-statics -D__WIN32__ -D_REENTRANT -Dmain=SDL_main -I/usr/x86_64-w64-mingw32/include/SDL2 -I$(IMGUI_DIR) -I$(IMGUI_DIR)/backends
CXXFLAGS += -g -Wall -Wformat
LIBS =

##---------------------------------------------------------------------
## OPENGL ES
##---------------------------------------------------------------------

## This assumes a GL ES library available in the system, e.g. libGLESv2.so
# CXXFLAGS += -DIMGUI_IMPL_OPENGL_ES2
# LINUX_GL_LIBS = -lGLESv2
## If you're on a Raspberry Pi and want to use the legacy drivers,
## use the following instead:
# LINUX_GL_LIBS = -L/opt/vc/lib -lbrcmGLESv2

##---------------------------------------------------------------------
## BUILD FLAGS PER PLATFORM
##---------------------------------------------------------------------

# -mwindows -lSDL2 -lSDL2main -lmingw32 -ld3d11 -ld3dcompiler -lshell32 -pthread -lm
#LIBS += -mwindows

# CXXFLAGS += `sdl2-config --cflags`
ifeq ($(UNAME_S), Linux) #LINUX
	ECHO_MESSAGE = "Linux"
	CXXFLAGS += -static-libstdc++ -lmingw32 -lSDL2main -lSDL2 -ld3d11 -ld3dcompiler
	CFLAGS = $(CXXFLAGS)
endif

# ifeq ($(UNAME_S), Darwin) #APPLE
# 	ECHO_MESSAGE = "Mac OS X"
# 	LIBS += -framework OpenGL -framework Cocoa -framework IOKit -framework CoreVideo `sdl2-config --libs`
# 	LIBS += -L/usr/local/lib -L/opt/local/lib

# 	CXXFLAGS += `sdl2-config --cflags`
# 	CXXFLAGS += -I/usr/local/include -I/opt/local/include
# 	CFLAGS = $(CXXFLAGS)
# endif

# ifeq ($(OS), Windows_NT)
#     ECHO_MESSAGE = "MinGW"
#     LIBS += -lgdi32 -lopengl32 -limm32 `pkg-config --static --libs sdl2`

#     CXXFLAGS += `pkg-config --cflags sdl2`
#     CFLAGS = $(CXXFLAGS)
# endif

##---------------------------------------------------------------------
## BUILD RULES
##---------------------------------------------------------------------

%.o:%.cpp
	x86_64-w64-mingw32-g++ $(CXXFLAGS) -c -o $@ $<

%.o:$(IMGUI_DIR)/%.cpp
	x86_64-w64-mingw32-g++ $(CXXFLAGS) -c -o $@ $<

%.o:$(IMGUI_DIR)/backends/%.cpp
	x86_64-w64-mingw32-g++ $(CXXFLAGS) -c -o $@ $<

all: $(EXE)
	@echo Build complete for $(ECHO_MESSAGE)

$(EXE): $(OBJS)
	x86_64-w64-mingw32-g++ -o $@ $^ $(CXXFLAGS) $(LIBS)

clean:
	rm -f $(EXE) $(OBJS)
