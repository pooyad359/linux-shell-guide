# Network

## `curl`

It is used for transferring data to/from a server.

### GET request

Basic get request syntax is:

```bash
curl <url>
```

#### Download a file

It is the same as basic GET request, except we redirect the output to a file instead of stdout.

- To download a file using a url: `curl -O <url>`
- To specify the name of file: `curl <url> -o <filename>` (or `--output`)

### POST request

For POST requests, use `-X POST`:

```bash
curl -X POST <url>
```

### Important Flags for `curl`

- Authentication (`-u` or `--user`): `curl --user username:password <url>`
- Header (`-H`, `--header`): `curl -H 'ContentType: application/json' <url>`
- Data (`-d`, `--data`): `curl -d '<data>' <url>`
  - Data from file: `curl -d @<file path> <url>`
- Custom HTTP Method (e.g., `PUT` request): `curl --request PUT url`
- Cookies (`-b`, `--cookie`): `curl -b <name>=<value> <url>`
  - From file: `curl -b <file> <url>`
- Follow Redirection (`-L`): `curl -L <url>`

## `wget`

Easy-to-use tool for downloading files. To download a file simply use: `wget <url>`.

### Important Flags for `wget`

- `-O`: To specify output file name. `wget -O <filename> <url>`
- `--user` and `--password`: To specify user credentials. `wget --user=<username> --password=<password> <url>`
Examples:

- Download a page and all its resources: `wget --page-requisites --convert-links <url>`

## `netstat`

### Open ports

This command displays open ports and some details about them.

```bash
netstat -nltp
```

### Netstat flags

- `--all`: List all ports
- `--listening`: List all listening ports
- `--tcp`: List listening tcp ports

## Find your public IP

```bash
curl whatismyip.akamai.com
```

## `ping`

- Ping a host: `ping <url>`
- Ping certain number of times: `ping -c <count> <url>`

## `host`

Search for information about an internet host by name of ip.

```bash
host www.google.com
```

### Secure Shell (`ssh`)

ssh (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine.
basic usage is `ssh <username>@<host>`:

```bash
ssh user@192.168.1.12
```

To add private key: `ssh -i <key-file> <username>@<host>`
