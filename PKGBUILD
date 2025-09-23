pkgname=appstream
pkgver=1.1.0
pkgrel=1
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
    'vala'
    'xmlto'
)
source=(git+https://github.com/ximion/appstream#tag=v${pkgver}
    update-appstream-cache.hook)
sha256sums=(c03eb6e25f39895ff97baa9047531f4553127f04a4d1ae159ae229ec2e0ea4b6
    edc632e4a76ebe5efc76a56fe5f797e5c981cca6f2f0111c7ce0170d1330c788)

build() {
    cd ${pkgname}

    local meson_args=(
        -D vapi=true
        -D compose=true
        -D qt=false
    )

    ${meson_options} "${meson_args[@]}"

    ${meson_build}
}

package() {
    cd ${pkgname}

    ${meson_install} ${pkgdir}

    install -Dm644 ${srcdir}/update-appstream-cache.hook $pkgdir/usr/share/libalpm/hooks/90-update-appstream-cache.hook
}
