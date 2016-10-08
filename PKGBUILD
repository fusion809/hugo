# Maintainer

pkgname=hugo
pkgver=0.17
pkgrel=1
pkgdesc="Fast and Flexible Static Site Generator in Go — build from source."
arch=('i686' 'x86_64')
url="http://hugo.spf13.com/"
conflicts=('hugo')
license=('Apache')
depends=('glibc')
makedepends=('go' 'git' 'mercurial')
source=("git+https://github.com/spf13/hugo.git#tag=v${pkgver}")
sha512sums=('SKIP')

pkgver() {
  cd "${srcdir}/${pkgname}"
  git describe --tags `git rev-list --tags --max-count=1` | sed 's/v//g'
}

build() {
  cd "$srcdir/$pkgname"

  # Force our own git checkout
  export GOPATH="$srcdir"
  mkdir -p "$GOPATH/src/github.com/spf13"
  ln -s `pwd` "$GOPATH/src/github.com/spf13/hugo"

  go get -d -v .
  make no-git-info
}

package() {
  cd "$srcdir/$pkgname"
  install -Dm755 "$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
