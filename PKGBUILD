# Maintainer: Yu-Sheng Lin <johnjohnlys@gmail.com>
_pkgbase=amd_energy
pkgname=amd_energy-morecpu-dkms-git
pkgver=1.0
pkgrel=1
pkgdesc="Add non-Epyc Zen CPUs to amd_energy"
arch=('x86_64' 'i686')
url="https://raw.githubusercontent.com/torvalds/linux/master/drivers/hwmon/amd_energy.c"
license=('GPL')
depends=('dkms')
makedepends=('linux-headers')
provides=('amd_energy')

source=("amd_energy.c::https://raw.githubusercontent.com/torvalds/linux/master/drivers/hwmon/amd_energy.c"
        "Makefile"
        "dkms.conf"
        "more_zen.h")

sha256sums=('SKIP'
            '1e05ccb8285dedd673100f7a36eaf86d02c0b2d9dc6bd4b17688b0eb29355aa4'
            'f325b751c8a81416a75c2c1e7a7bc9ca46ae0fa3b44d4ccc09593274be1b2dc7'
            '01ef8a2228b651771b206b74830f7b07ca2b71e3b2366ace32864f9bc9655812')

prepare() {
	sed "/static const struct x86_cpu_id cpu_ids\[\]/s/$/\n#include \"more_zen.h\"/" amd_energy.c -i
}

package() {
	cd ${srcdir}

	install -d "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/
	cp -r Makefile amd_energy.c more_zen.h "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/

	install -Dm644 dkms.conf "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf

	sed -e "s/@_PKGBASE@/${_pkgbase}/" \
	    -e "s/@PKGVER@/${pkgver}/" \
	    -i "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf
}

