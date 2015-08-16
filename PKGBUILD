# Maintainer:  TDY <tdy@archlinux.info>
# Contributor: Thomas Cyron <thomas@fooo.org>

pkgname=hgview-hg
pkgver=906
pkgrel=1
pkgdesc="A revision history browser for mercurial repositories"
arch=('any')
url="http://www.logilab.org/project/hgview/"
license=('GPL')
depends=('docutils' 'mercurial>=1.0' 'python2-egenix-mx-base' 'python2-qscintilla')
makedepends=('asciidoc' 'xmlto')
provides=('hgview')
conflicts=('hgview')

_hgroot=http://hg.logilab.org/
_hgrepo=hgview

build() {
  cd "$srcdir"

  if [[ -d $_hgrepo/.hg ]]; then
    (cd $_hgrepo && hg pull -u)
  else
    hg clone $_hgroot/$_hgrepo
  fi

  rm -rf $_hgrepo-build
  hg clone $_hgrepo $_hgrepo-build
  cd $_hgrepo-build

  python2 setup.py build
}

package() {
  cd "$srcdir/$_hgrepo-build"
  sed -i '/^MANDIR=/ s,man,share/,' doc/Makefile
  python2 setup.py install --prefix=/usr --root="$pkgdir" --optimize=1
}

# vim:set ts=2 sw=2 et:
