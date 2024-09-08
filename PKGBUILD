# Maintainer: Laura Demkowicz-Duffy <dev at demkowiczduffy.co.uk>
# Contributor: Kyle Keen <keenerd@gmail.com>
# Contributor: Daniel J Griffiths <ghost1227@archlinux.us>

pkgname=macchanger-dynamicoui
_pkgname=macchanger
pkgver=1.7.0
pkgrel=1
pkgdesc="A small utility to change your NIC's MAC address"
arch=('x86_64')
#url="https://ftp.gnu.org/gnu/macchanger"
url="https://www.gnu.org/software/macchanger"
license=('GPL')
depends=('glibc')
provides=('macchanger')
conflicts=('macchanger')
source=("$_pkgname-$pkgver.tgz::https://github.com/alobbs/macchanger/archive/$pkgver.tar.gz"
        "https://www.wireshark.org/download/automated/data/manuf.gz")
sha256sums=('1d75c07a626321e07b48a5fe2dbefbdb98c3038bb8230923ba8d32bda5726e4f'
            'SKIP')

prepare() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  # FS#59021
  sed -i 's|/dev/hwrng|/dev/random|' src/main.c

  # overwrite the OUI data from upstream
  grep -v '^#' ../manuf | \
  	sed 's/^\([^\t]\+\)\t\([^\t]\+\)\t\(.\+\)$/\1 \3/' | \
  	sed 's/ \+/ /g' | \
  	sed 's/ \t/ /g' | \
  	sed 's/:/ /g' > data/OUI.list
  echo "" > data/wireless.list
}

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  ./autogen.sh
  ./configure --prefix=/usr \
              --mandir=/usr/share/man \
              --infodir=/usr/share/info
  make
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"

  make DESTDIR="${pkgdir}" install
}
