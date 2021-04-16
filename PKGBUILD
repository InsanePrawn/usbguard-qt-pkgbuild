# Maintainer: InsanePrawn <insane.prawny@gmail.com>

pkgname=usbguard-qt-git
provides=('usbguard-qt')
pkgver=0.7.4.13.gae105c6
pkgrel=0
pkgdesc='QT Applet for controlling USBGuard'
url='https://github.com/pinotree/usbguard-apllet-qt'
arch=('x86_64')
license=('GPL2')
depends=('usbguard' 'libusbguard.so' 'qt5-base' 'qt5-svg' 'qt5-tools' 'hicolor-icon-theme' 'dbus-glib')
makedepends=('git' 'glibc')
source=(git+https://github.com/pinotree/usbguard-applet-qt.git)
sha512sums=('SKIP')
_pkgdir="usbguard-applet-qt"
build() {
  cd "${_pkgdir}"
  cmake . -DCMAKE_INSTALL_PREFIX=/usr
  make
}

pkgver() {
  cd "${_pkgdir}"
  git describe --always --dirty 2>/dev/null | sed -e 's/-/./g' -e 's/^usbguard.//'
}

package() {
  cd "${_pkgdir}"
  make INSTALL='install -p' SYSTEMD_UNIT_DIR="/usr/lib/systemd/system" DESTDIR="${pkgdir}" install

  # cleanup
  cd "${pkgdir}"
  rm -rf {etc,var,usr/{include,lib,share/{dbus-1,polkit-1,man/{man1/usbguard.1,man5,man8}}}} \
    usr/bin/usbguard{,-daemon,-dbus,-rule-parser}
}

# vim: ts=2 sw=2 et:
