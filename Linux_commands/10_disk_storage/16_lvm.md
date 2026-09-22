## `pvs`

### Purpose

Displays Physical Volumes.

```
sudo pvs
```

Example:

```
PV          VG        PSize    PFree
/dev/sda3   ubuntu-vg  50G      10G
```

---

## `vgs`

### Purpose

Displays Volume Groups.

```
sudo vgs
```

Shows:

- VG name
- total size
- free space
- number of physical volumes
- number of logical volumes

---

## `lvs`

### Purpose

Displays Logical Volumes.

```
sudo lvs
```

More detail:

```
sudo lvs -a
```

---

## `pvdisplay`

Detailed Physical Volume information:

```
sudo pvdisplay
```

---

## `vgdisplay`

Detailed Volume Group information:

```
sudo vgdisplay
```

---

## `lvdisplay`

Detailed Logical Volume information:

```
sudo lvdisplay
```