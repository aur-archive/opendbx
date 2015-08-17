# Maintainer: Leonard de Ruijter <leonard@aur.archlinux.org>
# Contributor: Hubert Kario <hubert@kario.pl>
# Contributor: Artyom Smirnov <smirnoffjr@gmail.com>
pkgname=opendbx
pkgver=1.4.6
pkgrel=1
pkgdesc="Extremely lightweight but extensible database access library written in C."
arch=('i686' 'x86_64')
url="http://www.linuxnetworks.de/doc/index.php/OpenDBX"
license=('LGPL2')
options=(!libtool)
depends=('libfbclient' 'libmariadbclient' 'postgresql-libs' 'sqlite' 'freetds')
source=(http://linuxnetworks.de/opendbx/download/${pkgname}-${pkgver}.tar.gz
        'opendbx.patch')
sha256sums=('2246a03812c7d90f10194ad01c2213a7646e383000a800277c6fb8d2bf81497c'
            '786f9622791de113bfe1ee9fc2fdc42ea4a58d31a006db1dc91ffd7fb8b6deeb')

prepare() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  patch -up1 < "../opendbx.patch"
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  CPPFLAGS=${CPPFLAGS}" -I/usr/include/mysql"\
  ./configure --with-backends="firebird mysql mssql odbc pgsql sqlite3 sqlite3 sybase" \
              --prefix=/usr
  make all -j1
}
check() {
  cd "$srcdir/$pkgname-$pkgver"
  make check
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}/" install
}

# vim:set ts=2 sw=2 et:
