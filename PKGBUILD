# Maintainer: Luis Martinez <luis dot martinez at disroot dot org>
# Maintainer: Moon Sungjoon <sumoon at seoulsaram dot org>
# Contributor: Yurii Kolesnykov <root@yurikoles.com>

pkgname=slack-electron
pkgver=4.29.144
pkgrel=1
pkgdesc="Slack Desktop (Beta) for Linux, using the system Electron package"
arch=('x86_64')
url="https://slack.com/downloads/linux"
license=('custom:proprietary')
depends=('electron20')
optdepends=('libappindicator-gtk3: for notification indicator in the status bar on GNOME')
provides=("slack-desktop")
conflicts=("slack-desktop")
source=("$pkgname-$pkgver.deb::https://downloads.slack-edge.com/releases/linux/$pkgver/prod/x64/slack-desktop-$pkgver-amd64.deb"
        'slack.sh')
sha256sums=('a810e780ae1d8c4bd963016a7b6d74e49d8f8bcdb206f6b2fb7647cfb70e3d2b'
            'cda3a8ac300697ff5a5516eb9662e7a4f482894ddd17fdf07abc7027d7de8bbe')

prepare() {
	bsdtar -xf data.tar.xz

	# Enable slack silent mode and fix icon
	sed -ri \
	-e 's|^(Exec=.+/slack)(.+)|\1 -s\2|' \
	-e 's/^Icon=.+slack\.png/Icon=slack/' \
	"usr/share/applications/slack.desktop"
}

package() {
	install -Dv "slack.sh" "$pkgdir/usr/bin/slack"
	install -dv "$pkgdir/usr/lib/slack/"
	cp -av --no-preserve=ownership usr/lib/slack/resources/* "$pkgdir/usr/lib/slack/"
	install -Dvm644 "usr/share/applications/slack.desktop" -t "$pkgdir/usr/share/applications"
	install -Dvm644 "usr/share/pixmaps/slack.png" -t "$pkgdir/usr/share/pixmaps"
	install -Dvm644 "usr/lib/slack/LICENSE" -t "$pkgdir/usr/share/licenses/$pkgname/"
}
