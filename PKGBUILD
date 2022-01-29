# Maintainer: Dylan Araps <dylan.araps@gmail.com>
#
# Below are the maintainers and contributors of the official
# Arch package that this PKGBUILD is based on.
#
# Maintainer: Florian pritz <bluewind@xinu.at>
# Contributor: Bartłomiej Piotrowski <nospam@bpiotrowski.pl>
# Contributor: Brad Fanella <bradfanella@archlinux.us>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: tobias <tobias@archlinux.org>
# Maintainer: Solomon Choina <shlomochoina@gmail.com
pkgname=openbox-debian
_pkgname=openbox
pkgver=3.6.1
pkgrel=2
pkgdesc='Openbox with Patches from Debian.'
arch=('i686' 'x86_64')
url='http://openbox.org'
license=('GPL')
provides=('libobrender.so' $_pkgname 'openbox')
conflicts=($_pkgname)
depends=('startup-notification' 'libxml2' 'libxinerama' 'libxrandr'
         'libxcursor' 'pango' 'imlib2' 'librsvg' 'libsm')
optdepends=('gnome-panel: for the openbox gnome session '
            'plasma-workspace: for the KDE/Openbox xsession'
            'python-xdg: for the openbox-xdg-autostart script')
makedepends=('automake-1.11' 'docbook-to-man')
groups=('lxde' 'lxde-gtk3' 'lxqt')
backup=('etc/xdg/openbox/menu.xml'
        'etc/xdg/openbox/rc.xml'
        'etc/xdg/openbox/autostart'
        'etc/xdg/openbox/environment')
source=("http://openbox.org/dist/openbox/${_pkgname}-${pkgver}.tar.gz"
        "http://http.debian.net/debian/pool/main/o/openbox/openbox_3.6.1-9+deb11u1.debian.tar.xz")
md5sums=('b72794996c6a3ad94634727b95f9d204'
         'SKIP')

prepare() {
    cd "${_pkgname}-${pkgver}"
    
    for p in ../debian/patches/*; do
     if [ "${f##*.}" = "patch" ]; then
      msg "Applying ${f}"
      patch -p1 -i "../debian/patches/${f}"
     fi
    done
    
}

build() {
    cd "${_pkgname}-${pkgver}"

    ./configure \
        --prefix=/usr \
        --with-x \
        --enable-startup-notification \
        --sysconfdir=/etc \
        --libexecdir=/usr/lib/openbox
    make
}

package() {
    cd "${_pkgname}-${pkgver}"
    make DESTDIR="$pkgdir" install

    sed -i 's:startkde:/usr/bin/\0:' \
        "${pkgdir}/usr/share/xsessions/openbox-kde.desktop"
}
