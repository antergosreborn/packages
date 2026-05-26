pkgname=cnchi-revive
pkgver=26.0.7
pkgrel=1
pkgdesc='Revived Antergos graphical installer'
arch=('x86_64')
url='https://gitlab.com/antergos-revive/packages/cnchi-revive'
license=('GPL3')

depends=(
  'python'
  'python-gobject'
  'gtk3'
  'python-requests'
  'python-mako'
  'python-parted'
  'pyalpm'
  'upower'
  'gptfdisk'
  'parted'
  'webkit2gtk'
)

makedepends=('git' 'gettext')

provides=('cnchi')
conflicts=('cnchi')

source=("git+https://gitlab.com/antergos-revive/packages/cnchi-revive.git")
sha256sums=('SKIP')

package() {
    cd "${srcdir}/cnchi-revive"

    install -d "${pkgdir}/usr/share/cnchi"
    install -d "${pkgdir}/usr/share/locale"

    install -Dm755 "bin/cnchi" "${pkgdir}/usr/bin/cnchi"
    install -Dm644 "cnchi.desktop" "${pkgdir}/usr/share/applications/cnchi.desktop"
    install -Dm644 "data/images/antergos/antergos-icon.png" "${pkgdir}/usr/share/pixmaps/cnchi.png"

    for i in src bin data scripts ui; do
        cp -R "${i}" "${pkgdir}/usr/share/cnchi/"
    done

    for files in po/*.po; do
        if [ -f "$files" ] && [ "$files" != 'po/cnchi.pot' ]; then
            lang="${files#*/}"
            lang="${lang%.po}"
            mkdir -p "${pkgdir}/usr/share/locale/${lang}/LC_MESSAGES"
            msgfmt "$files" -o "${pkgdir}/usr/share/locale/${lang}/LC_MESSAGES/cnchi.mo"
        fi
    done
}