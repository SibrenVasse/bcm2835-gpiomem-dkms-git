# Maintainer: Sibren Vasse <arch@sibrenvasse.nl>

_pkgbase=bcm2835-gpiomem
pkgname=bcm2835-gpiomem-dkms-git
pkgver=r1.52825a3
pkgrel=1
pkgdesc="BCM2835 gpiomem dkms kernel module (DKMS)"
arch=('aarch64')
url="https://github.com/SibrenVasse/bcm2835-gpiomem"
license=('GPL2')
depends=('dkms')
conflicts=("${_pkgbase}-git")
provides=("bcm2835-gpiomem-dkms")
source=("${pkgname%-git}::git+https://github.com/SibrenVasse/bcm2835-gpiomem.git"
        'dkms.conf')
sha256sums=('SKIP'
            'e62c30829136341bb043e5087a8059a00d30f60db8d4d52d2a79070c41c5862b')

pkgver() {
  cd "${srcdir}/${pkgname%-git}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
  install -Dm644 dkms.conf "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/dkms.conf"

  cd "${pkgname%-git}"
  # Install
  install -Dm644 Makefile "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/Makefile"
  install -Dm644 bcm2835-gpiomem.c "${pkgdir}/usr/src/${_pkgbase}-${pkgver}/bcm2835-gpiomem.c"

  # Set name and version
  sed -e "s/@_PKGBASE@/${_pkgbase}/" \
      -e "s/@PKGVER@/${pkgver}/" \
      -i "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf
}
