pkgname=mkinitcpio-sd-zfs
pkgver=1.0.3
pkgrel=1
pkgdesc='Compatibility between systemd and ZFS roots'
license=('MIT')
url='https://github.com/jkolo/sd-zfs'
conflicts=('mkinitcpio-sd-zfs-git')
depends=('mkinitcpio' 'systemd')
source=("https://github.com/jkolo/sd-zfs/archive/v${pkgver}.tar.gz")
sha512sums=('1488d13cb8cd9b9c9c2670ee6c77885de73507bcd55183c013a5be313878b08873ce71b07481b00ab13e1e1d7631f4b1b05e8c4fa4ff3223eef640bf39b981b4')
arch=('i686' 'x86_64')

build() {
	cd "sd-zfs-${pkgver}"

	make all
}

package() {
	local install bin
	cd "sd-zfs-${pkgver}"

	# mkinitcpio
	for install in sd-zfs{,-shutdown}; do
		install -Dm644 "mkinitcpio-install/${install}" "${pkgdir}/usr/lib/initcpio/install/${install}"
	done

	# binaries
	install -Dm755 zfs-shutdown "${pkgdir}/usr/lib/systemd/system-shutdown/zfs-shutdown"
	for bin in initrd-zfs-generator mount.initrd_zfs; do
		install -Dm755 "${bin}" "${pkgdir}/usr/lib/mkinitcpio-sd-zfs/${bin}"
	done

	# systemd unit
	install -Dm644 units/mkinitcpio-override.conf "${pkgdir}/usr/lib/systemd/system/mkinitcpio-generate-shutdown-ramfs.service.d/sd-zfs.conf"
}
