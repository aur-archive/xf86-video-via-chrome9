# Maintainer: Daichi Shinozaki <dsdseg@gmail.com>
# Contributor: Paul Burton <paulburton89@gmail.com>
pkgname=xf86-video-via-chrome9
pkgver=92.008.d9c5be.20140915
pkgrel=3
pkgdesc="VIA chrome9 Xorg driver"
arch=('i686' 'x86_64')
url="http://linux.via.com.tw"
license=('MIT')
depends=('xorg-server-devel' 'xproto' 'libdrm>=2.0' 'mesa-libgl' 'libxvmc' 'udev' 'via-chrome9-dkms')
makedepends=('autoconf' 'libtool')
source=('5.76.52.92-sourcecode-008-d9c5be-20140915.7z::http://linux.via.com.tw/support/beginDownload.action?eleid=741&fid=1041'
xf86drmvia.c.patch autogen.sh.patch)
md5sums=('f02433a9573ee07db0acc5723f75d8a3'
         'cb77b59fca35386bd053183eb25c0d8b'
         '42b6a597cdaa95bc2929e6376ed68140')
backup=('etc/X11/xorg.conf.via-chrome9')
_dir=5.76.52.92-sourcecode-008-d9c5be-20140915/XServer

prepare() {
  cd "$srcdir"/$_dir/src
  patch -p0 -i $srcdir/xf86drmvia.c.patch
  cd ..
  patch -p0 -i $srcdir/autogen.sh.patch
}

build() {
  cd "$srcdir"/$_dir
	sh autogen.sh
	# compile driver
  make
}

package() {
	cd "$srcdir"/$_dir

	# install driver
	install -dm755 "$pkgdir"/usr/lib/xorg/modules/drivers
	install -m755 src/.libs/via_drv.so "$pkgdir"/usr/lib/xorg/modules/drivers/

	# install sample xorg.conf
	install -dm755 "$pkgdir"/etc/X11
	install -m644 Misc/generic/xorg.conf "$pkgdir"/etc/X11/xorg.conf.via-chrome9
	install -Dm644 ./man/via.4 "$pkgdir"/usr/share/man/man4/via.4

	# install license
	#install -Dm644 ./LICENSE "$pkgdir"/usr/share/licenses/xf86-video-via-chrome9/LICENSE
}
