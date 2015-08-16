# Maintainer: oke3 <Sekereg at gmx dot com>

pkgname=kid3-git
pkgver=20130324
pkgrel=1
pkgdesc="An MP3, Ogg/Vorbis and FLAC tag editor for KDE."
arch=('i686' 'x86_64')
url="http://kid3.sourceforge.net/"
license=('GPL')
install=$pkgname.install
makedepends=('automoc4' 'cmake' 'docbook-xsl' 'git')
depends=('id3lib' 'kdelibs' 'kdebase-runtime' 'chromaprint')
provides=('kid3')
conflicts=('kid3')

_gitroot="git://kid3.git.sourceforge.net/gitroot/kid3/kid3"
_gitname="kid3"

build() {
    cd "$srcdir"

    msg "Connecting to the GIT server...."
    if [[ -d "$_gitname" ]]; then
        cd "$_gitname" && git pull origin && cd "$srcdir"
        msg "The local files are updated."
    else
        git clone "$_gitroot" "$_gitname"
    fi

    msg "GIT checkout done or server timeout"
    msg "Starting build..."

    rm -rf "$_gitname-build"
    git clone "$_gitname" "$_gitname-build"
    cd "$_gitname-build"

    cmake -DCMAKE_INSTALL_PREFIX=/usr
    make
}

package() {
    cd "$srcdir/$_gitname-build"

    make DESTDIR="$pkgdir" install
}
