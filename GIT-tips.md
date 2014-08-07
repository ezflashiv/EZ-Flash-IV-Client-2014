## Patches

#### Create patch file

Following will create a `my.patch` file with changes you did against branch `master`. This file then can be sent by email to anyone who then could apply it.

```
git format-patch master --stdout > my.patch
```

Following will create a `my.patch` file with changes that were done in 3 commits before commit `fb38e93`:

```
git format-patch -3 fb38e93 --stdout > my.patch
```

Following will create a `my.patch` file with changes in one commit of branch `my-feature`:

```
git format-patch -1 my-feature --stdout > my.patch
```

#### Apply patch

Assuming you have a `my.patch` file with some changes you want to merge in:

```
git am --signoff < my.patch
```

`--signoff` will take care to identify you as a person who merged that patch.