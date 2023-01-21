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

- Authentication (`-u` or `--user`): `curl --user username:password`
- Header (`-H`, `--header`): `curl -H 'ContentType: application/json' <url>`
- Data (`-d`, `--data`): `curl -d '<data>' <url>`
  - Data from file: `curl -d @<file path> <url>`
- Custom HTTP Method (e.g., `PUT` request): `curl --request PUT url`

## `netstat`

### Open ports

This command displays open ports and some details about them.

```bash
netstat -nltp
```

## Find your public IP

```bash
curl whatismyip.akamai.com
```

## `ping`

- Ping a host: `ping <url>`
- Ping certain number of times: `ping -c <count> <url>`

- [ ] `ssh`
- [ ] `put`
- [ ] `get`
- [ ] `quit`
- [ ] `ping`
- [ ] `netstat`
