# Maintainer: Your Name <youremail@domain.com>

pkgname=taffybar-git
_gitname=taffybar
pkgver=20141119
pkgrel=1
pkgdesc="A desktop bar similar to xmobar, but with more GUI"
arch=(i386 x86_64)
url="http://github.com/travitch/taffybar"
license=('BSD3')
depends=('haskell-text'
         'haskell-http'
         'haskell-parsec>=3.1'
         'haskell-mtl>=2'
         'haskell-network'
         'haskell-cairo'
         'haskell-dbus>=0.10.1'
         'haskell-gtk>=0.12.1'
         'haskell-dyre>=0.8.6'
         'haskell-hstringtemplate'
         'haskell-gtk-traymanager>=0.1.2'
         'haskell-xdg-basedir'
         'haskell-filepath'
         'haskell-utf8-string'
         'haskell-stm'
         'haskell-split'
         'haskell-enclosed-exceptions'
         'haskell-safe'
         'haskell-xmonad'
         'haskell-xmonad-contrib')
makedepends=('ghc' 'gtk2hs-buildtools')
provides=('taffybar')
conflicts=()
replaces=()
backup=()
options=()
install=$pkgname.install
source=(git+http://github.com/travitch/taffybar.git)
md5sums=('SKIP')

build() {
  cd "$_gitname"

	runhaskell Setup configure -O --enable-split-objs --enable-shared \
		--prefix=/usr --docdir="/usr/share/doc/$pkgname" \
		--libsubdir=\$compiler/site-local/\$pkgid
	runhaskell Setup build
	runhaskell Setup haddock
	runhaskell Setup register   --gen-script
	runhaskell Setup unregister --gen-script
	sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}

package() {
	cd "$_gitname"

	install -D -m744 register.sh   "$pkgdir/usr/share/haskell/$pkgname/register.sh"
	install	   -m744 unregister.sh "$pkgdir/usr/share/haskell/$pkgname/unregister.sh"
	install -d -m755 "$pkgdir/usr/share/doc/ghc/html/libraries"
	ln -s "/usr/share/doc/$pkgname/html" "$pkgdir/usr/share/doc/ghc/html/libraries/$_hkgname"
	runhaskell Setup copy --destdir="$pkgdir"
}

# vim:set ts=2 sw=2 et:
