# Maintainer: Andrea Scarpino <andrea@archlinux.org>

pkgname=libqsystemd-git
pkgver=20120211
pkgrel=1
pkgdesc="A library that provides a Qt implementation of the systemd's DBus API"
arch=('i686' 'x86_64')
url="http://majewsky.wordpress.com/2011/08/11/proof-of-concept-systemd-dataengine-plasma/"
license=('GPL')
depends=('kdelibs' 'systemd' 'python2')
makedepends=('git' 'cmake' 'automoc4')
provides=('libqsystemd')
conflicts=('libqsystemd')

_gitroot="git://anongit.kde.org/libqsystemd.git"
_gitname="libqsystemd"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/build"
  mkdir "$srcdir/build"
  cd "$srcdir/build"

  cmake ../${_gitname} \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=`kde4-config --prefix`
  make
}

package() {
  cd "$srcdir/build"
  make DESTDIR="$pkgdir" install
}
