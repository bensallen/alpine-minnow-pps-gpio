# Contributor:
# Maintainer:
pkgname=minnow-pps-gpio
pkgver=
pkgrel=0
arch="all"
depends=""
makedepends=""
install=""
subpackages="$pkgname-dev $pkgname-doc"
source=""
builddir="$srcdir/"

build() {
	cd "$builddir"
}

package() {
	cd "$builddir"
}

# Contributor: Ben Allen <bensallen@me.com>
# Maintainer: Ben Allen <bensallen@me.com>
_flavor=${FLAVOR:-grsec}
_kpkg=linux-$_flavor
_realname=minnow-pps-gpio
_name=$_realname-$_flavor

_kver=4.4.45
_kpkgrel=0

_gitver=eb4aec67c087b809460f629e6552bae3fe2ea4a0
_mypkgrel=0

# source the kernel version
if [ -f ../linux-$_flavor/APKBUILD ]; then
    . ../linux-$_flavor/APKBUILD
    [ "$_kver" != "$pkgver" ] && die "$_name: Please update _kver to $pkgver"
    [ "$_kpkgrel" != "$pkgrel" ] && die "$_name: Please update _kpkgrel to $pkgrel"
fi

_kernelver=$_kver-r$_kpkgrel
_abi_release=${_kver}-${_kpkgrel}-${_flavor}

pkgname=$_name
pkgver=$_kver
pkgrel=$(($_kpkgrel + $_mypkgrel))

pkgrel=0
pkgdesc="MinnowBoard Max - Board file (kernel module) to map GPIO to pps-gpio driver"
url="https://github.com/bensallen/Minnowboard"
arch="all"
license="GPL2"
depends="linux-${_flavor}=${_kernelver}"
makedepends="linux-${_flavor}-dev=${_kernelver} linux-headers"
install=
install_if="linux-$_flavor=$_kernelver $_realname"
subpackages=
source="$_realname-$_gitver.tar.gz::https://github.com/bensallen/Minnowboard/archive/$_gitver.tar.gz"
_builddir="$srcdir"/Minnowboard-$_gitver/minnow-pps-gpio

build() {
    make -C /lib/modules/$_abi_release/build M=$_builddir CFLAGS_minnow-pps-gpio.o="-DPPS_GPIO=340 -DCONFIG_PPS_CLIENT_GPIO=m -DCONFIG_PPS_CLIENT_GPIO_MODULE=y" modules || return 1
}

package() {
    make -C /lib/modules/$_abi_release/build M=$_builddir INSTALL_MOD_PATH=$pkgdir modules_install || return 1
}
md5sums="f73f1c8bbe3d62bb5a240f8dfb7efe9a  minnow-pps-gpio-eb4aec67c087b809460f629e6552bae3fe2ea4a0.tar.gz"
sha256sums="29f089291e275bbf1fab735b62cb4a02b83b68657def512cc24dd22ec7ebd30e  minnow-pps-gpio-eb4aec67c087b809460f629e6552bae3fe2ea4a0.tar.gz"
sha512sums="cda3ac3d5dc17b8000e35f17055998242b554deee7d24b8189d7bf7eae5b53ee55cdefbfe34e9e526f07368a338af7ae6b4bc67c2ea69209a0d82d0e45f2fe36  minnow-pps-gpio-eb4aec67c087b809460f629e6552bae3fe2ea4a0.tar.gz"
