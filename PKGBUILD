# Contributor: Christian Himpel <chressie at gmail dot com>
# Maintainer: Johannes Hanika <hanatos at gmail dot com>

pkgname=darktable-git
pkgrel=1
pkgver=20091116
pkgdesc="Utility to organize and develop raw images"
arch=('i686' 'x86_64')
url="http://darktable.sf.net/"
license=('GPL3')
depends=('gegl' 'libglade' 'exiv2' 'lcms')
makedepends=('git')
provides=('darktable')
conflicts=('darktable')
source=()
md5sums=()

_gitroot=git://darktable.git.sf.net/gitroot/darktable/darktable
_gitname=darktable

build() {
  # Linking fails with --as-needed linker option
  #if [ ! -z "$LDFLAGS" ]; then
  #  LDFLAGS=${LDFLAGS/-Wl,--as-needed/}
  #  LDFLAGS=${LDFLAGS/,--as-needed/}
  #fi
  unset LDFLAGS

  # Use maintainers optimizations
  unset CFLAGS
  unset CXXFLAGS

  if [ -d $srcdir/$_gitname ]; then
    cd $srcdir/$_gitname && git pull origin
  else
    git clone $_gitroot $srcdir/$_gitname
  fi

  cd $srcdir/$_gitname
  git clean -dfx
  ./autogen.sh || return 1
  ./configure --prefix=/usr || return 1
  make || return 1
  make DESTDIR=$pkgdir install || return 1
  mkdir -p $pkgdir/usr/share/doc/$pkgname-$pkgver
  install -m644 AUTHORS LICENSE NEWS README TODO $pkgdir/usr/share/doc/$pkgname-$pkgver || return 1
}
