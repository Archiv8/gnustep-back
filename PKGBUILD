#!/bin/bash

# Based on original packaging by <mumei AT airmail DOT cc>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/gnustep-back/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/gnustep-back/discussions>

pkgname=gnustep-back
pkgver=0.29.0
pkgrel=1
pkgdesc="The GNUstep GUI Backend"
arch=(
  "x86_64"
)
url="http://www.gnustep.org/"
license=(
  "LGPL"
)
depends=(
  "libgl"
  "libxmu"
  "gcc-libs"
  "freetype2"
  "cairo"
)
makedepends=(
  "gnustep-make"
  "gnustep-base"
  "gnustep-gui>=0.28.0"
  "libffi"
  "gcc-objc"
)
conflicts=(
  "gnustep-back-svn"
)
groups=(
  "gnustep-core"
)
source=(
  "https://github.com/gnustep/libs-back/releases/download/back-${pkgver//./_}/gnustep-back-$pkgver.tar.gz{,.sig}"
)
sha512sums=(
  "18dd4e9200abef16570b331e8725d2ecf808fa86d125a927cc9776e8b88a9892"
  "SKIP"
)
validpgpkeys=(
  "83AAE47CE829A4146EF83420CA868D4C99149679"
)

build() {
  cd "$srcdir"/$pkgname-$pkgver

  . /usr/share/GNUstep/Makefiles/GNUstep.sh

  ./configure --prefix=/usr --sysconfdir=/etc/GNUstep

  make
}

package() {
  cd "$srcdir"/$pkgname-$pkgver

  . /usr/share/GNUstep/Makefiles/GNUstep.sh

  make DESTDIR="$pkgdir" install

  mkdir -p "$pkgdir"/etc/ld.so.conf.d

  cat > "$pkgdir"/etc/ld.so.conf.d/gnustep.conf << EOF

/opt/GNUstep/System/Library/Libraries

/usr/lib/GNUstep/Libraries

EOF
}
