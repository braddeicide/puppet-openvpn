# OpenVPN

[![Build Status](https://travis-ci.org/xaque208/puppet-openvpn.png)](https://travis-ci.org/xaque208/puppet-openvpn)

A Puppet module to manage the OpenVPN client and server.

## Supported Platforms

* Debian
* FreeBSD
* OpenBSD

## Usage

### Server Setup

The configuration for the OpenVPN server can be accomplished using the
`openvpn::server` class.

``` Puppet
class { "openvpn::server":
  server => "10.0.0.0 255.255.255.0",
  route  => [
    "10.0.1.0 255.255.255.0",
    "10.0.2.0 255.255.255.0",
    "10.0.3.0 255.255.255.0",
    ],
  dns => '10.0.0.10',
  crl => 'mysite/crl.pem',
}
```

### Basic Client Setup

Clients can be configured using the `openvpn::client` defined type.  Multiple
connections can be specified if you have multiple locations to connect to.

``` Puppet
openvpn::client { "node_${hostname}_dc1":
  server => "vpn.dc1.example.com",
  cert   => "node_${hostname}";
}

openvpn::client { "node_${hostname}_office":
  server => "vpn.office.example.com",
  cert   => "node_${hostname}";
}
```

### Client Specific Configurations

Clients can have a more specific and static configuration.  For example, if you
wanted to specify the IP address a specific client should use, something like
the following will work for this purpose.

``` Puppet
openvpn::server::csc { "srv1.example.com":
  content => "ifconfig-push 10.0.0.50 10.0.0.51",
}
```

## Future Work

* OSX Client Configuration
* Certificate management (piggyback on puppet?)

