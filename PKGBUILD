# Current maintainer: Peter Enerccio <enerccio@gmail.com>

#  Changelog
# 01-30-2013: added gc dependency, removed strip option 
 
pkgname=ecl-unicode-git
pkgver=latest
pkgrel=1
pkgdesc="Embeddable Common Lisp"
arch=('i686' 'x86_64' 'armv6h')
url="http://sourceforge.net/projects/ecls/"
license=('LGPL')
depends=('bash' 'gmp' 'gc')
makedepends=('texinfo' 'git')
provides=('common-lisp' 'cl-asdf' 'ecl')
conflicts=('ecl' 'ecl-unicode')
options=('!makeflags' '!strip')
_gitrepo=ecls-ecl
_gitcmd=git://git.code.sf.net/p/ecls/ecl
source=()
md5sums=()

build() {
	 cd $srcdir
	 git clone ${_gitcmd} ${_gitrepo}
	 cd $srcdir/${_gitrepo}
	 sed -i 's|-Wl,--rpath,~A|-Wl,--rpath,/usr/lib/ecl|' src/configure || return 1
	 ./configure --build=$CHOST \
	 --prefix=/usr \
	 --with-tcp \
	 --with-clos-streams \
	 --with-serve-event \
	 --enable-shared \
	 --enable-unicode \
	 --enable-boehm=system \
	 --enable-threads \
	 --with-system-gmp \
	 --without-x \
	 --without-clx

	 make || return 1
}

package() {
	cd $srcdir/${_gitrepo}
	make DESTDIR=$pkgdir install || return 1
}

