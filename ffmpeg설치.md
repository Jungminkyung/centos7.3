```
reference : https://trac.ffmpeg.org/wiki/CompilationGuide/Centos
작성일 2019-01-10

yum install autoconf automake bzip2 cmake freetype-devel gcc gcc-c++ git libtool make mercurial pkgconfig zlib-devel


cd ~/ffmpeg_sources
curl -O -L https://www.nasm.us/pub/nasm/releasebuilds/2.14.02/nasm-2.14.02.tar.bz2
tar xvfj nasm-2.14.02.tar.bz2
cd nasm-2.14.02
./autogen.sh
./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin"
make
make install



cd ~/ffmpeg_sources
curl -O -L http://www.tortall.net/projects/yasm/snapshots/v1.3.0.6.g1962/yasm-1.3.0.6.g1962.tar.gz
tar xzvf yasm-1.3.0.6.g1962.tar.gz
cd yasm-1.3.0.6.g1962
./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin"
make
make install


cd ~/ffmpeg_sources
git clone --depth 1 https://git.videolan.org/git/x264.git
cd x264
PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --enable-static
make
make install


cd ~/ffmpeg_sources
hg clone https://bitbucket.org/multicoreware/x265
cd ~/ffmpeg_sources/x265/build/linux
cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX="$HOME/ffmpeg_build" -DENABLE_SHARED:bool=off ../../source
make
make install



cd ~/ffmpeg_sources
git clone --depth 1 https://github.com/mstorsjo/fdk-aac
cd fdk-aac
autoreconf -fiv
./configure --prefix="$HOME/ffmpeg_build" --disable-shared
make
make install



cd ~/ffmpeg_sources
curl -O -L http://downloads.sourceforge.net/project/lame/lame/3.100/lame-3.100.tar.gz
tar xzvf lame-3.100.tar.gz
cd lame-3.100
./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --disable-shared --enable-nasm
make
make install




cd ~/ffmpeg_sources
curl -O -L https://archive.mozilla.org/pub/opus/opus-1.3.tar.gz
tar xzvf opus-1.3.tar.gz
cd opus-1.3
./configure --prefix="$HOME/ffmpeg_build" --disable-shared
make
make install




cd ~/ffmpeg_sources
curl -O -L http://downloads.xiph.org/releases/ogg/libogg-1.3.3.tar.gz
tar xzvf libogg-1.3.3.tar.gz
cd libogg-1.3.3
./configure --prefix="$HOME/ffmpeg_build" --disable-shared
make
make install




cd ~/ffmpeg_sources
curl -O -L http://downloads.xiph.org/releases/vorbis/libvorbis-1.3.6.tar.gz
tar xzvf libvorbis-1.3.6.tar.gz
cd libvorbis-1.3.6
./configure --prefix="$HOME/ffmpeg_build" --with-ogg="$HOME/ffmpeg_build" --disable-shared
make
make install



cd ~/ffmpeg_sources
git clone --depth 1 https://chromium.googlesource.com/webm/libvpx
cd libvpx
./configure --prefix="$HOME/ffmpeg_build" --disable-examples --disable-unit-tests --enable-vp9-highbitdepth --as=yasm
make
make install

cd ~/ffmpeg_sources

git clone https://git.ffmpeg.org/ffmpeg.git ffmpeg

cd ffmpeg
PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
  --prefix="$HOME/ffmpeg_build" \
  --pkg-config-flags="--static" \
  --extra-cflags="-I$HOME/ffmpeg_build/include" \
  --extra-ldflags="-L$HOME/ffmpeg_build/lib" \
  --extra-libs=-lpthread \
  --extra-libs=-lm \
  --bindir="$HOME/bin" \
  --enable-gpl \
  --enable-libfdk_aac \
  --enable-libfreetype \
  --enable-libmp3lame \
  --enable-libopus \
  --enable-libvorbis \
  --enable-libvpx \
  --enable-libx264 \
  --enable-libx265 \
  --enable-nonfree 
  
make
make install
hash -r

####
configure에러날때

freetype오류때문에 ffmpeg설치 진행이 안됨.(2019-01-10) 
yum remove freetype*
삭제후에 되는 서버에서 아래 내용을 복사해온다(2.4.11-15.el7 버전.아래링크에서 다운로드후에 알맞은 위치에 위치시켜준다....) .
다운주소 https://github.com/Jungminkyung/centos7.3/blob/master/freetype2.zip


/usr/bin/freetype-config
/usr/lib64/pkgconfig/freetype2.pc
/usr/lib64/girepository-1.0/freetype2-2.0.typelib
/usr/share/doc/freetype-2.4.11
/usr/share/doc/freetype-devel-2.4.11
/usr/share/aclocal/freetype2.m4
/usr/include/freetype2
/usr/include/freetype2/freetype
/usr/include/freetype2/freetype/freetype.h
ffmpeg configure다시 시도.
```


