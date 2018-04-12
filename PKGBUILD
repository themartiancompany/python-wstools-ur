# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-wstools
pkgname=('python-wstools' 'python2-wstools')
pkgver=0.4.6
pkgrel=1
pkgdesc="WSDL parsing services package for Web Services for Python"
arch=('any')
url="https://github.com/pycontribs/wstools"
license=('custom')
makedepends=('python-pbr' 'python2-pbr' 'python-setuptools' 'python2-setuptools')
checkdepends=('python-pytest-runner' 'python2-pytest-runner' 'autopep8' 'python2-autopep8'
              'python-hacking' 'python2-hacking' 'python-pytest-cov' 'python2-pytest-cov')
source=("$pkgbase-$pkgver.tar.gz::https://github.com/pycontribs/wstools/archive/$pkgver.tar.gz")
sha512sums=('23d815ec7f58d30fdcefdb4bd7db544d61ecd6eed39666b09ad857ce9e6d8ccc148a3419698cab8dbc9d6d61fbd498de9c2afa12fc2c9aef47e2a94f687c276d')

prepare() {
  cp -a wstools-$pkgver{,-py2}
  sed -e 's|#! /usr/bin/env python$|#!/usr/bin/env python2|' \
      -e 's|#!/usr/bin/env python$|#!/usr/bin/env python2|' \
      -i wstools-$pkgver-py2/wstools/{c14n.py,Namespaces.py,XMLSchema.py,Utility.py,__init__.py}

  export PBR_VERSION=$pkgver
}

build() {
  cd "$srcdir"/wstools-$pkgver
  python setup.py build

  cd "$srcdir"/wstools-$pkgver-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/wstools-$pkgver
  python setup.py test

  cd "$srcdir"/wstools-$pkgver-py2
  python2 setup.py test
}

package_python-wstools() {
  depends=('python-six' 'python-setuptools')

  cd wstools-$pkgver
  python setup.py install --root="$pkgdir" --optimize=1

  install -d "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 docs/* "$pkgdir/usr/share/licenses/$pkgname"/
}

package_python2-wstools() {
  depends=('python2-six' 'python2-setuptools')

  cd wstools-$pkgver-py2
  python2 setup.py install --root="$pkgdir" --optimize=1

  install -d "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 docs/* "$pkgdir/usr/share/licenses/$pkgname"/
}
