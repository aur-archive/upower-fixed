# $Id$
# Maintainer: Jan de Groot <jgc@archlinux.org>
# Fixed PKGBUILD by: ultraviolet <ultravioletnanokitty@gmail.com>

pkgname=upower-fixed
_pkgname=upower
_commit=3a5f3e5
pkgver=0.99.2
pkgrel=2
pkgdesc="newest version of upower patched to solve a horrible memory leak"
arch=('i686' 'x86_64')
url="https://bugs.archlinux.org/task/40444"
license=('GPL')
conflicts=('upower' 'upower-git')
provides=('upower')
depends=('systemd-tools' 'systemd' 'libusb' 'dbus-glib' 'libimobiledevice')
makedepends=('git' 'intltool' 'gtk-doc' 'docbook-xsl' 'gobject-introspection' 'systemd')
backup=('etc/UPower/UPower.conf')
source=("git://anongit.freedesktop.org/upower#commit=$_commit"
        '0001-In-up_daemon_stop_poll-disconnect-the-g_signal_handl.patch'
        '0001-Added-prototypes-in-up-device.h-and-fixed-warning.patch')
sha256sums=('SKIP'
            'e02dad4e9c19149bfabc75d4e5bd17ee9e1c9a04c3091716901ad2b227c6e125'
            '0dcb96e5c38e31d0eb6ea20a80e4610018cfdb8168060addc12b01117a7f1359')

prepare() {
  cd $_pkgname
  git am $srcdir/0001-In-up_daemon_stop_poll-disconnect-the-g_signal_handl.patch
  git am $srcdir/0001-Added-prototypes-in-up-device.h-and-fixed-warning.patch
}

build() {
  cd $_pkgname

  ./autogen.sh --prefix=/usr --sysconfdir=/etc \
    --localstatedir=/var \
    --libexecdir=/usr/lib/$_pkgname \
    --disable-static
  make
}

package() {
  cd $_pkgname
  make DESTDIR="$pkgdir" install
}
