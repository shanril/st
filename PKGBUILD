# Contributor: Patrick Jackson <PatrickSJackson gmail com>
# Maintainer: Christoph Vigano <mail@cvigano.de>

pkgname=st
pkgver=0.8.2
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
url="http://st.suckless.org"
source=(http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz config.h)
sha256sums=('SKIP' 'SKIP')

prepare() {
  cp $srcdir/config.h $srcdir/$pkgname-$pkgver/config.h
  cd $srcdir/$pkgname-$pkgver
  #patch -p1 < ../st-no_bold_colors-0.8.1.diff
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
  # remove to avoid conflict with ncurses
  rm "${pkgdir}/usr/share/terminfo/s/st" "${pkgdir}/usr/share/terminfo/s/st-256color"
}
