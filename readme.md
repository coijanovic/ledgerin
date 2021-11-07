# What is ledgerinput?

[ledger-cli](https://ledger-cli.org) is great. It offers a powerful double-entry accounting system with all data in a plain text file.
But its reliance on the command line make it not very accessible for "normal" people. This is where ledgerweb comes in: It provides an easy to use web-interface for adding entries to your ledger-file.

# What is the intended use-case for ledgerweb?

ledgerinput is intended to be run as a local website (only accessible from within your home network) on a Raspberry Pi or something similar.

# Install (Podman/Docker)

1. Build the container: `podman build -t ledgerin .` (in the repo's main folder)
2. Run the container: `podman run -d --net=host -v /path/to/ledgerfile/:/data/:Z ledgerweb`
3. You may need to adjust your firewall settings to open the specified port

# Install (Direct)

You can also use ledgerinput without docker.
In that case, take the following steps:

1. Setup `python3` with the following packages:
    - `flask`
    - `subprocess`
    - `pyyaml`
3. Install `ledger`
4. Clone this repository
5. Customize your ledgerweb-instance by creating your own `config.yaml` file in the ledgerweb folder (see ch. config)
6. Run the server with `python3 /path/to/ledgerin/ledgerin.py`

# Config

The configuration of ledgerweb is done in a [yaml](https://yaml.org) file. 
Please create the file `config.yaml` for your own configuration. See `defaultconfig.yaml` for all available options and syntax.

Note: The config-file is only parsed on startup. If you change your configuration, you have to stop flask (`Ctrl-C`) and start it again for your changes to be effective.j


| Key        | Explanation                                                                                    |
|------------|------------------------------------------------------------------------------------------------|
| hostip     | ip address used by flask, should be the ip of your server                                      |
| hostport   | port used by flask, use 80 for (local) deployment                                              |
| ledgerfile | path to your ledger file |
| currency   | currency used in ledger file                                                                   |
| accounts   | a list of commonly used accounts (e.g. `Assets:Checking`) to be used as data for auto-complete |
| favs       | often used transactions, with `from` and `to`-account
