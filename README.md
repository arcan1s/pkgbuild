pkgbuild
========

My Arch AUR PKGBUILD's. At the moment this repository is only for private use
since any package points to git repository over SSH protocol (thus it requires
my private key).

Clone or submodule statuses update
----------------------------------

```
# clone if no repository clones
git clone https://github.com/arcan1s/pkgbuild.git
cd pkgbuild
git submodule update --init
```

Add package
-----------

```
cd pkgbuild
git submodule add ssh+git://aur@aur.archlinux.org/$pkgbase.git/
# some changes here if required (see package update below)
git add $pkgbase
git commit -m 'add $pkgbase'
git push
```

Update package
--------------

```
cd pkgbuild/$pkgbase
vim PKGBUILD
# some changes here
mksrcinfo
git add PKGBUILD .SRCINFO       # newly created (edited) files should be added too
                                # please do not use -A since it will add binaries too
git commit -m 'bump $pkgbase to $pkgver-$pkgrel'
git push
# now update repository if there are no errors
cd ..
git add $pkgbase
git commit -m 'bump $pkgbase to $pkgver-$pkgrel'
git push
```

Force update submodules to AUR state
------------------------------------

```
cd pkgbuild
git submodule foreach git pull origin master
git add -A .                    # or something like this
git commit -m 'bump packages to aur versions'
git push
```
