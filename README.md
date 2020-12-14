# IOTA Wallet CLI

Command line interface application for the [IOTA wallet library](https://github.com/iotaledger/wallet.rs).

## Usage

After downloading the CLI, create a new account:

```
$ ./wallet new --node http://node.url:port --alias ALIAS
```

If you already created an account, you can just run the CLI without args to get to the account selector:

```
$ ./wallet
```

Alternatively, you can select the account to use with the `account` command:

```
$ ./wallet account "my first account"
```

To run the CLI from source, install Rust (usually through [Rustup](https://rustup.rs/)) and run the following commands:

```
$ git clone https://github.com/iotaledger/wallet.cli
$ cargo run -- [COMMAND] [OPTIONS]
```

## Commands

The wallet CLI has a set of main commands accesible with `$ ./wallet COMMAND [ARGS]` and a dedicated command list for the account prompt.

### Main commands

#### help [COMMAND]

Prints the CLI help information. If a command is specified, the command's help will be printed.

#### new --node "http://node.url:portNumber" [--alias ALIAS --mnemonic 24_WORD_MNEMONIC_PHRASE]

Creates a new account connecting to the specified node URL. Optionally takes the account alias and 24 word mnemonic phrase.

#### account ALIAS

Selects the account associated with the specified alias.

#### delete ALIAS

Deletes the account associated with the specified alias.

#### sync

Synchronizes all accounts with the Tangle.

#### backup PATH

Backups the wallet database to the specified path.

#### import PATH

Imports the accounts stored on the specified backup path.

### Account prompt commands

#### help [COMMAND]

Prints the CLI help information. If a command is specified, the command's help will be printed.

#### exit

Exits the account prompt.

#### sync

Synchronizes the account with the Tangle.

#### address

Generates a new unused address.

#### balance

Gets the account balance.

#### list-addresses

Lists the account's addresses.

#### list-messages [MESSAGE_ID] [--type TYPE]

Lists the account's messages.
If an id is specified, the query will look for the message associated with that id.
If a type is specified, the messages will be filtered based on it.

- Possible `type` values: "received, "sent", "failed", "unconfirmed" or "value"

#### transfer ADDRESS AMOUNT

Transfer funds from the account to the given Bech32 address.

#### promote [MESSAGE_ID]

Promotes the specified message.

#### reattach [MESSAGE_ID]

Reattaches the specified message.

#### retry [MESSAGE_ID]

Retries (promotes or reattaches) the specified message.

## Caveats

### Database path

By default the database path is `./wallet-cli-database` but you can change this with the `WALLET_DATABASE_PATH` environment variable:

```
$ export WALLET_DATABASE_PATH=/path/to/database # or add it to your .bashrc, .zshrc
$ ./wallet [COMMAND] [OPTIONS]
```
