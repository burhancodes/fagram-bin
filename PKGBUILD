# Maintainer: omansh-krishn <omanshkrishn@duck.com>
pkgname=fagram-bin
pkgver=v4.20.2
pkgrel=1
pkgdesc="Telegram Desktop based messenger with Feature-rich modifications - Binary Version"
arch=(x86_64)
url="https://github.com/FajoX1/fagramdesktop"
license=(GPL3)
depends=('hunspell' 'ffmpeg' 'hicolor-icon-theme' 'lz4' 'minizip' 'openal'
         'qt6-imageformats' 'qt6-svg' 'qt6-wayland' 'xxhash'
         'rnnoise' 'pipewire' 'libxtst' 'libxrandr' 'libxcomposite' 'libxdamage' 'abseil-cpp' 'libdispatch'
         'openssl' 'protobuf' 'glib2' 'libsigc++-3.0' 'kcoreaddons')
makedepends=('chrpath')
optdepends=('webkit2gtk: embedded browser features'
            'xdg-desktop-portal: desktop integration')
provides=('fagram')
conflicts=('fagram')

source=("https://github.com/burhancodes/fagram-rpm/releases/download/${pkgver}/fagram-${pkgver}.tar.gz")

sha256sums=('SKIP') # Replace with actual SHA256 sum after downloading the file

package() {
    cd "$srcdir/"

    # Creating needed directories
    install -dm755 "$pkgdir/usr/bin"
    install -dm755 "$pkgdir/usr/share"
    install -dm755 "$pkgdir/usr/share/applications"
    install -dm755 "$pkgdir/usr/share/dbus-1"
    install -dm755 "$pkgdir/usr/share/icons"
    install -dm755 "$pkgdir/usr/share/pixmaps"
    install -dm755 "$pkgdir/usr/share/metainfo"

    # Application executable
    install -Dm755 "$srcdir/usr/bin/fagram" "$pkgdir/usr/bin/fagram"

    # Remove RPATH informations
    chrpath --delete "$pkgdir/usr/bin/fagram"

    # Desktop launcher
    install -Dm644 "$srcdir/usr/share/icons/hicolor/256x256/apps/fagram.png" "$pkgdir/usr/share/pixmaps/fagram.png"
    install -Dm644 "$srcdir/usr/share/applications/org.fagram.desktop.fagram.desktop" "$pkgdir/usr/share/applications/org.fagram.desktop.fagram.desktop"

    # DBus service
    install -Dm644 "$srcdir/usr/share/dbus-1/services/org.fagram.desktop.fagram.service" "$pkgdir/usr/share/dbus-1/services/org.fagram.desktop.fagram.service"

    # Metainfo
    install -Dm644 "$srcdir/usr/share/metainfo/org.fagram.desktop.fagram.metainfo.xml" "$pkgdir/usr/share/metainfo/org.fagram.desktop.fagram.metainfo.xml"

    # Icons
    local icon_size icon_dir
    for icon_size in 16 32 48 64 128 256 512; do
        icon_dir="$pkgdir/usr/share/icons/hicolor/${icon_size}x${icon_size}/apps"
        install -d "$icon_dir"
        install -m644 "$srcdir/usr/share/icons/hicolor/${icon_size}x${icon_size}/apps/fagram.png" "$icon_dir/fagram.png"
    done
}

