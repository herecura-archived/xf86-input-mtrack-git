# Maintainer: Zach <mikezackles@gmail.com>
# Contributor: James An <james@jamesan.ca>

_gitname=xf86-input-mtrack
pkgname="$_gitname-git"
pkgver=20150727.c1301b0
pkgrel=2
pkgdesc="A multitouch X driver using the kernel MT protocol"
arch=('x86_64')
url="http://github.com/BlueDragonX/$_pkgname"
license=('GPL')
depends=('mtdev' 'libxss')
makedepends=('git' 'xorg-server-devel' 'resourceproto' 'glproto')
provides=("$_gitname")
conflicts=("$_gitname")
backup=('usr/share/X11/xorg.conf.d/10-mtrack.conf')
options=()
install=
source=(
	"$_gitname"::"git+https://github.com/BlueDragonX/$_gitname.git"
	10-mtrack.conf
)
sha256sums=(
	'SKIP'
	'5e0bc6ee814165be31e0265842f066c290b544757451d15c7e6eb370d4c0e356'
)

pkgver() {
	cd "$_gitname"
	git log -1 --date=short --format="%cd.%h" | tr -d '-'
}

build() {
	cd "$_gitname"

	autoreconf --install
	./configure --prefix=/usr
	make
}

package() {
	cd "$_gitname"

	make DESTDIR="$pkgdir" install
	install -Dm644 "$srcdir/10-mtrack.conf" "$pkgdir/usr/share/X11/xorg.conf.d/10-mtrack.conf"
}
