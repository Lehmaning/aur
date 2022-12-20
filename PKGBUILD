# Maintainer: KUMAX <kumax2047@pm.me>

_pkgname=nvml_fix
pkgname=nvml-fix-git
pkgrel=1
pkgver=r35.038fa0c
pkgdesc="A workaround for an annoying bug in nVidia's NVML library."
url=https://github.com/CFSworks/nvml_fix
arch=('x86_64' 'i686')
conflicts=(${pkgname%-git})
provides=(${pkgname%-git})
options=(!ccache)
depends=('nvidia-utils')
makedepends=('git')
license=("custom:Public Domain")
source=("git+${url}.git"
		"nvml-fix-install.hook"
		"80-nvml-fix-upgrade.hook"
		"81-nvml-fix-reapply.hook"
		)
sha256sums=('SKIP'
'40c4d6ed233647fd604cb9e4f030266e5c6a3d1a048b198aa2804411e12cfe39'
'7eaee1f6fedcecb75e04b3f25167fbe4e94bf235c4c6d95228312fbc0c55d3f6'
'51c2e28e88193a8b2435ff23eb4d1818f8cdaaba32f7c2562862fae2223d3a35'
)

pkgver() {
  cd "${srcdir}/${_pkgname}"
  ( set -o pipefail
    git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

build() {
	NVIDIA_VERSION=$(pacman -Q nvidia-utils | awk '{print $2}' | sed  's/-[0-9]$//')
	cd ${srcdir}/${_pkgname}
	make TARGET_VER=$NVIDIA_VERSION libdir=/usr/lib
}
package() {
	install -Dm644 "${srcdir}/${_pkgname}/Makefile" "${pkgdir}/usr/src/nvml-fix-1/Makefile"
	install -Dm644 "${srcdir}/${_pkgname}/empty.c" "${pkgdir}/usr/src/nvml-fix-1/empty.c"
	install -Dm644 "${srcdir}/${_pkgname}/nvml_fix.c" "${pkgdir}/usr/src/nvml-fix-1/nvml_fix.c"
	install -Dm644 "${srcdir}/${_pkgname}/nvml_v9.h" "${pkgdir}/usr/src/nvml-fix-1/nvml_v9.h"
	install -Dm644 "${srcdir}/${_pkgname}/nvml_v3.h" "${pkgdir}/usr/src/nvml-fix-1/nvml_v3.h"
	install -Dm755 "${srcdir}/${_pkgname}/libnvidia-ml.so.1" "${pkgdir}/usr/lib/libnvidia-ml.so.1.fix"
	install -Dm644 "${srcdir}/nvml-fix-install.hook" "${pkgdir}/usr/share/libalpm/hooks/nvml-fix-install.hook"
	install -Dm644 "${srcdir}/80-nvml-fix-upgrade.hook" "${pkgdir}/usr/share/libalpm/hooks/80-nvml-fix-upgrade.hook"
	install -Dm644 "${srcdir}/81-nvml-fix-reapply.hook" "${pkgdir}/usr/share/libalpm/hooks/81-nvml-fix-install.hook"
}
