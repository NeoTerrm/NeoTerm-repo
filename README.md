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
nano (aptr)/conf/distributions

Codename: stable
Architectures: aarch64 arm
Components: main
Description: neoterm-repository
```
#### Command
* Here you need to be in (aptr) folder to execute these
```
# Remove all old packages
reprepro --ignore=forbiddenchar -V removefilter stable 'Section'

# Add new packages
reprepro --ignore=forbiddenchar -S main -P extra includedeb stable ../neoterm-packages/debs/*.deb
```
