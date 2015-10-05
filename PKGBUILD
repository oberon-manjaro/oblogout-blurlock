# Maintainer: Bernhard Landauer <oberon@manjaro.org>
# Contributor: Kirill Malyshev <keryascorpio at gmail.com>
# Contributor: Robert Orzanna <orschiro@googlemail.com>

pkgname=oblogout-manjaro
_gitname="oblogout-fork"
pkgver=20151005
pkgrel=1
pkgdesc="Systemd/OpenRC-compatible logout script for Openbox, Fluxbox and others. Including blurlock"
arch=('any')
url="https://forum.manjaro.org/index.php?topic=25894.0"
_gitroot="git://github.com/Cloudef/oblogout-fork.git"
license=('GPL2')
depends=('i3lock'
	'imagemagick'
	'pygtk'
	'python2-pillow'
	'python2-distutils-extra'
	'python2-dbus')
optdepends=('lightdm: for switch-user function')
makedepends=('git')
install=$pkgname.install 
conflicts=('fluxlogout'
	'oblogout'
	'openboxlogout-gnome')
replaces=('fluxlogout')
backup=('etc/oblogout.conf')
source=(fluxboxexit
	ob_blurlock
	oblogout.conf
	oblogout_blur
	http://www.oberon.at/oberon/src/OutMok.tar.xz
	switch-user.patch)
md5sums=('f10cb96555b02245d944b381abb14221'
         'eef31ce5c7a9f002ef407394cf6fd20b'
         'd2169918c0412cbc57f5024aa497fa2f'
         '0e9d42c6c83022515d3b14275f630f87'
         'a30813dafbe1b9d650db2f237ac1d89d'
         '4bb8046c6d6a9709796afd814feec8f1')

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname --dept=1
  fi

  cd "$srcdir/$_gitname"

  patch -p1 < "$srcdir/switch-user.patch"
}
pkgver() {
	date +'%Y%m%d'
}
package() {
  cd "$srcdir/$_gitname"
  python2 setup.py install --root="$pkgdir/"

  cd "$srcdir"
  install -m755 "$srcdir/fluxboxexit" "$pkgdir/usr/bin/"
  install -m755 "$srcdir/ob_blurlock" "$pkgdir/usr/bin/"
  install -m755 "$srcdir/oblogout_blur" "$pkgdir/usr/bin/"
  install -Dm644 "$srcdir/oblogout.conf" "$pkgdir/etc/oblogout-manjaro.conf"
  mkdir -p "$pkgdir/usr/share/themes/OutMok" \
	"$pkgdir/usr/share/themes/OutMok-small"
  cp -r "$srcdir/OutMok/oblogout" "$pkgdir/usr/share/themes/OutMok"
  cp -r "$srcdir/OutMok-small/oblogout" "$pkgdir/usr/share/themes/OutMok-small"
}
