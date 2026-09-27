CPU capabilities can be viewed with:

```
lscpu
```

or:

```
grep -m1 '^flags' /proc/cpuinfo
```

You may see flags such as:

```
sse
sse2
avx
avx2
aes
vmx
```

These indicate CPU-supported instruction sets or virtualization features.



# Virtualization Detection

Check:

```
lscpu | grep -i virtualization
```

Intel systems may show:

```
Virtualization: VT-x
```

AMD systems may show:

```
Virtualization: AMD-V
```

CPU flags can also reveal virtualization support:

```
grep -Eo 'vmx|svm' /proc/cpuinfo | sort -u
```