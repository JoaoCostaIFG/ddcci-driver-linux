# Maintainer: Joao Costa <me@joaocosta.dev>
# Based on ddcci-driver-linux-dkms-git by MaximMaximS <sklenicka dot maxim at gmail dot com>
# Contributor: Ewout van Mansom <ewout@vanmansom.name>
# Contributor: Iwan Timmer <irtimmer@gmail.com>
# Contributor: Porous3247
#
# Personal fork with Linux 7.2+ build fixes:
#   - strncpy -> strscpy (upstream MR !20)
#   - i2c remove callback parent fix (upstream MR !19)

pkgname=ddcci-driver-linux-joaocostaifg-dkms-git
_pkgname=${pkgname%-git}
_reponame=ddcci-driver-linux
pkgver=0.4.5.r11.gb298333
pkgrel=1
epoch=1
pkgdesc="A pair of Linux kernel drivers for DDC/CI monitors (DKMS) - fork with Linux 7.2+ fixes"
arch=('i686' 'x86_64' 'aarch64')
url="https://github.com/JoaoCostaIFG/ddcci-driver-linux/"
license=('GPL2')
depends=('dkms')
makedepends=('git')
# Drop-in replacement for the upstream/AUR packages (keep versions in sync
# with PACKAGE_VERSION in dkms.conf so versioned dependencies are satisfied).
provides=("ddcci-driver-linux=0.4.5" "ddcci-driver-linux-dkms=0.4.5" "ddcci-driver-linux-dkms-git=0.4.5")
conflicts=("ddcci-driver-linux" "ddcci-driver-linux-dkms" "ddcci-driver-linux-dkms-git")
source=("git+https://github.com/JoaoCostaIFG/ddcci-driver-linux.git")
# To build from this local checkout instead of GitHub:
#source=("git+file://${PWD}")
b2sums=('SKIP')

pkgver() {
  cd "$_reponame"
  git describe --long --tags --abbrev=7 | sed 's/\([^-]*-g\)/r\1/;s/-/./g' | sed 's/^v//'
}

package() {
  cd "$_reponame"
  # DKMS requires the source dir name to match the version in dkms.conf,
  # so take it from there instead of guessing from git tags.
  local ver="$(sed -n 's/^PACKAGE_VERSION="\(.*\)"$/\1/p' dkms.conf)"
  local destdir="${pkgdir}/usr/src/ddcci-${ver}"

  install -d "${destdir}"
  cp -aT . "${destdir}"
  rm -rf "${destdir}/.git"
}
