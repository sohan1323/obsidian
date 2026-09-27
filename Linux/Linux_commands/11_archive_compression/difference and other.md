### Archive

```
tar -cf files.tar files/
```

Packages multiple files together.

### Compression

```
gzip file.txt
```

Compresses the file.

### Archive + compression

```
tar -czf files.tar.gz files/
```

First creates an archive, then compresses it with gzip.




Inspect without extracting:

```
tar -tzf backup.tar.gz
```

```
unzip -l backup.zip
```

```
7z l backup.7z
```

Search compressed logs:

```
zgrep -i "password" access.log.gz
```

```
zcat auth.log.gz | grep "Failed password"
```

Find archive files:

```
find / -type f \( -name "*.zip" -o -name "*.tar.gz" -o -name "*.7z" \) 2>/dev/null
```

Extract an archive into a controlled directory:

```
mkdir /tmp/extracted
unzip suspicious.zip -d /tmp/extracted
```