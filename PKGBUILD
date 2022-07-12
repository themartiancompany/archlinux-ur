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

# shellcheck disable=SC2154
package() {
  local _pkg_path="/usr/share/${_pkg}"
  local _pkg_lib_path="/usr/lib/${_pkg}"
  local _dest="${pkgdir}/${_pkg_path}"
  local _iso="${pkgname}-${pkgver}-x86_64.iso"
  local _profile="${srcdir}/${profile}"
  local _build_repo="${_pkg_lib_path}/build_repo.sh"
  cp -r "${_pkg_path}/configs/${profile}" "${_profile}"
  cd "${_profile}" || exit
  mkdir -p work
  mkarchisorepo "fakepkg" "packages.extra"
  install -d -m 0755 -- "${_dest}"
  pkexec mkarchiso -v \
	           -o "${_dest}" \
		   -w "${_profile}/work" \
                      "${_profile}"
  mv "${_dest}/${_iso}" "${_dest}/${pkgname}-x86_64.iso"
}
