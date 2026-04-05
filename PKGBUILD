# Maintainer: Marco <marco@example.com>
pkgname=mailspring-optimized
pkgver=1.19.1.optimized
pkgrel=1
pkgdesc="Mailspring optimized with CPU fix (Local Build)"
arch=('x86_64')
url="https://github.com/Foundry376/Mailspring"
license=('GPL3')
depends=('libxss' 'libsecret' 'nss' 'atk' 'libcups' 'libdrm' 'gtk3' 'alsa-lib' 'libxcb' 'pango' 'mesa')
provides=('mailspring')
conflicts=('mailspring' 'mailspring-bin' 'mailspring-libre')
source=()

package() {
  # This assumes you have already run 'npm run build' in the root directory
  local _src_dir="$srcdir/../app/dist/mailspring-linux-x64"
  
  if [ ! -d "$_src_dir" ]; then
    error "Dist directory not found. Please run 'npm run build' first."
    return 1
  fi

  msg2 "Installing application files..."
  install -dm755 "$pkgdir/usr/lib/mailspring"
  cp -a "$_src_dir/"* "$pkgdir/usr/lib/mailspring/"
  
  msg2 "Creating symbolic link in /usr/bin..."
  install -dm755 "$pkgdir/usr/bin"
  ln -s /usr/lib/mailspring/mailspring "$pkgdir/usr/bin/mailspring"

  msg2 "Installing desktop files and icons..."
  install -dm755 "$pkgdir/usr/share/applications"
  cp "$srcdir/../app/dist/Mailspring.desktop" "$pkgdir/usr/share/applications/mailspring.desktop"
  
  # Install icons
  local _icon_src="$srcdir/../app/build/resources/linux/icons"
  for size in 16 32 64 128 256 512; do
    install -Dm644 "$_icon_src/${size}.png" "$pkgdir/usr/share/icons/hicolor/${size}x${size}/apps/mailspring.png"
  done
}
