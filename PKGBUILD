# Maintainer: Frederik Schwan <frederik dot schwan at linux dot com>

pkgbase=goland-eap
_pkgbase=goland
pkgname=(goland-eap goland-eap-jre)
pkgver=181.2784.36
pkgrel=1
pkgdesc='Capable and Ergonomic Go IDE'
arch=('x86_64' 'i686')
url='https://www.jetbrains.com/go/'
license=('Commercial')
makedepends=('rsync')
options=('!strip')
source=(https://download.jetbrains.com/go/${_pkgbase}-${pkgver}.tar.gz
        jetbrains-goland-eap.desktop)
sha512sums=('ee6a56e6001f006f015b7a00c25938141d7d0deeda39f61bccfd6add77745d1414d93997f4f20e5a1a95c9516963de4cce6e6e38ae9e73e9b665b9815dace5d8'
            'fc3f13133e8e9d68d351e9f628f9424c5aec5a323d92c6356ad2a44be69fbf947f3aa458e48139108b0ac2b71bbb9271506b8d91a76f46f7d32cdadf6d8fa962')

package_goland-eap() {
  optdepends=('goland-eap-jre: JetBrains custom Java Runtime (Recommended)'
              'java-runtime>=8: JRE - Required if goland-jre is not installed')
  conflicts=('gogland-eap')
  replaces=('gogland-eap')

  install -d -m 755 "${pkgdir}/opt/"
  install -d -m 755 "${pkgdir}/usr/bin/"
  install -d -m 755 "${pkgdir}/usr/share/applications/"
  install -d -m 755 "${pkgdir}/usr/share/pixmaps/"

  rsync -rtl "${srcdir}/GoLand-${pkgver}/" "${pkgdir}/opt/${pkgbase}" --exclude=/jre64

  chmod +x "${pkgdir}/opt/${pkgbase}/plugins/intellij-go-plugin/lib/dlv/linux/dlv"
  ln -s "/opt/${pkgbase}/bin/${_pkgbase}.sh" "${pkgdir}/usr/bin/${pkgbase}"
  install -D -m 644 "${srcdir}/jetbrains-${pkgbase}.desktop" "${pkgdir}/usr/share/applications/"
  install -D -m 644 "${pkgdir}/opt/${pkgbase}/bin/${_pkgbase}.png" "${pkgdir}/usr/share/pixmaps/${pkgbase}.png"
}

package_goland-eap-jre() {
  conflicts=('gogland-eap-jre')
  replaces=('gogland-eap-jre')

  install -d -m 755 "${pkgdir}/opt/${pkgbase}"
  rsync -rtl "${srcdir}/GoLand-${pkgver}/jre64" "${pkgdir}/opt/${pkgbase}"
}
