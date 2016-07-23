# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-wstools
pkgname=('python-wstools' 'python2-wstools')
pkgver=0.4.4
_commit=f74298a5b0527382e6482d2354150813e976f12d
pkgrel=1
pkgdesc="WSDL parsing services package for Web Services for Python"
arch=('any')
url="https://github.com/pycontribs/wstools"
license=('custom')
makedepends=('python-setuptools' 'python2-setuptools' 'python-docutils' 'python2-docutils' 'git')
checkdepends=('python-pytest-runner' 'python2-pytest-runner' 'autopep8' 'python2-autopep8')
source=("git+https://github.com/pycontribs/wstools.git#commit=$_commit")
md5sums=('SKIP')

prepare() {
  # pytest-pep8 doesn't work at the moment due to the upstream renaming from pep8 to pycodestyle
  sed -i 's/--pep8//' wstools/setup.cfg
  cp -a wstools{,-py2}
  sed -e 's|#! /usr/bin/env python$|#!/usr/bin/env python2|' \
      -e 's|#!/usr/bin/env python$|#!/usr/bin/env python2|' \
      -i wstools-py2/wstools/{c14n.py,Namespaces.py,XMLSchema.py,Utility.py,__init__.py}
}

build() {
  cd "$srcdir"/wstools
  python setup.py build

  cd "$srcdir"/wstools-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/wstools
  python setup.py test

  cd "$srcdir"/wstools-py2
  python2 setup.py test
}

package_python-wstools() {
  depends=('python-six' 'python-docutils')

  cd wstools
  python setup.py install --root="$pkgdir" --optimize=1

  install -d "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 docs/* "$pkgdir/usr/share/licenses/$pkgname"/
}

package_python2-wstools() {
  depends=('python2-six' 'python2-docutils')

  cd wstools-py2
  python2 setup.py install --root="$pkgdir" --optimize=1

  install -d "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm644 docs/* "$pkgdir/usr/share/licenses/$pkgname"/
}
