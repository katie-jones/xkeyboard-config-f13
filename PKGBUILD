# Maintainer: Andreas Radke <andyrtr@archlinux.org>
# Patches added by Katie Jones.

pkgname=xkeyboard-config-f13
_pkgname=xkeyboard-config
pkgver=2.42
pkgrel=1
pkgdesc="X keyboard configuration files"
arch=(any)
license=('LicenseRef-xkeyboard-config')
url="https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config"
makedepends=('xorg-xkbcomp' 'libxslt' 'python' 'meson') # 'git')
provides=('xkbdata' 'xkeyboard-config')
replaces=('xkbdata' 'xkeyboard-config')
conflicts=('xkbdata' 'xkeyboard-config')
# https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config
source=(https://xorg.freedesktop.org/archive/individual/data/${_pkgname}/${_pkgname}-${pkgver}.tar.xz{,.sig}
    'kj.patch')
sha256sums=('a6b06ebfc1f01fc505f2f05f265f95f67cc8873a54dd247e3c2d754b8f7e0807'
            'SKIP'
            'SKIP'
)
validpgpkeys=('FFB4CCD275AAA422F5F9808E0661D98FC933A145') # Sergey Udaltsov <sergey.udaltsov@gmail.com>

prepare() {
  cd ${_pkgname}-${pkgver}
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
  install -Dt "$pkgdir/usr/share/licenses/$_pkgname" -m644 $_pkgname-$pkgver/COPYING
}
