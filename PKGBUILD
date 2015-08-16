# Maintainer: luminoso < luminoso AT gmail DOT com>
#Shameless copy from vertcoin-git package

pkgname='monocle-git'
_gitname='monocle'
pkgver=0.8.7.1.r8
pkgrel=1
arch=('i686' 'x86_64')
url="https://monocle.vertcoin.org/"
depends=('qt4>=4.6' 'boost-libs>=1.46' 'miniupnpc>=1.6' 'qrencode>=3.4.3')
makedepends=('boost' 'automoc4' 'qrencode' 'miniupnpc' 'git')
license=('MIT')
pkgdesc="Peer-to-peer network based digital currency (includes 
both the qtclient and the headless daemon)"
provides=(monocle)
conflicts=(monocle)
source=("git://github.com/erkmos/monocle.git"
		monocle-git.desktop
		)
md5sums=('SKIP'
	'082699787294dd3b9413ee4e2f6877dc'
		)

pkgver() {
	cd "$srcdir/$_gitname"
	# Use tag of the last commit, but removing the prefix
	git describe --long | sed -r 's/^v//;s/([^-]*-g)/r\1/;s/-/./g'
}

build() {
	cd "${_gitname}"
	cd "$srcdir/$_gitname"

	# and make qt gui
	qmake-qt4 USE_QRCODE=1 USE_UPNP=1
	make

	# make monocle daemon
	cd "$srcdir/$_gitname/src"
	make $MAKEFLAGS -f makefile.unix
}


package() {
	# install monocle-qt client
	install -D -m755 "$srcdir/$_gitname/monocle-qt" "$pkgdir/usr/bin/monocle-qt"

	# install monocle daemon
	install -D -m755 "$srcdir/$_gitname/src/monocled" "$pkgdir/usr/bin/monocled"

	# install license
	install -D -m644 "$srcdir/$_gitname/COPYING" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

	# install monocle-qt desktop entry
	install -D -m644 "$srcdir/$_gitname/share/pixmaps/monocle128.png" "$pkgdir/usr/share/pixmaps/monocle128.png"
	install -D -m644 "$pkgname.desktop" "$pkgdir/usr/share/applications/monocle-git.desktop"
}
