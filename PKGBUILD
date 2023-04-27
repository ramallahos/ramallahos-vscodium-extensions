# Maintainer: Safwan Nayeem Yousuf <safwannayeemyousuf.com>
pkgname=ramallahos-vscodium-extensions
pkgver=20230427
pkgrel=1
pkgdesc="Vscodium extensions for RamallahOS"
arch=('any')
url="https://github.com/ramallahos/$pkgname"
license=('GPL3')
depends=('vscodium' 'lz4' 'tar')
makedepends=('coreutils')

pkgver() {
  date +%Y%m%d
}

data=$( curl https://github.com/ramallahos/ramallahos-repo/tree/main/x86_64 | grep ".tar.zst" | grep $pkgname | awk '{ print $NF }' | awk -F ">" '{ print $2 }' | awk -F "." '{ print $1 }' )
uppkgverdate=$( echo $data | awk -F "-" '{ print $2}' )
uppkgrel=$( echo $data | awk -F "-" '{ print $3 }' )

if [ "$pkgverdate" == "$(date +%Y%m%d)" ];
then
    pkgrel=$( echo "$uppkgrel + 1 " | bc )
else
    pkgrel=1
fi


prepare() {
  [ -d "$pkgname" ] && rm -rf $pkgname
  git clone $url.git
  cd "$pkgname"
  lz4 -d .vscode-oss.lz4 -c | tar xvf -
}

package() {
    cd "$pkgname"
    install -d "${pkgdir}/etc/skel/.vscode-oss"
    cp -rf .vscode-oss "${pkgdir}/etc/skel/"
}


# tar cvf - folderABC | lz4 > folderABC.tar.lz4

# lz4 -d folderABC.tar.lz4 -c | tar xvf -
