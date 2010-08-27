# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika  <hanatos at gmail dot com>

pkgname=darktable-git
pkgrel=1
pkgver=20100826
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
  make DESTDIR=$pkgdir install
  install -m755 -d $pkgdir/usr/share/doc/$pkgname-$pkgver
  install -m644 AUTHORS LICENSE NEWS README TODO TRANSLATORS $pkgdir/usr/share/doc/$pkgname-$pkgver
}

md5sums=()
