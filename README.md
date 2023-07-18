# Catalyst Fund9 Development Stack

This sets up an environment for developing the Catalyst Fund9 stack.


## Requirements

git
Rust v1.65 toolchain
cargo-make


## Clone the repositories

'''
git clone https://github.com/input-output-hk/chain-libs.git
git clone https://github.com/input-output-hk/chain-wallet-libs.git
git clone https://github.com/input-output-hk/jormungandr.git
git clone https://github.com/input-output-hk/jortestkit.git
git clone https://github.com/input-output-hk/vit-testing.git
git clone https://github.com/input-output-hk/vit-servicing-station.git
'''

Or, if you have write access:

'''
# use catalyst-fund9.1-dev branch
git clone git@github.com:input-output-hk/chain-libs.git
git clone git@github.com:input-output-hk/jormungandr.git
git clone git@github.com:input-output-hk/vit-testing.git
git clone git@github.com:input-output-hk/chain-wallet-libs.git

# use master branch
git clone git@github.com:input-output-hk/jortestkit.git

# use catalyst-fund9 branch
git clone git@github.com:input-output-hk/vit-servicing-station.git
'''

## Checkout `catalyst-fund9.1-dev` branches

At least jormungandr, chain-libs, and vit-testing have them.

jortestkit uses master.


## To build the stack

'''
cargo make build-all
'''

## To install the stack

'''
cargo make install-all
'''


## Example: to run `vitup`:

* `proposals` the total number of proposals that can be voted
* `initials` the total number of wallets that are registered for voting

`vitup start quick --log-level debug --private --proposals 200 --slot-duration 2 --slots-in-epoch 1000 --voting-power 500 --initials 500`

This creates a folder called `catalyst` in the current working directory.


## Example: to run `iapyx-load` on the default host (localhost:8080):

`iapyx-load node-only const duration --address http://localhost:8080 --duration 25 --delay 50 --threads 32 -s ./catalyst/quick/wallet_secrets`

## Example: to run `iapyx-load` with mitmproxy (localhost:9090)

In one terminal:

```
mitmproxy --listen-port 9090 --mode reverse:http://0.0.0.0:8080
```

You can use mitmproxy, mitmweb, or, mitmdump.

In another terminal:

```
iapyx-load node-only const duration --address http://localhost:9090 --duration 25 --delay 50 --threads 32 -s ./catalyst/quick/wallet_secrets
```
