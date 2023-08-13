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

### `tar` falgs

- `-z`: Compress with gzip
- `-c`: Create an archive
- `-f`: Name of the archive
- `-x`: Extract archive to disk
- `-a`: Auto compress. Based on archive extension select the type of compression, e.g., `.tgz`, `.tar.bz2.uu`, `.zip`, etc.

### TAR + GZIP

We can make `tar` to compress the archive using `gzip` by passing the flag `-z`.

Examples:

- Create tar.gz from multiple files: `tar -czf archive.tar.gz file1 file2`
  > **Same syntax can be used for viewing and extracting .tar.gz files**
- Change directory (temporarily) before compressing the files: `tar -czf archive.tar.gz -C my_directory .`
  > **`-C` or `--directory` changes the directory before compression before compression; hence, when extracting, the directory won't appear.**
