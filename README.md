## NeoTerm apt repo
### Repo link
```
https://raw.githubusercontent.com/NeoTerm/NeoTerm-repo/main/ stable main
```

### Supported architectures

ARCH    :|: SUPPORTED
--------:|:-------------
ARM     :|: NO
AARCH64 :|: YES
I386    :|: NO
X86-X64 :|: NO

### Mini guide to add/remove/update packages
#### Deps
```
apt install reprepro
```
#### Conf example (Needed to be only once)
* Lets take (aptr) as root dir here (Clean/empty folder)
```
$ nano (aptr)/conf/distributions

Codename: stable
Architectures: aarch64 arm
Components: main
Description: neoterm-repository
```
#### Command
* Here you need to be in (aptr) folder to execute these
```
# Remove all old packages
$ reprepro --ignore=forbiddenchar -V removefilter stable 'Section'

# Add new packages
$ reprepro --ignore=forbiddenchar -S main -P extra includedeb stable ../neoterm-packages/debs/*.deb
```
#### Get all of current package(s) list (Mainly for neoterm-packages)
* Get Packages file from apt repo
```
$ wget https://github.com/NeoTerm/NeoTerm-repo/raw/main/dists/stable/main/binary-aarch64/Packages
```
* Cat packages to file (List)
```
$ grep -ra "Package" >> List
```
* Now open text editor and replace these with nothing
* (Packages:Package: ) and (-static) both need to be replaces with nothing
* Now to sort and make it to oneliner
```
$ cat List | uniq > proper-list

$ cat proper-list | awk '{print}' ORS=' ' > oneliner
```
* End result of it should be good enough for ./build-package.sh but some of these will need cleaning still (Example at the bottom)
```
$ ./build-package.sh package1 package2 package3 and etc
```
