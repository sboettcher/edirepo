# edirepo
A repository to use with opkg on the edison.

To install packages on your edison, edit /etc/opkg/base-feeds.conf and add the line

    src/gz edirepo https://github.com/sboettcher/edirepo/raw/master
    
then run `opkg update`.

## Creating new packages
1. Get opkg-utils from the [yoctoproject git](http://git.yoctoproject.org/clean/cgit.cgi/opkg-utils/), and install with `make install`.
2. Create your package file structure. See [this wiki](http://buffalo.nas-central.org/wiki/Construct_ipkg_packages_%28for_developers%29#Package_structure_.2F_prototype_directory_structure) for some detailed explanation of how this should look.
3. When you have your directory structure, make sure permissions and ownage are correct! For the edison, all files/directories should be owned by root:root! (`chown root:root -R <pkg>`)
4. Run `opkg-build <pkg>` to automatically build the .ipk for the package.
5. Run `opkg-make-index . > Packages` to create the package index.
6. Run `gzip -k Packages`.
7. Update the repo.
