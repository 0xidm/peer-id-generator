# IPFS / IPNS peer ID generator

This tool generates IPFS public and private keypair until it finds public key
which contains required substring. Keys are stored in local directory. If you
like one of them, you can move it to ~/.ipfs/keystore/ to use it with IPFS.

## Installation

Install the 0xidm fork of the [meehow repo](https://github.com/meehow/peer-id-generator):

```
go install github.com/0xidm/peer-id-generator
```

If your version is too old for that method to work, try the following:

```
git clone https://github.com/0xidm/peer-id-generator
cd peer-id-generator
go build
go install
```

## Usage

➜  ~ peer-id-generator **dupa**

12D3KooWDpLVwxMacesha42m**dupa**3H8jU7bbJdAmsMD7iPjzrkfK

12D3KooWLhGVro7Ks**DUPa**4FX3LpWC61xACoj7AEZg5wmz6VqDGJ9

12D3KooWMJm**DUPA**tjcaHo8LARo5VHQ5uSxrt8Mdi5fytiRnnfD2f

^C

➜  ~ cp 12D3KooWMJm**DUPA**tjcaHo8LARo5VHQ5uSxrt8Mdi5fytiRnnfD2f ~/.ipfs/keystore/dupa

➜  ~ ipfs name publish --key=dupa {ipfs-path}

Published to 12D3KooWMJm**DUPA**tjcaHo8LARo5VHQ5uSxrt8Mdi5fytiRnnfD2f: {ipfs-path}

## Examples

In [examples](examples) you can find key pairs which contain word "funny"
at the end of Peer ID. They are just for demonstration purposes.
Please consider these private keys as already leaked.

## Benchmarks

This tool is using [Ed25519](https://godoc.org/golang.org/x/crypto/ed25519)
algorithm because it is able to generate keys **2500 times faster**
than [RSA](https://godoc.org/crypto/rsa) and both can work with IPFS.

> *note from idm:*
> This 0xidm fork makes trivial changes that should not affect performance.
> The original code by meehow has the following benchmark profile:

```
goos: linux
goarch: amd64
pkg: github.com/meehow/peer-id-generator
BenchmarkRSA-4       	      10	 162383811 ns/op
BenchmarkEd25519-4   	   20000	     64165 ns/op
PASS
ok  	github.com/meehow/peer-id-generator	4.384s
```
