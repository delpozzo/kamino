# Kamino Changelog

### v1.0.1

- Release Date: 03 April 2019
- Kamino will now wake drives up before performing operations on them. This fixes a bug where in some rare cases the dd command finishes immediately without actually doing anything.
- Removed the `protect_root_filesystem` option from `kamino.config`. This functionality only worked in limited circumstances and wasn't supported on certain Linux distributions and raid setups.

### v1.0.0

- Release Date: 16 January 2019
- Initial release of Kamino.

