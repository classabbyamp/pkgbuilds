# Maintainer: Galen Gold <galen@galengold.me>

pkgname=js8call
pkgver=0.7.2
pkgrel=1
pkgdesc="Software for ragchewing and message-passing based on WSJT-X"
arch=('i686' 'x86_64')
url="https://groups.io/g/js8call"
license=('GPL-3')
makedepends=(cmake asciidoc asciidoctor)
depends=(qt5-base qt5-multimedia qt5-serialport libusb libusb-compat gcc-fortran libpulse libpng fftw)
source=($pkgname-$pkgver.tar.gz::https://bitbucket.org/widefido/wsjtx/get/v$pkgver.tar.gz)
md5sums=('8fb9b91a00f367c7c02befed99ec22d5')

build() {
    mv $srcdir/widefido-wsjtx* $srcdir/$pkgname-$pkgver
    mkdir -p $srcdir/build
    cd $srcdir/build
    cmake -Wno-dev -Dhamlib_LIBRARY_DIRS=/usr/lib/ -DCMAKE_INSTALL_PREFIX=${pkgdir}/usr -DCMAKE_BUILD_TYPE=Release $srcdir/$pkgname-$pkgver
    cmake --build .
}

package() {
    cd ${srcdir}/build
    patch < ../../install-dirs.patch
    sed -i.bak1 's%file(INSTALL DESTINATION "/usr/share/applications"%file(INSTALL DESTINATION "${CMAKE_INSTALL_PREFIX}/share/applications"%' cmake_install.cmake
    sed -i.bak2 's%file(INSTALL DESTINATION "/usr/share/pixmaps"%file(INSTALL DESTINATION "${CMAKE_INSTALL_PREFIX}/share/pixmaps"%' cmake_install.cmake
    sed -i.bak3 '\%file(INSTALL DESTINATION "/usr/bin"%d' cmake_install.cmake
    cmake --build . --target install
}
