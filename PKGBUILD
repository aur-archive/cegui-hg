# Maintainer: Pavlos Touboulidis <pavlos256-gmail-com>
# Contributor: Predator106
pkgname=cegui-hg
pkgver=3832
pkgrel=1
pkgdesc="A free library providing windowing and widgets for graphics APIs/engines (Mercurial)"
arch=('i686' 'x86_64')
url="http://www.cegui.org.uk/"
license=('MIT')
depends=('pcre' 'glew' 'expat' 'freetype2' 'devil' 'freeglut' 'lua' 'silly' 'boost')
optdepends=('ogre: build the Ogre rendering module'
'doxygen: build documentation'
'minizip: build the minizip based resource provider'
'libxml2: build libxml support')
makedepends=('mercurial' 'python2' 'cmake')
provides=('cegui')
conflicts=('cegui')
#options=('!libtool')
md5sums=() #generate with 'makepkg -g'

_hgroot=http://bitbucket.org/cegui/
_hgrepo=cegui

build() {
  cd "$srcdir"
  msg "Connecting to Mercurial server...."

  if [[ -d "$_hgrepo" ]]; then
    cd "$_hgrepo"
    hg pull -u
    msg "The local files are updated."
  else
    hg clone "$_hgroot" "$_hgrepo"
  fi

  msg "Mercurial checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_hgrepo-build"
  cp -r "$srcdir/$_hgrepo" "$srcdir/$_hgrepo-build"
  cd "$srcdir/$_hgrepo-build"

  #
  # BUILD HERE
  #
  cmake . \
	-DCMAKE_INSTALL_PREFIX:PATH=/usr \
	-DCEGUI_SLOTTED_INSTALLATION:BOOL=OFF \
	-DPYTHON_EXECUTABLE=/usr/bin/python2 \
	-DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
	-DPYTHON_INCLUDE_DIR=/usr/include/python2.7/ # -DCMAKE_BUILD_TYPE:STRING=Debug
}

package() {
  cd "$srcdir/$_hgrepo-build"
  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
