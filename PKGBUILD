# Maintainer: KUMAX <kumax2048@pm.me>

_name=ddns
pkgname=python-ddns
pkgrel=1
pkgver=2.10.3
pkgdesc="Automatically update DNS records to dynamic local IP."
url=https://pypi.org/project/ddns
arch=('any')
license=("MIT")
provides=("ddns")
conflicts=("ddns" "newfuture-ddns-bin")
makedepends=('python-pip' 'python-installer')
source=(
	"https://files.pythonhosted.org/packages/py2.py3/${_name::1}/$_name/${_name//-/_}-$pkgver-py2.py3-none-any.whl"
	"newfuture_ddns.service"
	"newfuture_ddns.timer"
	"config.json"
)
sha256sums=(
"ef84efaf305d656400eca8a924754d9d31b28378f96b2704b1f3c162de609d5a"
"11a427cc3d3a8a4c5e1bbcaba8c94dd9265a6b4c4f53f16d694d83ff92514078"
"1e084c5349449289129006b21294699ec34122050ada92be81e682631a60f159"
"aab0eb4c02ab5fa20f1b6c2f66542358ee18ebbb0a60ec2c60e6371844c48d73"
)
makedepends=(python-build python-installer python-wheel)
install=$pkgname.install
#backup=("etc/ddns/config.json" "usr/lib/systemd/system/newfuture_ddns.service" "usr/lib/systemd/system/newfuture_ddns.timer")
backup=("etc/ddns/config.json")

package() {
	python -m installer --destdir="$pkgdir" *.whl
    install -Dm644 newfuture_ddns.service  "${pkgdir}/usr/lib/systemd/system/newfuture_ddns.service"
    install -Dm644 newfuture_ddns.timer "${pkgdir}/usr/lib/systemd/system/newfuture_ddns.timer";
    install -Dm644 config.json "${pkgdir}/etc/ddns/config.json";
}
