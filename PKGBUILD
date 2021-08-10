# Maintainer: Leo Hogan <hello@hepno.dev>

pkgname=calamares
pkgver=3.2.40
pkgrel=1
pkgdesc="Distribution-Independent Installer Framework"
arch=('x86_64')
url="https://github.com/calamares/calamares"
license=('GPL')
makedepends=('cmake' 'extra-cmake-modules' 'kpmcore' 'boost-libs' 'yaml-cpp')
depends=('qt5-svg' 'qt5-webengine' 'yaml-cpp' 'networkmanager' 'boost' 'upower'
         'kcoreaddons' 'kconfig' 'ki18n' 'kservice' 'kwidgetsaddons' 'kpmcore'
         'squashfs-tools' 'rsync' 'cryptsetup' 'qt5-xmlpatterns' 'doxygen'
         'dmidecode' 'gptfdisk' 'hwinfo' 'kparts' 'polkit-qt5' 'python' 'qt5ct'
         'solid' 'qt5-tools')
provides=("${pkgname}-${pkgver}")
source=("${url}/releases/download/v${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha512sums=('74cbe2411042e82d4e354ce269bf0827baf99f382823052520f8f18de729169c340f01af32f897e20a0d6218faea09c0581d0e2d9a4ed2db5c0f46480163f5a3')

build() {
           mkdir -p ${srcdir}/${pkgname}-${pkgver}/build
           cd ${srcdir}/${pkgname}-${pkgver}/build
           cmake -DCMAKE_BUILD_TYPE=Release -DWITH_PYTHONQT=ON ..
           make -j$(nproc)
}

package() {
           cd ${srcdir}/${pkgname}-${pkgver}/build
           make DESTDIR=${pkgdir} install
           # make the config
           sudo mkdir -p "$pkgdir/etc/calamares"
           # copy the settings.conf for calamares
           sudo wget -q https://raw.githubusercontent.com/Hep-OS/Calamares-config/master/calamares/settings.conf -P "$pkgdir/etc/calamares"
           # unconventional cd to /tmp in PKGBUILD
           cd /tmp
           git clone --depth=1 https://github.com/Hep-OS/Calamares-config
           cd Calamares-config/calamares/modules
           sudo mv * "$pkgdir/etc/calamares/modules/"
}
