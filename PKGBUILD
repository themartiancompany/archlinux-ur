# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>

# shellcheck disable=SC2034
_pkg="archiso"
_variant="persistent"
_distro="archlinux"
_pkgbase="${_pkg}-profiles"
profile="ereleng"
pkgname="${_distro}"
pkgver="$(date +%Y.%m.%d)"
pkgrel=1
pkgdesc="Builds an Archlinux install drive."
arch=('i686'
      'pentium4'
      'x86_64')
license=('AGPL3')
url="https://gitlab.${_distro}.org/tallero/${_pkgbase}"
provides=("${_distro}-${profile}")
makedepends=("${_pkg}-${_variant}-git"
             "cryptsetup-nested-cryptkey"
             # "devtools"
             "fakepkg"
             "git"
             "mkinitcpio-${_pkg}-encryption-git"
             "${_pkgbase}-git"
             "polkit")
checkdepends=('shellcheck')
source=("git+${url}")
sha256sums=('SKIP')

# shellcheck disable=SC2154
package() {
  local _dest="${pkgdir}/usr/share/${_distro}"
  local _iso="${pkgname}-${pkgver}-x86_64.iso"
  local _profile="${srcdir}/${_pkgbase}/${profile}"
  local _build_repo="${srcdir}/${_pkgbase}/.gitlab/ci/build_repo.sh"
  cp -r "/usr/share/${_pkgbase}/${profile}" "${_profile}"
  cd "${_profile}" || exit
  mkdir -p work
  "${_build_repo} fakepkg"
  install -d -m 0755 -- "${_dest}"
  pkexec mkarchiso -v \
	           -o "${_dest}" \
		   -w "${_profile}/work" \
                      "${_profile}"
  mv "${_dest}/${_iso}" "${_dest}/${pkgname}-x86_64.iso"
}
