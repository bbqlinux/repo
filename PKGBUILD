# Maintainer: Daniel Hillenbrand <codeworkx@bbqlinux.org>

pkgname=repo
pkgver=1.19
pkgrel=3
pkgdesc="The Multiple Git Repository Tool from the Android Open Source Project"
arch=('any')
url="http://source.android.com/source/git-repo.html"
license=('APACHE')
depends=('git' 'python2')
makedepends=('git')

_gitrepo="https://gerrit.googlesource.com/git-repo"
_gittag="v1.12.2"
_gitbranch="master"
_gitname="repo"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server..."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitrepo $_gitname
    cd "$_gitname"
    git checkout "$_gitbranch"
    cd "$srcdir"
  fi

  msg "GIT checkout done or server timeout"

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"
}

package() {
  cd "$srcdir/$_gitname-build"

  install -D -m 755 repo "$pkgdir/usr/bin/repo"
  install -D -m 644 docs/manifest-format.txt "$pkgdir/usr/share/doc/$pkgname/manifest-format.txt"
} 
