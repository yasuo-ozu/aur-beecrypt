# Maintainer: Jaroslav Lichtblau <dragonlord@aur.archlinux.org>

pkgname=beecrypt
pkgver=4.2.1
pkgrel=5
pkgdesc="A strong and fast cryptography toolkit"
arch=('i686' 'x86_64')
url="http://beecrypt.sourceforge.net/"
license=('LGPL')
depends=('icu')
makedepends=('python2')
options=('!libtool')
source=(http://downloads.sourceforge.net/sourceforge/$pkgname/$pkgname-$pkgver.tar.gz)
sha256sums=('286f1f56080d1a6b1d024003a5fa2158f4ff82cae0c6829d3c476a4b5898c55d')

build() {
  cd "${srcdir}"/$pkgname-$pkgver

  CXXFLAGS=-fpermissive
  ./configure --prefix=/usr --sysconfdir=/etc --without-java --disable-openmp --with-python=python2
  for fname in "include/beecrypt/c++/lang/String.h" "c++/lang/String.cxx" "c++/util/Date.cxx" "c++/lang/Integer.cxx"  "c++/lang/Long.cxx" "c++/crypto/Cipher.cxx"; do
	  sed -i -e 's/\(namespace .*\)$/\1using namespace icu;/' "$fname"
  done
  #sed -i -e 's/\<UnicodeString\>/icu::UnicodeString/g' include/beecrypt/c++/lang/String.h
  #sed -i -e 's/\<UnicodeString\>/icu::UnicodeString/g' c++/lang/String.cxx 
  #sed -i -e 's/\<UnicodeString\>/icu::UnicodeString/g' c++/util/Date.cxx 
  #sed -i -e 's/\<DateFormat\>/icu::DateFormat/g' c++/util/Date.cxx 
  #sed -i -e '30i using namespace icu_61;' c++/lang/Integer.cxx
  #sed -i -e '30i using namespace icu_61;' c++/lang/Long.cxx
  make
}

package() {
  cd "${srcdir}"/$pkgname-$pkgver

  make DESTDIR="${pkgdir}" install
}

