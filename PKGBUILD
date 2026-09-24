pkgname="bakeryos-calamares"
pkgver=1.0.2
pkgrel=1
pkgdesc="Calamares for BakeryOS"
url=""
license=("GPL-3.0-or-later")
arch=('x86_64')
_ver=3.4.2
_repository="https://codeberg.org/Calamares/calamares"
options=(!debug !strip)

depends=(
  'kcoreaddons'
  'kpmcore'
  'libpwquality'
  'qt6-declarative'
  'qt6-svg'
  'yaml-cpp'

  'squashfs-tools'
  'parted'
  'gptfdisk'
  'dosfstools'

  'efibootmgr'
  'grub'
  'os-prober'

  'xdg-user-dirs'

  'konsole'
  'kcrash'
  'kservice'
  'ki18n'
  'kwidgetsaddons'
  'kconfig'
  'kconfigwidgets'
  'kdbusaddons'
  'kwindowsystem'
  'kauth'
  'kitemviews'
  'kguiaddons'
  'kcodecs'
  'karchive'
  'kjobwidgets'
  'knotifications'
  'kpackage'
)


makedepends=(
  'extra-cmake-modules' 'libglvnd' 'ninja' 'qt6-tools' 'qt6-translations'
)

source=("calamares-$_ver.tar.gz::$_repository/releases/download/v$_ver/calamares-$_ver.tar.gz")
sha256sums=('733bbbb00dc9f84874bd5c22960952f317ea2537565431179fa2152b2fbfdccc')


build() {
  rm -rf build
  
  local _cmake_options=(
    -B build
    -S "$srcdir/calamares-$_ver"
    -G Ninja
    -DCMAKE_BUILD_TYPE=Release
    -DCMAKE_INSTALL_PREFIX='/usr'
    -DCMAKE_SKIP_RPATH=ON
    -DWITH_QT6=ON
    -DBUILD_TESTING=OFF
    
    -DKDE_INSTALL_BINDIR=/usr/bin
    -DKDE_INSTALL_SBINDIR=/usr/sbin
    -DKDE_INSTALL_LIBDIR=/usr/lib
    -DKDE_INSTALL_LIBEXECDIR=/usr/libexec
    -DKDE_INSTALL_INCLUDEDIR=/usr/include
    -DKDE_INSTALL_LOCALSTATEDIR=/var
    -DKDE_INSTALL_SHAREDSTATEDIR=/usr/share
    -DKDE_INSTALL_DATAROOTDIR=/usr/share
    -DKDE_INSTALL_DATADIR=/usr/share
    -DKDE_INSTALL_LOCALEDIR=/usr/share/locale
    -DKDE_INSTALL_MANDIR=/usr/share/man
    -DKDE_INSTALL_INFODIR=/usr/share/info
    -DKDE_INSTALL_SYSCONFDIR=/etc

    -Wno-dev
  )

  cmake "${_cmake_options[@]}"
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}