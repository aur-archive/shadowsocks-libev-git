# Contributor: xjpvictor Huang <ke [AT] xjpvictor [DOT] info>
pkgname=shadowsocks-libev-git
pkgver=20130908
pkgrel=1
pkgdesc="A lightweight secured scoks5 proxy for embedded devices and low end boxes"
url="https://github.com/madeye/shadowsocks-libev"
license=('GPL' 'custom')
arch=('i686' 'x86_64')
makedepends=('autoconf' 'libtool')
conflicts=('shadowsocks-libuv-git' 'shadowsocks-nodejs-git')

_gitroot="git://github.com/madeye/shadowsocks-libev.git"
_gitname="shadowsocks"
source=(${_gitname}@.service
        tmpfiles.d)

build() {
  cd ${srcdir}
  if [ -d ${_gitname} ] ; then
    cd ${_gitname} && git pull origin
    msg "The local files are updated."
  else
    git clone ${_gitroot} ${_gitname}
    msg "GIT checkout done."
  fi

  cd ${srcdir}/${_gitname}
  ./configure --prefix=/usr \
              --sbindir=/usr/bin
  make
}

package() {
  cd ${srcdir}/${_gitname}
  make DESTDIR="${pkgdir}" install

  install -Dm600 ./debian/config.json ${pkgdir}/etc/${_gitname}/config.json.sample
  install -Dm644 ${srcdir}/${_gitname}@.service ${pkgdir}/usr/lib/systemd/system/${_gitname}@.service
  install -dm755 ${pkgdir}/run/${_gitname}
  install -Dm644 ${srcdir}/tmpfiles.d ${pkgdir}/usr/lib/tmpfiles.d/${_gitname}.conf

  # Copy License
  install -Dm644 COPYING ${pkgdir}/usr/share/licenses/${_gitname}/COPYING
  install -Dm644 LICENSE ${pkgdir}/usr/share/licenses/${_gitname}/LICENSE
}
md5sums=('bb7e53f6da7ce26e1cbe55e510fcad3f'
         '667e6b707f80bc5c15dbf4a22d78355c')
