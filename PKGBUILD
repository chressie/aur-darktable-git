# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika  <hanatos at gmail dot com>
# Contributor: Kevin Brubeck Unhammer <unhammer at member dot fsf dot org>

pkgname=darktable-git
pkgrel=1
pkgver=20100831
pkgdesc="Utility to organize and develop raw images"
arch=(i686 x86_64)
url=http://darktable.sf.net/
license=(GPL3)
depends=(gconf libglade exiv2 openexr libgphoto2 libgnome-keyring lensfun lcms)
makedepends=(git intltool)
provides=(darktable)
conflicts=(darktable)
install=darktable.install
source=()

_gitroot=git://darktable.git.sf.net/gitroot/darktable/darktable
_gitname=darktable

build() {
  _gitdir=$srcdir/$_gitname

  if [ -d $_gitdir/.git ]; then
    cd $_gitdir
    git pull origin
  else
    git clone $_gitroot $_gitdir
    cd $_gitdir
  fi

  git clean -dfx
  ./autogen.sh
  ./configure --prefix=/usr --disable-schemas-install --with-gconf-schema-file-dir=/usr/share/gconf/schemas
  make
}

package() {
  cd $srcdir/$_gitname
  make DESTDIR=$pkgdir install
  mv $pkgdir/usr/share/doc/darktable $pkgdir/usr/share/doc/$pkgname-$pkgver
}

md5sums=()
