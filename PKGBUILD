pkgname=idlehack
pkgver=0.r4
pkgrel=4
pkgdesc="Monitor dbus and inhibit swayidle when Firefox or Chromium request it "
arch=('i686' 'x86_64' 'aarch64')
url="https://github.com/loops/idlehack"
license=('custom:ICS')
provides=('idlehack' 'idlehack-git')
conflicts=('idlehack-git')
_commit="fd73c76c2d289f9eb9ad9b0695fa9e9f151be22f"
source=("$pkgname::git+https://github.com/loops/idlehack.git#commit=$_commit")
sha256sums=('SKIP')
depends=('libx11')

pkgver() {
  cd "$pkgname" || return 1
  rev="$(git rev-list --count HEAD)"
  echo -n "0.r${rev}"
}

build() {
  cd "$srcdir/$pkgname" || return 1

  make || return 1

  sed -i 's/libexec/bin/' idlehack.service
}

package() {
  cd "$srcdir/$pkgname" || return 1

  mkdir -p "$pkgdir/usr/bin"
  cp idlehack "$pkgdir/usr/bin/"
  cp swayidle-inhibit "$pkgdir/usr/bin/"

  mkdir -p "$pkgdir/usr/lib/systemd/user"
  cp idlehack.service "$pkgdir/usr/lib/systemd/user/"
}
