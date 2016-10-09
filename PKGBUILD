# xkeyboard-config-f13
# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot <jgc@archlinux.org>
# Option to map caps lock to f13 added by katie-jones, see https://github.com/katie-jones/xkeyboard-config-f13

pkgname=xkeyboard-config-f13
_pkgname=xkeyboard-config
pkgver=2.14
pkgrel=2
pkgdesc="X keyboard configuration files"
arch=(any)
license=('custom')
url="http://www.freedesktop.org/wiki/Software/XKeyboardConfig"
makedepends=('intltool' 'xorg-xkbcomp')
provides=('xkbdata', 'xkeyboard-config')
replaces=('xkbdata')
conflicts=('xkbdata', 'xkeyboard-config')
source=(http://xorg.freedesktop.org/archive/individual/data/${_pkgname}/${_pkgname}-${pkgver}.tar.bz2
        001-xkeyboard-config-f13-base.patch
        002-xkeyboard-config-f13-evdev.patch
        003-xkeyboard-config-f13-capslock.patch)

sha256sums=('dc91458a214c56a35727f9e523fc647615de64137057ca6ee4d4d4474a4bb2ae'
            '2eeecf7c5529d2d04ebae8803bfea6a9475437c66f058b41a4ed51a702d75265'
            '40cabc4f9794541868d5e7b6c58b8ff2bd099de1c7c98c03b49d68fbb049a085'
            '36220cfba33b0d13f0fa5860af7b42cdc495577196f7597bbc7ad059f4297fff')

install=

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"

  patch -p1 -i "${srcdir}/001-xkeyboard-config-f13-base.patch"

  patch -p1 -i "${srcdir}/002-xkeyboard-config-f13-evdev.patch"

  patch -p1 -i "${srcdir}/003-xkeyboard-config-f13-capslock.patch"

  ./configure --prefix=/usr \
      --with-xkb-base=/usr/share/X11/xkb \
      --with-xkb-rules-symlink=xorg \
      --enable-compat-rules=yes
  make
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"

  make DESTDIR="${pkgdir}" install
  rm -f "${pkgdir}/usr/share/X11/xkb/compiled"

  install -m755 -d "${pkgdir}/var/lib/xkb"
  install -m755 -d "${pkgdir}/usr/share/licenses/${_pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${_pkgname}/"
}
