# Maintainer: Christian Weber <christianweber802 at gmx dot net>

pkgname=ndiswrapper
pkgver=1.59
pkgrel=4
epoch=
pkgdesc="Module for NDIS (Windows Network Drivers) drivers supplied by vendors."
arch=('i686' 'x86_64')
url="http://sourceforge.net/projects/ndiswrapper/"
license=('GPL')
depends=('linux>=3.14' 'linux<3.15')
makedepends=('linux-headers>=3.14' 'linux-headers<3.15')
optdepends=('ndisgtk: GTK+ based frontend for ndiswrapper.')
provides=('ndiswrapper')
install=".install"
source=("http://download.sourceforge.net/ndiswrapper/$pkgname-$pkgver.tar.gz" "https://raw.githubusercontent.com/fauxsoup/ndiswrapper-patch/master/ndiswrapper-1.59.patch")
md5sums=('e26a7213468ccd6b0bb4c211c7aadeaa'
         '76298a85e1442eb65990cadbaaeaa321')

_EXTRAMODULES='extramodules-3.14-ARCH'
_KERNEL=$(cat /usr/lib/modules/${_EXTRAMODULES}/version)


prepare() {
	[ -z "$_KERNEL" ] && error "Could not get kernel version from '/usr/lib/modules/${_EXTRAMODULES}/version'..." && false
	msg "Found kernel version: $_KERNEL"
}

build() {
	cd "$srcdir/$pkgname-$pkgver"
	patch -p1 -i ../ndiswrapper-1.59.patch
	make -C driver KVERS_UNAME=${_KERNEL}
	make -C utils
}

package() {
	cd "$srcdir/$pkgname-$pkgver"
	make -C driver DESTDIR=${pkgdir} KVERS_UNAME=${_KERNEL} install
	make -C utils DESTDIR=${pkgdir} install
}
