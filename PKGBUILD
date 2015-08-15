# Maintainer: Simon Legner <Simon.Legner@gmail.com>
# Maintainer: Chris Molozian (novabyte) <chris DOT molozian AT gmail DOT com>
# Contributor: Sanjuro Makabe (itti) <vuck AT gmx DOT de>
pkgname=('gradle' 'gradle-doc' 'gradle-src')
pkgbase=gradle
pkgver=2.5
pkgrel=1
pkgdesc=('A powerful build system for the JVM')
arch=('any')
url='https://gradle.org/'
license=('APACHE')
depends=('java-environment')
makedepends=('zip')
source=("https://services.gradle.org/distributions/${pkgbase}-${pkgver}-all.zip"
        "${pkgbase}.sh")

package_gradle(){
  # install profile.d script
  install -dm755 "${pkgdir}"/etc/profile.d
  install -m755 "${srcdir}/${pkgbase}.sh" "${pkgdir}/etc/profile.d/"
  cd "${srcdir}/${pkgname}-${pkgver}"

  # create the necessary directory structure
  mkdir -p "${pkgdir}/usr/share/java/${pkgname}/bin"
  mkdir -p "${pkgdir}/usr/share/java/${pkgname}/lib/plugins"
  mkdir -p "${pkgdir}/usr/share/java/${pkgname}/init.d"
  mkdir -p "${pkgdir}/usr/bin"

  # copy across jar files
  install -Dm644 lib/*.jar "${pkgdir}/usr/share/java/${pkgname}/lib" || return 1
  install -Dm644 lib/plugins/*.jar "${pkgdir}/usr/share/java/${pkgname}/lib/plugins" || return 1

  # copy across supporting text documentation and scripts
  install -m644 NOTICE "${pkgdir}/usr/share/java/${pkgname}" || return 1
  install -m644 LICENSE "${pkgdir}/usr/share/java/${pkgname}" || return 1
  install -m644 *.txt "${pkgdir}/usr/share/java/${pkgname}" || return 1
  install -m644 *.html "${pkgdir}/usr/share/java/${pkgname}" || return 1
  install -m755 bin/gradle "${pkgdir}/usr/share/java/${pkgname}/bin" || return 1
  install -m644 init.d/*.* "${pkgdir}/usr/share/java/${pkgname}/init.d" || return 1

  # link gradle script to /usr/bin
  ln -s /usr/share/java/${pkgname}/bin/${pkgname} ${pkgdir}/usr/bin
}

package_gradle-doc() {
  pkgdesc=('A powerful build system for the JVM (documentation and samples)')
  options=('!strip')
  optdepends=('gradle')
  cd "${srcdir}/gradle-${pkgver}"

  # create the necessary directory structure
  mkdir -p "${pkgdir}/usr/share/java/gradle/docs/"
  mkdir -p "${pkgdir}/usr/share/java/gradle/samples/"
  # copy across documentation and samples
  cp --recursive docs/* "${pkgdir}/usr/share/java/gradle/docs/"
  cp --recursive samples/* "${pkgdir}/usr/share/java/gradle/samples/"
}

package_gradle-src() {
  pkgdesc=('A powerful build system for the JVM (sources)')
  options=('!strip')
  optdepends=('gradle')

  cd "${srcdir}/gradle-${pkgver}"
  mkdir -p "${pkgdir}/usr/share/java/gradle/src/"
  cp --recursive src/* "${pkgdir}/usr/share/java/gradle/src/"
}

md5sums=('17295dee02217cbe4f07b0d8bb72c467'
         'd73a375d2796dfe4ec170f2f5af3a0c9')
sha1sums=('f3c307a91d14b4d30973e61b59bdd80e19093f33'
          '07239706341968f2929f412ed3a7b286c1e05b9d')
sha256sums=('b71ab21fa5e91dcc6a4bd723b13403e8610a6e1b4b9d4b314ff477820de00bf9'
            '84294ba7bf75587204e0f46f6e0d001f26b0133f7ecdbaf55cc9d8478dc77caf')
