# Originally copied from [AUR](https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=dwm).

# $Id$
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'dmenu')

prepare() {
  # Merge remote patch branches.
  git branch --list -r "*/patch-*" | while read branch; do
    echo "Merging branch: $branch"
    git merge $branch -m "$branch"
  done

  # Create a directory in srcdir and cd into it.
  mkdir -p $srcdir/$pkgname-$pkgver
  cd $srcdir/$pkgname-$pkgver

  # Copy all files at the root of the repo into the new directory and ignore errors.
  cp $startdir/* . 2> /dev/null || true

  # Remove unneeded files.
  rm -f PKGBUILD README.md $pkgname-*.tar.xz
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC="/usr/include/X11" X11LIB="/usr/lib/X11" FREETYPEINC="/usr/include/freetype2"
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX="/usr" DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D dwm.desktop "$pkgdir/usr/share/xsessions/dwm.desktop"
}
