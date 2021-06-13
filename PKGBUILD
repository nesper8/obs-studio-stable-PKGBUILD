pkgname=obs-studio
pkgver=27.0.0
pkgrel=6
pkgdesc="Free and open source software for video recording and live streaming."
arch=('x86_64')
url="https://obsproject.com"
license=("GPL2")
depends=("ffmpeg" "jansson" "libxinerama" "libxkbcommon-x11" "mbedtls"
         "qt5-svg" "qt5-x11extras" "curl" "jack" "gtk-update-icon-cache" "pipewire")
makedepends=("cmake" "git" "libfdk-aac" "libxcomposite" "x264"
             "swig" "luajit" "python" "cef-minimal>=87.0.0" "wayland"
             "qt5-wayland" "xdg-desktop-portal")
optdepends=("libfdk-aac: FDK AAC codec support"
            "libxcomposite: XComposite capture support"
            "libva-intel-driver: hardware encoding"
            "libva-mesa-driver: hardware encoding"
            "luajit: Lua scripting"
            "python: Python scripting"
            "v4l2loopback-dkms: Virtual webcam"
            "xdg-desktop-portal: Pipewire capture")
provides=("obs-studio=$pkgver")
conflicts=("obs-studio")
source=("$pkgname-$pkgver.tar.gz::https://github.com/obsproject/obs-studio/archive/$pkgver.tar.gz"
        "git+https://github.com/microsoft/ftl-sdk.git"
        "git+https://github.com/obsproject/obs-browser.git"
        "git+https://github.com/obsproject/obs-vst.git"
        "fix_python_binary_loading.patch::https://raw.githubusercontent.com/archlinux/svntogit-community/packages/obs-studio/trunk/fix_python_binary_loading.patch")
md5sums=("cd3da7551dc4a007c6b01145d037b910" "SKIP" "SKIP" "SKIP" "051b90f05e26bff99236b8fb1ad377d1")

prepare() {
  cd $pkgname-$pkgver
  patch -Np1 < "$srcdir"/fix_python_binary_loading.patch
}

build() {
  cp -r ftl-sdk $pkgname-$pkgver/plugins/
  cp -r obs-browser $pkgname-$pkgver/plugins/
  cp -r obs-vst $pkgname-$pkgver/plugins/

  cd $pkgname-$pkgver

  mkdir -p build; cd build

  cmake \
    -DUNIX_STRUCTURE=1 \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DBUILD_BROWSER=ON \
    -DDISABLE_VLC=ON \
    -DCEF_ROOT_DIR="/opt/cef" \
    -DOBS_VERSION_OVERRIDE="$pkgver-$pkgrel" .. \
    -DENABLE_PIPEWIRE=ON

  make
}

package() {
  cd $pkgname-$pkgver/build

  make install DESTDIR="$pkgdir"
}

