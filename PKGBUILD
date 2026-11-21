pkgname=dwm
pkgver=6.0
pkgrel=2
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=('zipman' '!debug')
depends=('libx11' 'libxinerama')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        dwm.desktop
    )
_patches=(01.Setup.makefiles.patch
          02.Base.config.changes.patch
          03.New.master.patch
          04.Xft.patch
          05.Statuscolours.config.def.h.patch
          06.Statuscolours.dwm.c.patch
          08.ScreenGrab-Editor.config.def.h.patch
          )
source=(${source[@]} ${_patches[@]})

prepare() {
   cd "$srcdir/$pkgname-$pkgver" 

 for p in "${_patches[@]}"; do
    echo "=> $p"
    patch < ../$p || return 1
  done
}

build() {
   cd "$srcdir/$pkgname-$pkgver"

  sed -i 's/^CFLAGS = -g/#CFLAGS += -g/g' config.mk
  sed -i 's/^#CFLAGS = -std/CFLAGS += -std/g' config.mk
  sed -i 's/^LDFLAGS = -g/#LDFLAGS += -g/g' config.mk
  sed -i 's/^#LDFLAGS = -s/LDFLAGS += -s/g' config.mk
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
md5sums=('8bb00d4142259beb11e13473b81c0857'
         '939f403a71b6e85261d09fc3412269ee'
         '009a8b8f7c3b28414f9cd966678ce65c'
         '3e4d9e51417bc2bb66cbeb53a58b094c'
         '7a6b8586127c7169ab2485cb89aeda42'
         'eb03fb0e8368e9f69a9d28271d73acc5'
         '1f88510e788b9d2e90e29246c1d7804d'
         '55bb2b7d43df438f2b5cffaf703f3d14')
