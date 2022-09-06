# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Maintainer: Jan de Groot <jgc@archlinux.org>
# Patches added by Katie Jones.

pkgname=xkeyboard-config-f13
_pkgname=xkeyboard-config
pkgver=2.36
pkgrel=3
pkgdesc="X keyboard configuration files"
arch=(any)
license=('custom')
url="https://www.freedesktop.org/wiki/Software/XKeyboardConfig"
makedepends=('intltool' 'xorg-xkbcomp' 'libxslt')
provides=('xkbdata' 'xkeyboard-config')
replaces=('xkbdata' 'xkeyboard-config')
conflicts=('xkbdata' 'xkeyboard-config')
source=(https://xorg.freedesktop.org/archive/individual/data/${_pkgname}/${_pkgname}-${pkgver}.tar.xz{,.sig}
alujiskeys.patch::https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config/-/commit/dc1534b4b0cf2153e4b8848310efc8393fb73830.patch
backslahes-instead-of-slashes.patch::https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config/-/commit/8ac41c50ab0aa7cd3a7e94313074115de2a172d2.patch
    'kj.patch')
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145')
validpgpkeys+=('15CFA5C595041D2CCBEA155F1732AA424A0E86B4') # "Sergey Udaltsov (For GNOME-related tasks) <svu@gnome.org>"
sha512sums=('a81054ff6b7928a445a913b80fad995056559feff7bc1f4926657f171a102108b6e22958dc6c814ae2a25445f65c94485f13399628016f1358cf3840e235e3de'
            'SKIP'
            'SKIP'
            'SKIP'
            'e9057028e4e8fd67a07e62c44e0748554b0f01b79209b3df8a447fe612315bba5a3ac223e338f74bd3197899602c4a401cac063aa3f787170145c1a17cd03e47')

prepare() {
  cd ${_pkgname}-${pkgver}
  # FS##75007 / https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config/-/issues/325
  patch -Np1 -i ../alujiskeys.patch
  patch -Np1 -i ../backslahes-instead-of-slashes.patch
  patch -Np1 -i "${srcdir}/kj.patch"

}

build() {
  arch-meson ${_pkgname}-${pkgver} build \
	-D xkb-base="/usr/share/X11/xkb" \
	-D compat-rules=true \
	-D xorg-rules-symlinks=true

  # Print config
  meson configure build

  ninja -C build

 }
 
 package() { 

  DESTDIR="$pkgdir" ninja -C build install

  install -m755 -d "${pkgdir}/var/lib/xkb"
  install -m755 -d "${pkgdir}/usr/share/licenses/${_pkgname}"
  install -m644 ${_pkgname}-${pkgver}/COPYING "${pkgdir}/usr/share/licenses/${_pkgname}/"
}
