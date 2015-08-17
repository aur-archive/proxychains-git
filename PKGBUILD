# Contributor: Jianing YANG < jianingy.yang at gmail dot com >

pkgname=proxychains-git
pkgver=20130114
pkgrel=1
pkgdesc="a tool that forces any TCP connection made by any given application to follow through proxy like TOR or any other SOCKS4, SOCKS5 or HTTP(S) proxy."
url="https://github.com/haad/proxychains"
depends=('git')
arch=('i686' 'x86_64')
license=('GPL2')
provides=('proxychains')
conflicts=('proxychains')
backup=(etc/proxychains.conf)
_pkgname='proxychains'

_gitroot="git://github.com/rofl0r/proxychains.git"
_gitname="proxychains"

build() {
  cd "${srcdir}"
  msg "Connecting to GIT server..."

  if [ -d ${_gitname} ]; then
    cd ${_gitname} && git pull origin
    msg "The local files are updated."
  else
    git clone ${_gitroot} ${_gitname}
  fi
  msg "GIT checkout done or server timeout."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  ./configure --prefix=/usr
  echo "sysconfdir=etc" >> config.mak
  make
}

package() {
  cd ${srcdir}/${_gitname}-build

  make DESTDIR=${pkgdir}/ install && make DESTDIR=${pkgdir}/ install-config
  install -D -m644 COPYING ${pkgdir}/usr/share/licenses/${pkgname}/COPYING
}
