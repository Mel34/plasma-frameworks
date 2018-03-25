# $Id$
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=plasma-framework
pkgver=5.44.0
pkgrel=1.1
pkgdesc='Plasma library and runtime components based upon KF5 and Qt5'
arch=(x86_64)
url='https://community.kde.org/Frameworks'
license=(LGPL)
depends=(qt5-quickcontrols kactivities kdeclarative kwayland kirigami2)
makedepends=(extra-cmake-modules qt5-tools kdoctools python doxygen)
groups=(kf5)
source=("https://download.kde.org/stable/frameworks/${pkgver%.*}/$pkgname-$pkgver.tar.xz"{,.sig}
001-thumbnails.patch)
sha256sums=('bfb647e4119764872f29685ec84206e4031d9d1aaeba2a539eeec7aa5eaed9d1'
            'SKIP'
            '5d8926a5ca409c4a8ae163bd4d98aa4fcc0f65aa74c9a2ae3e1a9ac898ffaed8')
validpgpkeys=(53E6B47B45CEA3E0D5B7457758D0EE648A48B3BB) # David Faure <faure@kde.org>

prepare() {
  mkdir -p build
  cd $pkgname-$pkgver
  msg "Thumbnails patch" #https://phabricator.kde.org/D10251?id=29832
  patch -p1 -i ../001-thumbnails.patch
}

build() {
  cd build
  cmake ../$pkgname-$pkgver \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DBUILD_TESTING=OFF \
    -DBUILD_QCH=ON
  make
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
}
