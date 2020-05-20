# MR

## What is MR

MR can help you expose local server to external network. Support both TCP/UDP, of course support HTTP. Keep it **simple**, **stupid**.

### Install MR

Download from [releases](https://github.com/dolfly/mr/releases) or `go get github.com/dolfly/mr/cli/mr`.

### Server

    $ mr server -l :9999 -p password

    # Only allow partial ports, and set password on each port
    $ mr server -l :9999 -P '5678 password' -P '6789 password1'

### Client

    # Local server is 127.0.0.1:1234, expect to expose: server_address:5678
    $ mr client -s server_address:port -p password -P 5678 -c 127.0.0.1:1234

    # Local web root is /path/to/www, expect to expose: server_address:5678
    $ mr client -s server_address:port -p password -P 5678 --clientDirectory /path/to/www

### Example

#### Access local HTTP server

    $ mr client -s server_address:port -p password -P 5678 -c 127.0.0.1:8080

    # then
    Your HTTP server in external network is: server_address:5678

#### SSH into local computer

    $ mr client -s server_address:port -p password -P 5678 -c 127.0.0.1:22

    # then
    $ ssh -oPort=5678 user@server_address

#### Access local DNS server

    $ mr client -s server_address:port -p password -P 5678 -c 127.0.0.1:53

    # then
    Your DNS server in external network is: server_address:5678

    $ dig github.com @server_address -p 5678

#### Access your local directory via HTTP

    $ mr client -s server_address:port -p password -P 5678 --clientDirectory /path/to/www

    # then
    A HTTP server in external network is: server_address:5678

#### Any TCP-based/UDP-based ideas you think of

...

## Contributing

Please read [CONTRIBUTING.md](https://github.com/dolfly/mr/blob/master/.github/CONTRIBUTING.md) first