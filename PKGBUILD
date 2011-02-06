#Maintainer kfgz <kfgz at interia pl>

pkgname=adjtimex
pkgver=1.29
pkgrel=2.1
arch=('i686' 'x86_64')
pkgdesc="Displays or sets the kernel time variable"
url="http://packages.qa.debian.org/a/adjtimex.html"
license=('other')
source=(ftp://ftp.debian.org/debian/pool/main/a/${pkgname}/${pkgname}_${pkgver}.orig.tar.gz
        ftp://ftp.debian.org/debian/pool/main/a/${pkgname}/${pkgname}_${pkgver}-${pkgrel}.diff.gz
        ${pkgname})
install=('adjtimex.install')
md5sums=('7ff7731baf829fdf6ad9af963a526cda'
         '7972df0bb37b6e203c2045478c2e016f'
         'e5862c394d35f4eceb0e640c78a3c6de')
         
build() {
  sed -i "s/${pkgname}-${pkgver}/src\/${pkgname}-${pkgver}/g" \
  ${srcdir}/${pkgname}_${pkgver}-${pkgrel}.diff
  patch -Np1 -i ${srcdir}/${pkgname}_${pkgver}-${pkgrel}.diff
  
  cd ${srcdir}/${pkgname}-${pkgver}
  install -dm755 \
  ${pkgdir}/{etc/rc.d,sbin,usr/{sbin,share/{licenses/${pkgname},doc/${pkgname}}}}
  ./configure --prefix=${pkgdir}/usr
  make
  make bindir=${pkgdir}/sbin install
  install -m644 ChangeLog ${pkgdir}/usr/share/doc/${pkgname}/changelog.txt
  install -m644 README ${pkgdir}/usr/share/doc/${pkgname}/readme.txt
  
  cd debian
  sed -i "s/init.d/rc.d/g" adjtimexconfig
  sed -i "s/init.d/rc.d/g" adjtimexconfig.8
  install -m755 adjtimexconfig ${pkgdir}/usr/sbin
  install -m755 ${srcdir}/${pkgname} ${pkgdir}/etc/rc.d
  install -m644 copyright ${pkgdir}/usr/share/licenses/${pkgname}
  install -m644 adjtimexconfig.8 ${pkgdir}/usr/share/man/man8
}
