# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=darcs-beta
pkgname=darcs-beta
pkgver=2.7.99.2
pkgrel=1
pkgdesc="a distributed, interactive, smart revision control system"
url="http://hackage.haskell.org/package/${_hkgname}"
license=('GPL')
arch=('i686' 'x86_64')
makedepends=()
depends=('gmp' 'curl' 'ghc' 'haskell-http=4000.0.9' 'haskell-array=0.3.0.1' 'haskell-bytestring=0.9.1.7' 'haskell-containers=0.3.0.0' 'haskell-directory=1.0.1.1' 'haskell-extensible-exceptions=0.1.1.1' 'haskell-filepath=1.1.0.4' 'haskell-hashed-storage<0.6' 'haskell-haskeline<0.7' 'haskell-html=1.0.1.2' 'haskell-mmap<0.6' 'haskell-mtl<1.2' 'haskell-network=2.2.1.7' 'haskell-old-time=1.0.0.5' 'haskell-parsec=2.1.0.1' 'haskell-process=1.0.1.3' 'haskell-random=1.0.0.2' 'haskell-regex-compat=0.93.1' 'haskell-tar<0.4' 'haskell-terminfo<0.4' 'haskell-text>=0.3' 'haskell-unix=2.4.0.2' 'haskell-zlib=0.5.2.0' 'curl')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/darcs-beta/2.7.99.2/darcs-beta-2.7.99.2.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
}
md5sums=('e27077ece0d69bbf659d2570c49cefd2')
