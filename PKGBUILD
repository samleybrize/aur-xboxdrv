# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Jack Mitchell <jack@embed.me.uk>
# Contributor: Kevin MacMartin <prurigro at gmail dot com>

pkgname=xboxdrv
pkgver=0.8.8
pkgrel=2
pkgdesc='Userspace gamepad driver for Linux'
url='http://pingus.seul.org/~grumbel/xboxdrv'
arch=('i686' 'x86_64' 'armv7h')
license=('GPL3')
depends=('libx11' 'dbus-glib' 'libusb' 'python2-dbus')
makedepends=('scons' 'boost' 'pkg-config' 'libx11')
backup=("etc/default/${pkgname}")
source=(${pkgname}-${pkgver}.tar.gz::https://github.com/xboxdrv/${pkgname}/archive/v${pkgver}.tar.gz
        ${pkgname}.service
        ${pkgname}.default)
sha512sums=('3f27856da211a14e27a84fa5919da7965262adc36da16c75eed9bae891098183b5751a3e707573b4ab64e69096ea74d455e8f64827c88b38b65af94cc13b34ad'
            'c148ae286e3611bf61c0b34e9b2b48d76b4283ec81a4edcd0e330ec89dcee77f275e3052b8e204645aaf511452af9940ad3e0b9b43866daf18dfa202cade1934'
            '4f6e9a12b208254e19daba477dd7787147a8b2c8a83007d92f8cfce6212c21ce3306f23a2669080f0e46986ca102ab08c262b42c678caf1a891326b4e2c40b5f')

prepare() {
  cd ${pkgname}-${pkgver}
  sed 's|python|python2|g' -i examples/*.py
}

build() {
  cd ${pkgname}-${pkgver}
  scons \
    "${MAKEFLAGS}"
}

package() {
  cd ${pkgname}-${pkgver}
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm 644 "${srcdir}/${pkgname}.service" "${pkgdir}/usr/lib/systemd/system/${pkgname}.service"
  install -Dm 644 "${srcdir}/${pkgname}.default" "${pkgdir}/etc/default/${pkgname}"
  install -Dm 644 README.md NEWS PROTOCOL -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 examples/* -t "${pkgdir}/usr/share/doc/${pkgname}/examples"
  install -Dm 644 data/org.seul.Xboxdrv.conf -t "${pkgdir}/etc/dbus-1/system.d"
}

# vim: ts=2 sw=2 et:
