# Maintainer: Luis Martinez <luis dot martinez at disroot dot org>
# Contributor: Yurii Kolesnykov <root@yurikoles.com>

pkgname=slack-electron
pkgver=4.23.0
pkgrel=1
pkgdesc="Slack Desktop (Beta) for Linux, using the system Electron package"
arch=('x86_64')
url="https://slack.com/downloads"
license=('custom:proprietary')
depends=('electron')
optdepends=('libappindicator-gtk3: for notification indicator in the status bar on GNOME')
provides=("slack-desktop")
conflicts=("slack-desktop")
source=("https://downloads.slack-edge.com/releases/linux/$pkgver/prod/x64/slack-desktop-$pkgver-amd64.deb"
        'slack.sh')
sha256sums=('3a823be14d9aaea2ef565ac6c3fc62580a10775bcc1eadcc62c3256999ea59f3'
            '4db11d083626a561129ca40e9cce7cc613c42223f138bb0136c62064c57471fd')

prepare() {
	bsdtar -xf data.tar.xz

	# Enable slack silent mode and fix icon
	sed -ri \
	-e 's|^(Exec=.+/slack)(.+)|\1 -s\2|' \
	-e 's/^Icon=.+slack\.png/Icon=slack/' \
	"usr/share/applications/slack.desktop"
}

package() {
	install -D "slack.sh" "$pkgdir/usr/bin/slack"

	install -d "$pkgdir/usr/lib/slack/"
	cp -a --no-preserve=ownership usr/lib/slack/resources/* "$pkgdir/usr/lib/slack/"

	install -Dm644 "usr/share/applications/slack.desktop" -t "$pkgdir/usr/share/applications"
	install -Dm644 "usr/share/pixmaps/slack.png" -t "$pkgdir/usr/share/pixmaps"
	install -Dm644 "usr/lib/slack/LICENSE" -t "$pkgdir/usr/share/licenses/$pkgname/"
}
