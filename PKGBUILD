# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>

# shellcheck disable=SC2034
_pkg="archiso"
_distro="archlinux"
_pkgbase="${_pkg}-profiles"
_profile=ereleng
pkgname="${_distro}"
pkgver="$(date +%Y.%m.%d)"
pkgrel=1
pkgdesc='Builds an Archlinux install drive.'
arch=('any')
license=('AGPL3')
url="https://gitlab.${_distro}.org/tallero/${_pkgbase}"
depends=('archiso-persistent-git'
	 'cryptsetup-nested-cryptkey'
	 'fakepkg'
	 'mkinitcpio-archiso-encryption-git'
         'polkit')
provides=("${_distro}-${profile}")
makedepends=('devtools' 'git')
checkdepends=('shellcheck')
source=("git+${url}")
sha256sums=('SKIP')

# shellcheck disable=SC2154
package() {
  local _dest="${pkgdir}/usr/share/${_distro}"
  local _profile="${srcdir}/${_pkgbase}/${_profile}"
  cd "${_profile}" || exit

  mkdir -p work
  ./build_repo.sh fakepkg
  install -d -m 0755 -- "${_dest}"
  pkexec mkarchiso -v \
	           -o "${_dest}" \
		   -w "${_profile}/work" \
                      "${_profile}"
}
