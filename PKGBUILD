# Maintainer: Maik Broemme <mbroemme@libmpq.org>
pkgname="media_build_experimental-dkms-hg"
pkgdesc="Oliver Endriss experimental media tree as DKMS - latest mercurial (hg)"
pkgver=r500.ada40c8874d5
pkgrel=1
arch=("i686" "x86_64")
url="http://linuxtv.org/hg/~endriss/media_build_experimental"
license=("GPL")
depends=("dkms" "linux-headers")
makedepends=("mercurial")
source=(
  "media_build_experimental::hg+http://linuxtv.org/hg/~endriss/media_build_experimental"
  "${pkgname}.conf"
)
sha256sums=(
  "SKIP"
  "aade2d6f2f0ecc95b6db7bd8c41061c6ff4dc85010aa91097edfcf9a7c4af4eb"
)
install="${pkgname}.install"

pkgver() {
  cd "${srcdir}/media_build_experimental"
  printf "r%s.%s" "$(hg identify -n)" "$(hg identify -i)"
}

build() {
  cd "${srcdir}/media_build_experimental"
  make download
  make untar
  sed "/scripts\/rmmod.pl/d" -i "${srcdir}/media_build_experimental/experimental/v4l-dvb-saa716x/v4l/Makefile"
  sed "/scripts\/rmmod.pl/d" -i "${srcdir}/media_build_experimental/v4l/Makefile"
}

package() {
  cd "${srcdir}/media_build_experimental"
  install -D -m 0644 "${srcdir}/${pkgname}.conf" "${pkgdir}/usr/src/media_build_experimental-${pkgver}/dkms.conf"
  cp -a "${srcdir}/media_build_experimental"/* "${pkgdir}/usr/src/media_build_experimental-${pkgver}"
  sed "s|@VERSION@|${pkgver}|g" -i "${pkgdir}/usr/src/media_build_experimental-${pkgver}/dkms.conf"
}
