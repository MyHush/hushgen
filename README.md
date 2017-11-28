# HUSHgen

Offline BIP32 HD wallet and vanity address generator for Hush.

Currently returns the first address associated with m/0'/0/0 (hardened key for account 0/external account)

##Pre-requisites
* Golang 1.7.3 (altought lower versions may work)
* Git

##Build
~~~~
go get -u github.com/TheTrunk/hushgen
go build github.com/TheTrunk/hushgen
go build github.com/TheTrunk/hushgen/hushretrieve
~~~~

##Update an Existing Install
~~~~
go clean github.com/TheTrunk/hushgen
go build github.com/TheTrunk/hushgen
go build github.com/TheTrunk/hushgen/hushretrieve
~~~~

##Usage
To generate a wallet:
~~~~
hushgen [-t] [-n 1]

Options
-t generate testnet addresses
-n number of addresses to generate. Defaults to 1
~~~~

To retrieve addresses generated from your HD wallet:
	
~~~~
hushretrieve -passphrase="<passphrase>" [-t] [-n 1] [-match="t1yourdesiredstring"] [-i]

Options
-t generate testnet addresses	
-n number of addresses to retrieve. Defaults to 1
-match regex string to search for in the address
-i case insensitive string matching
~~~~

eg. Search case insensitive for a vanity address which starts with the string "t1jl"
~~~~
hushretrieve -passphrase="board start difference answer blossom roll powerful million rough butterfly bedroom beam" -match "t1jl" -i
~~~~

Note: The maximum number of addresses that can be searched given a wallet passphrase is restricted to 4,294,967,295 (unsigned 32 bit integer). Depending on your version of Go, case insensitive matching may be slow. https://github.com/golang/go/issues/13288.

To import the private key into Hush:
~~~~
./hush-cli importprivkey "private_key_from_hushgen"
~~~~
Hushd will automatically rescan the blockchain for transactions
