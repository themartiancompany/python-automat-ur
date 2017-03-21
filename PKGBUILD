# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-automat
pkgname=('python-automat' 'python2-automat')
pkgver=0.5.0
pkgrel=1
arch=('any')
license=('MIT')
pkgdesc="Self-service finite-state machines for the programmer on the go."
url="https://github.com/glyph/automat"
makedepends=('python-setuptools-scm' 'python2-setuptools-scm' 'm2r' 'python2-m2r' 'python-attrs'
             'python2-attrs')
checkdepends=('python-pytest-runner' 'python2-pytest-runner')
source=("$pkgbase-$pkgver.tar.gz::https://github.com/glyph/automat/archive/v$pkgver.tar.gz")
sha512sums=('b0d6a290d83c8d1ad9a798e172e0c21dfa80c692ac469286b51cffefd2a9b93475faf55efb60553814603c4be574b5f5d1835c753888bf5ae8cd448fd06cdb1c')

prepare() {
  cp -a automat-$pkgver{,-py2}

  # Set version for setuptools_scm
  export SETUPTOOLS_SCM_PRETEND_VERSION=$pkgver
}

build() {
  cd "$srcdir"/automat-$pkgver
  python setup.py build

  cd "$srcdir"/automat-$pkgver-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/automat-$pkgver
  python setup.py pytest

  cd "$srcdir"/automat-$pkgver-py2
  python2 setup.py pytest
}

package_python-automat() {
  depends=('python-attrs' 'python-setuptools')

  cd automat-$pkgver
  python setup.py install --root="$pkgdir" --optimize=1
  install -D -m644 LICENSE "$pkgdir"/usr/share/licenses/python-automat/LICENSE
}

package_python2-automat() {
  depends=('python2-attrs' 'python2-setuptools')

  cd automat-$pkgver-py2
  python2 setup.py install --root="$pkgdir" --optimize=1
  install -D -m644 LICENSE "$pkgdir"/usr/share/licenses/python2-automat/LICENSE

  mv "$pkgdir"/usr/bin/automat-visualize{,2}
}
