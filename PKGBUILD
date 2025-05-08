# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: Pierre Schmitz <pierre@archlinux.de>

pkgname=cmake
pkgver=4.0.1
pkgrel=4
pkgdesc='A cross-platform open-source make system (isolated build under /opt)'
arch=('x86_64')
url="https://www.cmake.org/"
license=('custom')
depends=(
  cppdap
  curl
  expat
  gcc-libs
  glibc
  hicolor-icon-theme
  jsoncpp
  libarchive
  libuv
  ncurses
  rhash
  zlib
)
makedepends=(
  emacs
  git
  nlohmann-json
  python-sphinx
  qt6-base
  ninja
  cmake
)
optdepends=(
  'make: for unix Makefile generator'
  'ninja: for ninja generator'
  'qt6-base: cmake-gui'
)
source=(
  "git+https://gitlab.kitware.com/cmake/cmake.git#tag=v$pkgver?signed"
)
sha512sums=('0c85dee64524600e3c052aa54d2d52d3dbcd875bedeb8e72844abae20fc54267ff19c5364136b57c0a947f40bfbace547aad12cd92ae4d59d0c73bd2310e620d')
validpgpkeys=(
  CBA23971357C2E6590D9EFD3EC8FEF3A7BFB4EDA  # Brad King <brad.king@kitware.com>
)

prepare() {
  cd "${pkgname}"
  git cherry-pick -n a869b79c5921412c91fb71a761748ae5f7d3fb23 # Fix FindHDF5 for HDF5 built with cmake
}

build() {
  cmake -S "${pkgname}" -B build -G Ninja \
    -DCMAKE_INSTALL_PREFIX=/opt/cmake-4.0.1 \
    -DCMAKE_INSTALL_MANDIR=share/man \
    -DCMAKE_INSTALL_DOCDIR=share/doc/cmake \
    -DCMAKE_INSTALL_DATADIR=share/cmake \
    -DCMAKE_POLICY_VERSION_MINIMUM=3.5 \
    -DBUILD_QtDialog=ON \
    -DCMAKE_USE_SYSTEM_LIBRARIES=ON \
    -DSPHINX_MAN=ON \
    -DSPHINX_HTML=ON \
    -DCMAKE_BUILD_TYPE=Release
  cmake --build build --parallel "$(nproc)"
}

package() {
  DESTDIR="${pkgdir}" cmake --install build

  # Clean up Sphinx source listings
  rm -r "${pkgdir}/opt/cmake-4.0.1/share/doc/cmake/html/_sources"

  # Install license into opt hierarchy
  install -Dm644 "${pkgname}/LICENSE.rst" "${pkgdir}/opt/cmake-4.0.1/share/licenses/${pkgname}/LICENSE"
}
