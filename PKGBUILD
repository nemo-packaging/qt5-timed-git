## $Id$
# Maintainer: TheKit <nekit1000 at gmail.com>
# Maintainer: James Kittsmiller (AJSlye) <james@nulogicsystems.com>

_pkgname=timed
pkgname=timed-git
pkgver=3.6.5.r0.gfc298b0
pkgrel=1
pkgdesc="Mer time daemon"
arch=('x86_64' 'aarch64')
url="https://git.sailfishos.org/mer-core/timed"
license=('GPL')
depends=('dbus' 'libiodata')
makedepends=('git')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=('git+https://git.sailfishos.org/mer-core/timed.git'
        '0001-Fixes-build.patch')
md5sums=('SKIP'
         'ec4429789c7eb13d442cbd445d0c3853')

pkgver() {
	cd "$srcdir/$_pkgname"
	git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
	cd "$srcdir/$_pkgname"
    patch -Np1 -i "${srcdir}/0001-Fixes-build.patch"
    mkdir -p src/h/timed-qt5/
    cp src/lib/qmacro.h src/h/timed-qt5/qmacro.h
    sed -i "s|libsystemd-daemon|libsystemd|g" ./src/server/server.pro
}

build() {
	cd "$srcdir/$_pkgname"
    qmake
    cd "$srcdir/$_pkgname/src/server"
    
    cd "$srcdir/$_pkgname"
    make
}

package() {
	cd "$srcdir/${pkgname%-git}"
	make INSTALL_ROOT="$pkgdir/" install
}
