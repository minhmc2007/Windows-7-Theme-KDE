# Maintainer: Your Name <quangminh21072010@gmail.com>
pkgname=windows-7-theme
pkgver=1.0
pkgrel=1
pkgdesc="Windows 7/10 Look and Feel transformation pack (Auto-applies configs)"
arch=('any')
url="https://github.com/minhmc2007/Windows-7-Theme-KDE"
license=('custom')
depends=('plasma-desktop' 'kwin' 'dolphin')
makedepends=('unzip' 'zip' 'imagemagick')
install=windows-7-theme.install

# Skip checksums for local building
source=(
    "file://Lock Widgets.desktop"
    "file://Unlock Widgets.desktop"
    "file://Win 7 Splash Fix.desktop"
    "file://Se7enAero.zip"
)
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP')

prepare() {
    msg2 "Preparing icon archives..."
    cd "$startdir"
    
    # Merge the split zip for We10X if it exists
    if [ -f "cursors-icons/We10X.zip" ]; then
        zip -s 0 "cursors-icons/We10X.zip" --out "cursors-icons/We10X-unsplit.zip"
    fi
}

package() {
    cd "$startdir"

    msg2 "Installing Wallpapers..."
    install -d "$pkgdir/usr/share/wallpapers"
    cp -r wallpaper/* "$pkgdir/usr/share/wallpapers/"

    msg2 "Installing Icons and Cursors..."
    install -d "$pkgdir/usr/share/icons"
    install -m644 cursors-icons/win7startorb.png "$pkgdir/usr/share/icons/"
    
    unzip -q -o cursors-icons/Windows-7.zip -d "$pkgdir/usr/share/icons/"
    
    if[ -f "cursors-icons/We10X-unsplit.zip" ]; then
        unzip -q -o "cursors-icons/We10X-unsplit.zip" -d "$pkgdir/usr/share/icons/"
    fi
    
    tar xf cursors-icons/Win-8.1-NS.tar.gz --directory "$pkgdir/usr/share/icons/"
    tar xf cursors-icons/Win-8.1-S.tar.gz --directory "$pkgdir/usr/share/icons/"

    msg2 "Installing Desktop Themes..."
    install -d "$pkgdir/usr/share/plasma/desktoptheme"
    cp -r desktopthemes/* "$pkgdir/usr/share/plasma/desktoptheme/"

    msg2 "Installing Aurorae Themes..."
    install -d "$pkgdir/usr/share/aurorae/themes"
    unzip -q -o Se7enAero.zip -d "$pkgdir/usr/share/aurorae/themes/"

    msg2 "Installing GTK Themes..."
    install -d "$pkgdir/usr/share/themes"
    cp -r gtktheme/* "$pkgdir/usr/share/themes/"

    msg2 "Installing Splash Screens..."
    install -d "$pkgdir/usr/share/plasma/look-and-feel"
    cp -r splashtheme/* "$pkgdir/usr/share/plasma/look-and-feel/"
    install -Dm644 "splashtheme/org.Win7.desktop/contents/splash/images/background-logon-default-windows-7.png" \
        "$pkgdir/usr/share/plasma/look-and-feel/org.Win7.desktop/contents/splash/images/background.png"

    msg2 "Installing Helper Applications..."
    install -d "$pkgdir/usr/share/applications"
    install -m644 "Lock Widgets.desktop" "$pkgdir/usr/share/applications/"
    install -m644 "Unlock Widgets.desktop" "$pkgdir/usr/share/applications/"
    install -m644 "Win 7 Splash Fix.desktop" "$pkgdir/usr/share/applications/"

    msg2 "Installing Fonts..."
    install -d "$pkgdir/usr/share/fonts/windows7"
    cp -r sevenfonts/* "$pkgdir/usr/share/fonts/windows7/"

    msg2 "Staging Configs for Auto-Apply..."
    #  place these in a temporary system folder so the .install script can move them to /home and SDDM
    install -d "$pkgdir/usr/share/$pkgname/presets"
    cp -r presets/* "$pkgdir/usr/share/$pkgname/presets/"
    
    install -d "$pkgdir/usr/share/$pkgname/sddmsettings"
    cp -r sddmsettings/* "$pkgdir/usr/share/$pkgname/sddmsettings/"
}
