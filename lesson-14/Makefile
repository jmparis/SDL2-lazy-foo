# Compute compilation flags

ifeq ($(CXX),g++)

GCCVERSION		:= $(shell gcc --version | grep ^gcc | sed 's/^.* //g')
ifeq ($(shell printf '%s\n%s\n' "$(GCCVERSION)" "10.0.0" | sort -V -C; echo $$?),0)
	# Use old flag for gcc <= 10.0.0
	CPPFLAGS	+=	-std=c++2a
else
	CPPFLAGS	+=	-std=c++20
endif
	CPPFLAGS	+=	-O3
	CPPFLAGS	+=	-DMESSAGE='"Compiled with GCC"'
endif

ifeq ($(CXX),clang)
	CPPFLAGS	+=	-std=c++20
	CPPFLAGS	+=	-O3
	CPPFLAGS	+=	-DMESSAGE='"Compiled with Clang"'
endif

CPPFLAGS+=	-Wall -Wextra -Werror
#CPPFLAGS+=	$(shell pkg-config --cflags sdl2)
CPPFLAGS+=	$(shell pkg-config --cflags SDL2_image)

#LDLIBS	+=	$(shell pkg-config --libs   sdl2)
LDLIBS	+=	$(shell pkg-config --libs   SDL2_image)
LDLIBS	+=	-lstdc++

SRCS	=	$(shell echo *.cpp)
OBJS	=	$(subst .cpp,.o,$(SRCS))
EXES	=	$(subst .cpp,,$(SRCS))

$(EXES):	$(OBJS)

clean:
	$(RM) $(EXES)
	$(RM) $(OBJS)
