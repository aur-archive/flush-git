# Maintainer: CYB3R <dima@golovin.in>

pkgname=flush-git
pkgver=20130202
pkgrel=1
pkgdesc="GTK+ based BitTorrent client"
arch=('i686' 'x86_64')
url="http://sourceforge.net/projects/flush/"
license=('GPL')
depends=('libconfig' 'libtorrent-rasterbar' 'libglademm' 'libnotify' 'dbus-core')
makedepends=('boost' 'git')
install=${pkgname}.install
conflicts=('flush' 'flush-new')
replaces=('flush' 'flush-new')

_gitroot="git://github.com/KonishchevDmitry/flush.git"
_gitname="${pkgname}"

build() {    
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."
  
  cd "${srcdir}/${pkgname}"

   # No idea what is it, but compiling works fine without. Curiosity never killed the cat, so ask previous maintaner. 
   # export LDFLAGS="${LDFLAGS//-Wl,--as-needed}"
    export CXXFLAGS="${CXXFLAGS} -DBOOST_FILESYSTEM_VERSION=3" # I just incremented this number. CYB3R
    ./configure --prefix=/usr
    make
}

package() {
    cd "${srcdir}/${pkgname}"
    make DESTDIR="${pkgdir}/" install
}
