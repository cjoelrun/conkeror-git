# Maintainer: Ivy Foster <joyfulgirl@archlinux.us>
# Maintainer: Stefan Husmann <stefan-husmann@t-online.de>
# Contributor: Heeru Kiyura <M8R-p9i5nh@mailinator.com>

pkgname=conkeror-git
pkgver=120527.1.88.ga737e50
pkgrel=1
pkgdesc="A highly programmable web browser based on Mozilla XULRunner."
arch=('i686' 'x86_64')
url="http://conkeror.mozdev.org/"
license=('MPL' 'GPL' 'LGPL')
depends=('xulrunner' 'desktop-file-utils')
makedepends=('git' 'imagemagick')
provides=(conkeror)
changelog=ChangeLog
install=conkeror-git.install

source=('git://repo.or.cz/conkeror.git' 
        'conkeror_gimpfile.xpm' 'conkeror.sh')
md5sums=('SKIP' 'SKIP' 'SKIP')
_gitname="conkeror"

pkgver() {
  cd $_gitname
  # Git tag
  echo $(git describe --always|sed -e 's/debian.*+git//' -e 's/-/./g')
}

build() {
  cd "$srcdir"/${_gitname}
  make
}

package() { 
  install -d "$pkgdir"/usr/share/{conkeror,man/man1,pixmaps}
  cp -a "$srcdir"/${_gitname}/* "$pkgdir"/usr/share/conkeror

  install -Dm644 "$pkgdir"/usr/share/conkeror/contrib/man/conkeror.1 \
    "$pkgdir"/usr/share/man/man1/conkeror.1
  install -Dm644 "$srcdir"/${_gitname}/debian/conkeror.desktop \
    "$pkgdir"/usr/share/applications/conkeror.desktop
  install -Dm644 "$srcdir"/conkeror_gimpfile.xpm \
    "$pkgdir"/usr/share/pixmaps

  install -Dm755 "$srcdir"/conkeror.sh "$pkgdir"/usr/bin/conkeror
  mv "$pkgdir"/usr/share/conkeror/conkeror-spawn-helper \
    "$pkgdir"/usr/bin

  rm "$pkgdir"/usr/share/conkeror/conkeror-spawn-helper.c
  rm -r "$pkgdir"/usr/share/conkeror/contrib/man
  rm -r "$pkgdir"/usr/share/conkeror/debian
} 
