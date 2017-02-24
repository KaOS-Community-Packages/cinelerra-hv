pkgname=cinelerra-hv
_basename=cinelerra
pkgver=6
pkgrel=1
pkgdesc="A complete audio and video production environment"
arch=('x86_64')
url="https://sourceforge.net/projects/heroines/"
license=('GPL')
depends=(
    'alsa-lib'
    'bzip2'
    'expat'
    'fontconfig'
    'freeglut'
    'freetype2'
    'gcc-libs'
    'glibc'
    'glu'
    'libdrm'
    'libgl'
    'libpng'
    'libpng12'
    'libva'
    'libx11'
    'libxau'
    'libxcb'
    'libxdamage'
    'libxdmcp'
    'libxext'
    'libxfixes'
    'libxft'
    'libxrender'
    'libxshmfence'
    'libxv'
    'libxxf86vm'
    'mesa'
    'ncurses'
    'openexr'
    'termcap'
    'texinfo'
    'xz'
    'zlib'
)
makedepends=(
    'gcc'
    'libtool'
    'linux-api-headers'
    'nasm'
    'yasm'
)
source=(
    "https://svwh.dl.sourceforge.net/project/heroines/${_basename}-${pkgver}-src.tar.xz"
    'kaos.patch'
    'cinelerra.desktop'
    'cinelerra.png'
)
md5sums=(
    '8688a2138c442288ad721ca8ec620820'
    '135e61f1d6776749b19d2f657093d38e'
    'f91515830ab8f9723b4ab49004b45095'
    '4c6e4051552b11c2951f5f1767e76163'
)

prepare() {
    cd "${srcdir}/${_basename}-${pkgver}"
    patch -Np1 -i "${srcdir}/kaos.patch"
}

build() {
    cd "${srcdir}/${_basename}-${pkgver}"
    ./configure
    # forces include of lzma.h in quicktime/thirdparty/ffmpeg-3.0.2/libavcodec/tiff.c
    export CONFIG_LZMA=1
    make
}

package() {
    cd "${srcdir}/${_basename}-${pkgver}"

    make install

    # install puts it in bin. no way to configure prefix or select DESTDIR.
    mkdir -p "${pkgdir}/usr/lib"
    mv bin "${pkgdir}/usr/lib/${_basename}"

    mkdir -p "${pkgdir}/usr/bin"
    ln -s "/usr/lib/${_basename}/${_basename}" "${pkgdir}/usr/bin/${_basename}"

    install -Dm644 "${srcdir}/cinelerra.desktop" "${pkgdir}/usr/share/applications/cinelerra.desktop"    
    install -Dm644 "${srcdir}/cinelerra.png" "${pkgdir}/usr/share/icons/hicolor/48x48/apps/cinelerra.png"
}
