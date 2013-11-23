# Maintainer: Kyle Keen <keenerd@gmail.com>
# Contributor: Daniel J Griffiths <ghost1227@archlinux.us>

pkgname=macchanger
pkgver=1.6.0
pkgrel=2
pkgdesc="A small utility to change your NIC's MAC address"
arch=('i686' 'x86_64')
url="http://ftp.gnu.org/gnu/macchanger"
license=('GPL')
depends=('glibc')
install='macchanger.install'
source=(http://ftp.gnu.org/gnu/macchanger/${pkgname}-${pkgver}.tar.gz)
md5sums=('1257b18e9067a8192c9747da52aabdda')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr \
              --mandir=/usr/share/man \
              --infodir=/usr/share/info
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"

  make DESTDIR="${pkgdir}" install
}
