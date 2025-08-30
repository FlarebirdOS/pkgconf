pkgname=pkgconf
pkgver=2.5.1
pkgrel=2
pkgdesc="Package compiler and linker metadata toolkit"
arch=('x86_64')
url="http://pkgconf.org/"
license=('ISC')
groups=('base-devel')
depends=('glibc')
makedepends=('meson')
source=(https://distfiles.ariadne.space/${pkgname}/${pkgname}-${pkgver}.tar.xz
    x86_64-flarebird-linux-gnu.personality
    i686-flarebird-linux-gnu.personality)
sha256sums=(cd05c9589b9f86ecf044c10a2269822bc9eb001eced2582cfffd658b0a50c243
    831befbcfab07c35e87b6e63d4646071d896c8b74e672a1720abb9c27813c47c
    57637de34b6c53d473b2ef04e01ac09bff783f9c4d272bada4368b2cc72caa0c)

build() {
    cd ${pkgname}-${pkgver}

    local meson_args=(
        -D tests=disabled
    )

    ${meson_options} "${meson_args[@]}"

    ${meson_build}

}

package() {
    cd ${pkgname}-${pkgver}

    ${meson_install} ${pkgdir}

    ln -sv pkgconf ${pkgdir}/usr/bin/pkg-config
    ln -sv pkgconf.1 ${pkgdir}/usr/share/man/man1/pkg-config.1

    for p in {x86_64,i686}-flarebird-linux-gnu; do
        install -Dt ${pkgdir}/usr/share/pkgconfig/personality.d -m644 ${srcdir}/${p}.personality
        ln -sv pkgconf ${pkgdir}/usr/bin/${p}-pkg-config
    done
}
