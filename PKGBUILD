# Maintainer: laloch <laloch@atlas.cz>
pkgname=qtcreator-py-reborn-git
pkgver=20130306
pkgrel=1
pkgdesc="Qt Creator with Python / PySide support"
arch=('i686' 'x86_64')
url="http://qt.gitorious.org/~sergey-shambir/qt-creator/qt-creator-py-reborn"
license=('LGPL')
depends=('qt4')
makedepends=('qt4-private-headers' 'git')
optdepends=('qt-doc: for the integrated Qt documentation'
            'gdb: for the debugger'
            'cmake: for cmake project support'
            'openssh-askpass: for ssh support'
            'git: for git support'
            'mercurial: for mercurial support'
            'bzr: for bazaar support'
            'valgrind: for analyze support')
provides=('qtcreator')
conflicts=('qtcreator')
options=('!emptydirs' 'docs')
install="qtcreator-py-reborn-git.install"
source=('qtcreator.desktop')
md5sums=('82888d4be900e7833d768050a135cd37')

_gitroot=git://gitorious.org/~sergey-shambir/qt-creator/qt-creator-py-reborn.git
_gitname=qt-creator-py-reborn

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  
  rm -rf ${srcdir}/${_gitname}-build
  mkdir ${srcdir}/${_gitname}-build && cd ${srcdir}/${_gitname}-build

  msg2 'Starting make...'
  qmake ${srcdir}/${_gitname}/qtcreator.pro
  make
  make docs -j1
}

package() {
  cd ${srcdir}/${_gitname}-build
  make INSTALL_ROOT="${pkgdir}/usr/" install
  make INSTALL_ROOT="${pkgdir}/usr/" install_docs

  install -Dm644 ${srcdir}/qtcreator.desktop ${pkgdir}/usr/share/applications/qtcreator.desktop
}

# vim:set ts=2 sw=2 et:
