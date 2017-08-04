## Requirements

- Vagrant
- VirtualBox
- Internet Connection

## Usage

1. Run `vagrant up` inside the directory.
1. Verify the return values with `curl 33.33.33.82`. It should reply with the names web1 and web2 alternating.
1. Log into the loadbalncer VM with `vagrant ssh loadbalancer`.
1. Run `./eZServerMonitor.sh` to check ping and status of SSH and Web service.

