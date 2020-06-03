# $Id: PKGBUILD 266875 2017-11-15 14:29:11Z foutrelis $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer: Vesa Kaihlavirta <vegai@iki.fi>

pkgname=pwsafe
pkgver=20181220
_commit=1dbcfd01a502d1579a80c208662add64b4090818
pkgrel=1
pkgdesc="A commandline program for managing encrypted password databases"
arch=('x86_64')
url="https://github.com/nsd20463/pwsafe"
license=('GPL')
depends=('openssl' 'libxmu')
makedepends=('git')
source=("git://github.com/nsd20463/pwsafe.git#commit=${_commit}"
	pwsafe-XChangeProperty.patch
	update-config.guess.patch)
md5sums=('SKIP'
         'cff6aee2e43f5fbe82e8cd7ccfefb099'
         '8ded5e6bcaed9c2e8e84833e423a8706')
prepare() {
  cd "$srcdir"/${pkgname}
  # Patch from fedora, fixes FS#28339
  patch -Np0 -i ../pwsafe-XChangeProperty.patch
  # Patch to config.guess for building on aarch64
  patch -Np1 -i ../update-config.guess.patch
}

build() {
  cd "$srcdir"/${pkgname}
  aclocal
  autoheader
  automake --add-missing
  autoconf
  ./configure --prefix=/usr --mandir=/usr/share/man
  make
}

package() {
  cd "$srcdir"/${pkgname}
  make DESTDIR="$pkgdir" install
  # Make pwsafe suid root so it can seed rng as a user
  chmod +s "$pkgdir"/usr/bin/pwsafe
}
