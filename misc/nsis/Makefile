ifndef VERSION
VERSION=1.36_SVN
endif
ifndef RELEASE
RELEASE=0
endif
ifndef PLATFORM
PLATFORM=mingw32
endif
ifndef ARCH
ARCH=x86
endif
ifndef INSTALLDIR
INSTALLDIR=.
endif
ifndef USE_RENDERER_DLOPEN
USE_RENDERER_DLOPEN=1
endif
ifndef USE_OPENAL_DLOPEN
USE_OPENAL_DLOPEN=1
endif
ifndef USE_INTERNAL_ZLIB
USE_INTERNAL_ZLIB=1
endif
ifndef USE_INTERNAL_JPEG
USE_INTERNAL_JPEG=1
endif
ifndef SDLDLL
	ifeq ($(ARCH),x86_64)
		SDLDLL=SDL264.dll
	else
		SDLDLL=SDL2.dll
	endif
endif
ifndef OPENALDLL
	ifeq ($(ARCH),x86_64)
		OPENALDLL=OpenAL64.dll
	else
		OPENALDLL=OpenAL32.dll
	endif
endif

DEFINES=
ifeq ($(USE_RENDERER_DLOPEN),1)
	DEFINES+= -DUSE_RENDERER_DLOPEN
endif
ifeq ($(USE_OPENAL_DLOPEN),1)
	DEFINES+= -DUSE_OPENAL_DLOPEN
endif
ifeq ($(USE_INTERNAL_ZLIB),1)
	DEFINES+= -DUSE_INTERNAL_ZLIB
endif
ifeq ($(USE_INTERNAL_JPEG),1)
	DEFINES+= -DUSE_INTERNAL_JPEG
endif


all: ioquake3-$(VERSION)-$(RELEASE).$(ARCH).exe

ioquake3.$(ARCH).nsi: ioquake3.nsi.in
	sed 's/XXXVERSIONXXX/$(VERSION)/;s/XXXRELEASEXXX/$(RELEASE)/;s/mingw32/$(PLATFORM)/g;s/x86/$(ARCH)/g;s/SDL2.dll/$(SDLDLL)/g;s/OpenAL32.dll/$(OPENALDLL)/g' < $< > $@

ioquake3-$(VERSION)-$(RELEASE).$(ARCH).exe: ioquake3.$(ARCH).nsi
	makensis $(DEFINES) ioquake3.$(ARCH).nsi

clean:
	rm -rf *.exe ioquake3.$(ARCH).nsi

install:
	mkdir -p $(INSTALLDIR)
	mv ioquake3-$(VERSION)-$(RELEASE).$(ARCH).exe $(INSTALLDIR)

.PHONY: all clean

