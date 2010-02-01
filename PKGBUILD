# Maintainer:  Christian Himpel <chressie at gmail dot com>
# Contributor: Johannes Hanika  <hanatos at gmail dot com>

pkgname=darktable-git
pkgrel=1
pkgver=20100201
pkgdesc="Utility to organize and develop raw images"
arch=(i686 x86_64)
url=http://darktable.sf.net/
license=(GPL3)
depends=('exiv2>=0.18' 'gconf>=2.26' 'intltool>=0.40' lcms 'lensfun>=0.2.3' libglade)
makedepends=(git 'intltool>=0.40')
provides=(darktable)
conflicts=(darktable)
install=darktable.install
source=()

_gitroot=git://darktable.git.sf.net/gitroot/darktable/darktable
_gitname=darktable

build() {
  # Linking fails with --as-needed linker option
  unset LDFLAGS

  _gitdir=$srcdir/$_gitname

  if [ -d $_gitdir/.git ]; then
    cd $_gitdir
    git pull origin
  else
    git clone $_gitroot $_gitdir
    cd $_gitdir
  fi

  git clean -dfx
  ./autogen.sh || return 1
  ./configure --prefix=/usr --disable-schemas-install --with-gconf-schema-file-dir=/usr/share/gconf/schemas || return 1
  make || return 1
  make DESTDIR=$pkgdir install || return 1
  install -m755 -d $pkgdir/usr/share/doc/$pkgname-$pkgver
  install -m644 AUTHORS LICENSE NEWS README TODO TRANSLATORS $pkgdir/usr/share/doc/$pkgname-$pkgver || return 1
}

md5sums=()
