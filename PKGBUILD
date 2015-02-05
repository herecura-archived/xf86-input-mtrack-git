# Maintainer: Zach <mikezackles@gmail.com>
# Contributor: James An <james@jamesan.ca>

_pkgname=xf86-input-mtrack
pkgname="$_pkgname-git"
pkgver=0.3.0.r2.g5f53106
pkgrel=1
pkgdesc="A multitouch X driver using the kernel MT protocol"
arch=('i686' 'x86_64')
url="http://github.com/BlueDragonX/$_pkgname"
license=('GPL')
depends=('mtdev' 'libxss')
makedepends=('git' 'xorg-server-devel' 'resourceproto' 'glproto')
provides=("$_pkgname")
conflicts=("$_pkgname")
backup=('usr/share/X11/xorg.conf.d/10-mtrack.conf')z
options=()
install=
source=(
  "$_pkgname"::"git+https://github.com/BlueDragonX/$_pkgname.git"
  10-mtrack.conf
)
md5sums=(
  'SKIP'
  ffb540330d92957e0da28af5a005136e
)

pkgver() {
  cd "$_pkgname"
  ( set -o pipefail
    git describe --long --tags | sed -r 's/([^-]*-g)/r\1/;s/-/./g;s/^[^0-9]*//' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
  cd "$_pkgname"

  autoreconf --install
  ./configure --prefix=/usr
  make
}

package() {
  cd "$_pkgname"

  make DESTDIR="$pkgdir" install
  install -Dm644 "$srcdir/10-mtrack.conf" "$pkgdir/usr/share/X11/xorg.conf.d/10-mtrack.conf"
}
