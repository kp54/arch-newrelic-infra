# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: kp54 <kangpang65@gmail.com>
pkgname=newrelic-infra
pkgver=1.72.9
pkgrel=1
pkgdesc="NewRelic Infrastructure Agent"
arch=('x86_64' 'aarch64')
url="https://newrelic.com/"
license=('LicenseRef-scancode-commercial-license')
depends=('glibc')

source=('tweak-systemd-unit.diff')
source_x86_64=("https://download.newrelic.com/infrastructure_agent/binaries/linux/amd64/newrelic-infra_linux_${pkgver}_amd64.tar.gz")
source_aarch64=("https://download.newrelic.com/infrastructure_agent/binaries/linux/arm64/newrelic-infra_linux_${pkgver}_arm64.tar.gz")

sha256sums=('ca9e683ac8df68d224af4cd20587fbde8b326b2bf742b7f2d4bf5f329bb1dadb')
sha256sums_x86_64=('2a3c1a9a861bc46dc0d501671d966d2237eb67f4882796d1f5245e37fa28f421')
sha256sums_aarch64=('402daa03f864f04387e079730822a1f7d53ce0cde23eb31053dbb067867e0cb8')

prepare() {
  patch -p1 -i tweak-systemd-unit.diff
}

package() {
  install -d "${pkgdir}/etc/newrelic-infra/integrations.d/"
  install -Dm644 "${pkgname}/etc/init_scripts/systemd/newrelic-infra.service" "${pkgdir}/usr/lib/systemd/system/newrelic-infra.service"

  install -Dm644 "${pkgname}/var/db/newrelic-infra/LICENSE.txt" "${pkgdir}/usr/share/licenses/newrelic-infra/LICENSE.txt"
  install -d "${pkgname}/var/db/newrelic-infra/custom-integrations/" "${pkgdir}/var/lib/newrelic-infra/custom-integrations/"
  install -d "${pkgname}/var/db/newrelic-infra/integrations.d/" "${pkgdir}/var/lib/newrelic-infra/integrations.d/"
  install -d "${pkgname}/var/db/newrelic-infra/newrelic-integrations/" "${pkgdir}/var/lib/newrelic-infra/newrelic-integrations/"

  install -d "${pkgname}/var/log/newrelic-infra/"
  install -d "${pkgname}/var/run/newrelic-infra/"

  install -Dm755 "${pkgname}/usr/bin/newrelic-infra" "${pkgdir}/usr/bin/newrelic-infra"
  install -Dm755 "${pkgname}/usr/bin/newrelic-infra-ctl" "${pkgdir}/usr/bin/newrelic-infra-ctl"
  install -Dm755 "${pkgname}/usr/bin/newrelic-infra-service" "${pkgdir}/usr/bin/newrelic-infra-service"
}
