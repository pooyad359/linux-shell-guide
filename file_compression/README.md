# File Compression

## GZIP

`gzip` is a command used for compressing and decompressing files. It compresses a single file at a time. To compress a file to `.gz` format you can use one of the methods below:

### Compress

```bash
gzip -c file.txt > file.txt.gz
```

or

```bash
gzip -k file.txt
```

### Decompress

Use `-d` flag to decompress files.

```bash
gzip -d file.txt.gz
```

You could also use `gunzip` command :

```bash
gunzip file.txt,gz
```

**both `gzip -d` and `gunzip` will remove the compressed file when decompression is completed.**

## TAR

Combines multiple files into a single file.

Examples:

- Create an archive from multiple files: `tar -cf archive.tar file1 file2`
- Create an archive from a directory: `tar -cf archive.tar <directory>`
- Extract files from archive: `tar -xf archive.tar`
- Extract files from archive to a specific directory: `tar -xf archive.tar -C directory`
- View the content of archive: `tar -tf archive.tar`

### TAR + GZIP

We can make `tar` to compress the archive using `gzip` by passing the flag `-z`.

Examples:

- Create tar.gz from multiple files: `tar -czf archive.tar.gz file1 file2`
  > **Same syntax can be used for viewing and extracting .tar.gz files**
