pkgname=(
    appstream
    appstream-qt
)
pkgbase=appstream
pkgver=1.1.0
pkgrel=2
pkgdesc="Provides a standard for creating app stores across distributions"
arch=('x86_64')
url="https://distributions.freedesktop.org/wiki/AppStream"
license=('LGPL-2.1-or-later')
depends=(
    'cairo'
    'curl'
    'fontconfig'
    'freetype2'
    'gcc-libs'
    'gdk-pixbuf'
    'glib2'
    'glibc'
    'libfyaml'
    'librsvg'
    'libstemmer'
    'libxml2'
    'libxmlb'
    'pango'
    'systemd-libs'
    'zstd'
)
makedepends=(
    'git'
    'glib2-devel'
    'gobject-introspection'
    'gperf'
    'itstool'
    'meson'
    'python-gi-docgen'
    'qt6-qttools'
    'vala'
    'xmlto'
)
source=(git+https://github.com/ximion/appstream#tag=v${pkgver}
    update-appstream-cache.hook)
sha256sums=(c03eb6e25f39895ff97baa9047531f4553127f04a4d1ae159ae229ec2e0ea4b6
    edc632e4a76ebe5efc76a56fe5f797e5c981cca6f2f0111c7ce0170d1330c788)

build() {
    cd ${pkgbase}

    local meson_args=(
        -D vapi=true
        -D compose=true
        -D qt-versions=6
        -D qt=true
    )

    ${meson_options} "${meson_args[@]}"

    ${meson_build}
}

package_appstream() {
    cd ${pkgbase}

    ${meson_install} ${pkgdir}

    install -Dm644 ${srcdir}/update-appstream-cache.hook $pkgdir/usr/share/libalpm/hooks/90-update-appstream-cache.hook

    # provided by -qt subpackage
    rm -r $pkgdir/usr/{include/AppStreamQt,lib64/cmake,lib64/libAppStreamQt.*}
}

package_appstream-qt() {
    pkgdesc='Qt6 interface for AppStream'
    depends=(
        'appstream'
        'gcc-libs'
        'glib2'
        'glibc'
        'qt6-qtbase'
    )

    cd ${pkgbase}

    ${meson_install} ${pkgdir}

    # provided by appstream
    rm -r ${pkgdir}/usr/{bin,include/appstream{,-compose},lib64/{girepository-1.0,libappstream*,pkgconfig},libexec/appstreamcli-compose,share}
}
