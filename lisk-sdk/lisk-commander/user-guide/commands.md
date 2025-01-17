# Lisk Commander Reference

- [Account](#account)
  - [account:create](#create-account)
  - [account:get](#get-account)
  - [account:show](#show-account)
- [Block](#block)
  - [block:get](#get-block)
- [Config](#config)
  - [config:show](#show-config)
  - [config:set](#set-config)
- [copyright](#copyright)
- [Delegate](#delegate)
  - [delegate:get](#get-delegate)
  - [delegate:voters](#get-voters-of-a-delegate)
  - [delegate:votes](#get-votes-of-a-delegate)
- [help](#help)
- [Message](#message)
  - [message:decrypt](#decrypt-message)
  - [message:encrypt](#encrypt-message)
  - [message:sign](#sign-message)
  - [message:verify](#verify-message)
- [Node](#node)
  - [node:forging](#forging)
  - [node:get](#get-node)
- [Passphrase](#passphrase)
  - [passphrase:decrypt](#decrypt-passphrase)
  - [passphrase:encrypt](#encrypt-passphrase)
- [Signature](#signature)
  - [signature:broadcast](#broadcast-signature)
  - [signature:create](#create-signature)
- [Transaction](#transaction)
  - [transaction:broadcast](#broadcast-transaction)
  - [transaction:create](#create-transaction)
    - [transaction:create:transfer](#transfer-transaction)
    - [transaction:create:second-passphrase](#second-passphrase-transaction)
    - [transaction:create:delegate](#register-delegate-transaction)
    - [transaction:create:vote](#cast-votes-transaction)
    - [transaction:create:multisignature](#multisignature-account-registration)
  - [transaction:get](#get-transaction)
  - [transaction:sign](#sign-transaction)
  - [transaction:verify](#verify-transaction)
- [warranty](#warranty)

## Account

Commands relating to Lisk accounts.

### Create Account

Returns a randomly-generated mnemonic passphrase with its corresponding public/private key pair and Lisk address.

```bash
USAGE
  $ lisk account:create

OPTIONS
  -j, --[no-]json      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -n, --number=number  [default: 1] Number of accounts to create.

  --[no-]pretty        Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table.
                       You can change the default behaviour in your config.json file.

EXAMPLES
  account:create
  account:create --number=3
```

**Example JSON Output**
```json
{
	"passphrase": "account reform outdoor curtain animal zoo best gain super glue bacon endless",
	"privateKey": "c0554188319a911aec70a6e044cbf69ec0da19269d11e8cd4e2b5ee18afe4402f7425ba1b192e07639a0304531e21117ccc1852279b6ec7c296b18bd95bcc4c3",
	"publicKey": "f7425ba1b192e07639a0304531e21117ccc1852279b6ec7c296b18bd95bcc4c3",
	"address": "9292797545729948557L"
}
```

### Get Account

Gets information about one or several accounts from the blockchain.

```bash
USAGE
  $ lisk account:get ADDRESSES

ARGUMENTS
  ADDRESSES  Comma-separated address(es) to get information about.

OPTIONS
  -j, --[no-]json  Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.

EXAMPLES
  account:get 3520445367460290306L
  account:get 3520445367460290306L,2802325248134221536L
```

**Example JSON Output**
```json
[
	{
		"address": "8004805717140184627L",
		"unconfirmedBalance": "3254116037008",
		"balance": "3254116037008",
		"publicKey": "30c07dbb72b41e3fda9f29e1a4fc0fce893bb00788515a5e6f50b80312e2f483",
		"secondPublicKey": "f7a16edaf7995d522d5e6ac69d7325df76f5883dd084409eb13df8d61c33abfb",
		"delegate": {
			"username": "tschakki",
			"vote": "1372073738324255",
			"rewards": "3190700000000",
			"producedBlocks": 9377,
			"missedBlocks": 905,
			"rank": 94,
			"approval": 10.66,
			"productivity": 91.2
		}
	}
]
```

### Show Account

Shows private account information for a given passphrase.
Displays lisk address, publickey and privatekey that belong to the entered passphrase.

```bash
USAGE
  $ lisk account:show

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLE
  account:show
```

**Example JSON Output**
```json
{
        "privateKey": "a665a45920422f9d417e4867efdc4fb8a04a1f3fff1fa07e998e86f7f7a27ae3a4465fd76c16fcc458448076372abf1912cc5b150663a64dffefe550f96feadd",
        "publicKey": "a4465fd76c16fcc458448076372abf1912cc5b150663a64dffefe550f96feadd",
        "address": "12475940823804898745L"
}
```

## Block

Commands relating to Lisk blocks.

### Get Block

Gets block information from the blockchain.

```bash
USAGE
  $ lisk block:get BLOCKIDS

ARGUMENTS
  BLOCKIDS  Comma-separated block ID(s) to get information about.

OPTIONS
  -j, --[no-]json  Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.

EXAMPLES
  block:get 369374894959871969
  block:get 17108498772892203620,8541428004955961162
```

**Example JSON Output**
```json
[
	{
		"id": "369374894959871969",
		"version": 1,
		"timestamp": 76721330,
		"height": 6587884,
		"numberOfTransactions": 1,
		"totalAmount": "11100000",
		"totalFee": "10000000",
		"reward": "300000000",
		"payloadLength": 117,
		"payloadHash": "76eba40d186274ac79a8a5c2b5d73a5d214acfa1829763f59035d61c43a2ff2d",
		"generatorPublicKey": "279320364fc3edd39b77f1fa29594d442e39220b165956fa729f741150b0dc4d",
		"blockSignature": "6f1448a8b25b427bdc05e46d0383f6f1e0af45319591ad5507deaf298428d7fb16c82b4156dd0a444b0b70ef586bb95eb0853cb90937c980c3b939d1a65d1900",
		"confirmations": 4,
		"totalForged": "310000000",
		"generatorAddress": "8191405714437232748L",
		"previousBlockId": "6777587147545065709"
	}
]
```

## Config

Commands to get and manage configurations for Lisk Commander.

### Show Config

Prints the current configuration.

```bash
USAGE
  $ lisk config:show

OPTIONS
  -j, --[no-]json  Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.

DESCRIPTION
  Prints the current configuration.

EXAMPLE
  config:show
```

**Example JSON Output (default values):**

```
{
	"json": true, // if false, displays output in table format
	"api": {
		"nodes": [], // custom nodes, lisk-commander should connect to
		"network": "main" // main for Mainnet, test for Testnet
	},
	"pretty": false // if true, displays output nicely formatted. Has no effect if json:false
}
```

### Set Config

Sets configuration.

When `api.nodes` is empty, lisk-commander will connect to official Lisk Seed Nodes depending on the network specified in `api.network`.

If `api.nodes` is set to one or multiple nodes, lisk commander will ignore `api.network` and will make all requests to the specified Lisk node.

When multiple nodes are specified, queries will always go to the first listed node. The later nodes serve as a fallback, if query to the first node was not successful.

```bash
USAGE
  $ lisk config:set VARIABLE [VALUES]

OPTIONS
  -j, --[no-]json  Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.

EXAMPLES
  config:set pretty true
  config:set api.network test 
  config:set api.nodes https://127.0.0.1:4000,http://mynode.com:7000
```

**Example JSON Output**
```json
{
	"message": "Successfully set pretty to true."
}
```

## Copyright

Displays copyright notice.

```
USAGE
  $ lisk copyright

OPTIONS
  -j, --[no-]json  Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.

EXAMPLE
  copyright
```

## Delegate

Commands relating to Lisk delegates.

### Get Delegate

Gets delegate information from the blockchain.

```
USAGE
  $ lisk delegate:get USERNAMES

ARGUMENTS
  USERNAMES  Comma-separated username(s) to get information about.

OPTIONS
  -j, --[no-]json  Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.

DESCRIPTION
  Gets delegate information from the blockchain.

EXAMPLES
  delegate:get lightcurve
  delegate:get lightcurve,4miners.net
```

**Example JSON Output**
```json
[
	{
		"rewards": "3209000000000",
		"vote": "1372446779413292",
		"producedBlocks": 9437,
		"missedBlocks": 905,
		"username": "tschakki",
		"rank": 94,
		"approval": 10.66,
		"productivity": 91.25,
		"account": {
			"address": "8004805717140184627L",
			"publicKey": "30c07dbb72b41e3fda9f29e1a4fc0fce893bb00788515a5e6f50b80312e2f483",
			"secondPublicKey": "f7a16edaf7995d522d5e6ac69d7325df76f5883dd084409eb13df8d61c33abfb"
		}
	}
]
```

## Get voters of a delegate

Gets voters information for given delegate(s) from the blockchain.

```
USAGE
  $ lisk delegate:voters USERNAMES

ARGUMENTS
  USERNAMES  Comma-separated username(s) to get information about.

OPTIONS
  --limit          Limits the returned voters array by specified integer amount. Maximum is 100.

  --offset         Offsets the returned voters array by specified integer amount.

  --sort           Sorts the returned voters array. Sort type must be one of `publicKey:asc`, `publicKey:desc`, `balance:asc`, `balance:desc`, `username:asc` or `username:desc`.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.


DESCRIPTION
  Gets voters information for given delegate(s) from the blockchain.

EXAMPLES
  delegate:voters lightcurve
  delegate:voters lightcurve,4miners.net
  delegate:voters lightcurve,4miners.net --limit 20 --offset 5 --sort publicKey:asc --pretty
```

## Get votes of a delegate

Gets votes information for given delegate(s) from the blockchain.

```
USAGE
  $ lisk delegate:votes ADDRESSES

ARGUMENTS
  ADDRESSES  Comma-separated address(es) to get information about.

OPTIONS
  --limit          Limits the returned voters array by specified integer amount. Maximum is 100.

  --offset         Offsets the returned voters array by specified integer amount.

  --sort           Sorts the returned voters array. Sort type must be one of `balance:asc`, `balance:desc`, `username:asc` or `username:desc`.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.


DESCRIPTION
  Gets voting information for given delegate(s) from the blockchain.

EXAMPLES
  delegate:votes 8004805717140184627L
  delegate:votes 13133549779353512613L,16010222169256538112L
  delegate:votes 8004805717140184627L,8820447240686843261L --limit 20 --offset 5 --sort balance:asc --pretty
```

## Help

Displays command reference.

```bash
USAGE
  $ lisk help [COMMAND]

ARGUMENTS
  COMMAND  command to show help for

OPTIONS
  --all  see all commands in CLI
```

## Message

Commands relating to user messages.

### Decrypt Message

Decrypts a previously encrypted message from a given sender public key for a known nonce using your secret passphrase.

> **Important:** Since the secret passphrase is a sensitive input, it can be provided using one of the available methods described in the [Sensitive Inputs section](sensitive-inputs.md). 
> The encrypted message can be provided either directly as an argument, or by specifying a source with the --message option. 
> If both the secret passphrase and the encrypted message are provided via stdin, the secret passphrase must be given in the first line and the encrypted message must be given in the subsequent lines.

```bash
USAGE
  $ lisk message:decrypt SENDERPUBLICKEY NONCE [MESSAGE]

ARGUMENTS
  SENDERPUBLICKEY  Public key of the sender of the message.
  NONCE            Nonce used during encryption.
  MESSAGE          Encrypted message.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -m, --message=message
      Specifies a source for providing a message to the command. If a string is provided directly as an argument, this
      option will be ignored. The message must be provided via an argument or via this option. Sources must be one of
      `file` or `stdin`. In the case of `file`, a corresponding identifier must also be provided.
      	Note: if both secret passphrase and message are passed via stdin, the passphrase must be the first line.
      	Examples:
      	- --message=file:/path/to/my/message.txt
      	- --message=stdin

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLES
  message:decrypt bba7e2e6a4639c431b68e31115a71ffefcb4e025a4d1656405dfdcd8384719e0 4b800d90d54eda4d093b5e4e6bf9ed203bc90e1560bd628d dcaa605af45a4107a699755237b4c08e1ef75036743d7e4814dea7
  message:decrypt bba7e2e6a4639c431b68e31115a71ffefcb4e025a4d1656405dfdcd8384719e0 1f9008c2813901366f3452431c27218be2c08ac85d6b28a3 --message file:/path/to/encrypted_message.txt
  $ echo f359abaf52a8fb68086cee580ce2b4656840c7c2af1308424eb9ff2b17eae87943502b8f14b6 | lisk message:decrypt bba7e2e6a4639c431b68e31115a71ffefcb4e025a4d1656405dfdcd8384719e0 1f9008c2813901366f3452431c27218be2c08ac85d6b28a3 --message stdin
```

**Example JSON Output**
```json
{
	"message": "My very secret message"
}
```

### Encrypt Message

Encrypts a message for a given recipient public key using your secret passphrase.

This command uses lisk-elements passphrase module to encrypt a message you provide for a given public key using a randomly generated nonce. In order to decrypt the encrypted message later your recipient will need your public key (to verify the message came from you), the nonce and the secret passphrase which matches the specified public key.

> **Important:** Since the secret passphrase is a sensitive input, it can be provided using one of the available methods described in the [Sensitive Inputs section](sensitive-inputs.md). 
> The encrypted message can be provided either directly as an argument, or by specifying a source with the --message option. 
> If both the secret passphrase and the encrypted message are provided via stdin, the secret passphrase must be given in the first line and the encrypted message must be given in the subsequent lines.

```bash
USAGE
  $ lisk message:encrypt RECIPIENTPUBLICKEY [MESSAGE]

ARGUMENTS
  RECIPIENTPUBLICKEY  Public key of the recipient of the message.
  MESSAGE             Message to encrypt.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -m, --message=message
      Specifies a source for providing a message to the command. If a string is provided directly as an argument, this
      option will be ignored. The message must be provided via an argument or via this option. Sources must be one of
      `file` or `stdin`. In the case of `file`, a corresponding identifier must also be provided.
      	Note: if both secret passphrase and message are passed via stdin, the passphrase must be the first line.
      	Examples:
      	- --message=file:/path/to/my/message.txt
      	- --message=stdin

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLES
  message:encrypt bba7e2e6a4639c431b68e31115a71ffefcb4e025a4d1656405dfdcd8384719e0 "My very secret message"
  message:encrypt 5d036a858ce89f844491762eb89e2bfbd50a4a0a0da658e4b2628b25b117ae09 --message file:/path/to/message.txt
  $ echo "My very secret message" | lisk message:encrypt 5d036a858ce89f844491762eb89e2bfbd50a4a0a0da658e4b2628b25b117ae09 --message stdin
```

**Example JSON Output**
```json
 {
	"nonce": "cb4d497e6834e0e888e285f32ddb02bdfd4b471f6ad04e6d",
	"encryptedMessage": "82af57f715c69958bda8b9e95b7f7a09bfaa5afeb94960bf243d7c77a656a3e1ff061c68e20e"
}
```

### Sign Message

Signs a message using your secret passphrase.

This command signs message. You will need the passphrase you sign with.

> **Important:** Since the secret passphrase is a sensitive input, it can be provided using one of the available methods described in the [Sensitive Inputs section](sensitive-inputs.md). 
> The encrypted message can be provided either directly as an argument, or by specifying a source with the --message option. 
> If both the secret passphrase and the encrypted message are provided via stdin, the secret passphrase must be given in the first line and the encrypted message must be given in the subsequent lines.

```bash
USAGE
  $ lisk message:sign [MESSAGE]

ARGUMENTS
  MESSAGE  Message to sign.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -m, --message=message
      Specifies a source for providing a message to the command. If a string is provided directly as an argument, this
      option will be ignored. The message must be provided via an argument or via this option. Sources must be one of
      `file` or `stdin`. In the case of `file`, a corresponding identifier must also be provided.
      	Note: if both secret passphrase and message are passed via stdin, the passphrase must be the first line.
      	Examples:
      	- --message=file:/path/to/my/message.txt
      	- --message=stdin

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

DESCRIPTION
  Signs a message using your secret passphrase.

EXAMPLES
  message:sign "Hello world"
  message:sign --message file:/path/to/message.txt
  $ echo 'Hello World' | lisk message:sign --message stdin
```

**Example JSON Output**
```json
{
	"message": "Hello World",
	"publicKey": "a4465fd76c16fcc458448076372abf1912cc5b150663a64dffefe550f96feadd",
	"signature": "0c70c0ed6ca16312c6acab46dd8b801fd3f3a2bd68018651c2792b40a7d1d3ee276a6bafb6b4185637edfa4d282e18362e135c5e2cf0c68002bfd58307ddb30b"
}
```

### Verify Message

Verifies a signature for a message using the signer’s public key.

This command verify a message after being signed with the sign message command. You will need the public key, signature and message.

```bash
USAGE
  $ lisk message:verify PUBLICKEY SIGNATURE [MESSAGE]

ARGUMENTS
  PUBLICKEY  Public key of the signer of the message.
  SIGNATURE  Signature to verify.
  MESSAGE    Message to verify.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -m, --message=message
      Specifies a source for providing a message to the command. If a string is provided directly as an argument, this
      option will be ignored. The message must be provided via an argument or via this option. Sources must be one of
      `file` or `stdin`. In the case of `file`, a corresponding identifier must also be provided.
      	Note: if both secret passphrase and message are passed via stdin, the passphrase must be the first line.
      	Examples:
      	- --message=file:/path/to/my/message.txt
      	- --message=stdin

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

DESCRIPTION
  Verifies a signature for a message using the signer’s public key.

EXAMPLES
  message:verify 647aac1e2df8a5c870499d7ddc82236b1e10936977537a3844a6b05ea33f9ef6 2a3ca127efcf7b2bf62ac8c3b1f5acf6997cab62ba9fde3567d188edcbacbc5dc8177fb88d03a8691ce03348f569b121bca9e7a3c43bf5c056382f35ff843c09 "Hello world"
  message:verify 647aac1e2df8a5c870499d7ddc82236b1e10936977537a3844a6b05ea33f9ef6 2a3ca127efcf7b2bf62ac8c3b1f5acf6997cab62ba9fde3567d188edcbacbc5dc8177fb88d03a8691ce03348f569b121bca9e7a3c43bf5c056382f35ff843c09 --message file:/path/to/signed_message.txt
  $ echo 'Hello World' | lisk message:verify 647aac1e2df8a5c870499d7ddc82236b1e10936977537a3844a6b05ea33f9ef6 2a3ca127efcf7b2bf62ac8c3b1f5acf6997cab62ba9fde3567d188edcbacbc5dc8177fb88d03a8691ce03348f569b121bca9e7a3c43bf5c056382f35ff843c09 --message stdin
```

**Example JSON Output**
```json
 {
	"verified": true
}
```

## Node

Commands relating to Lisk nodes.

Uses official Lisk Seed Nodes, if no other nodes are provided in [config](#config).

### Forging

Updates the forging status of a node.

```bash
USAGE
  $ lisk node:forging STATUS PUBLICKEY

ARGUMENTS
  STATUS     (enable|disable) Desired forging status.
  PUBLICKEY  Public key of the delegate whose status should be updated.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -w, --password=password
      Specifies a source for your secret password. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --password=prompt (default behaviour)
      	- --password=pass:password123 (should only be used where security is not important)
      	- --password=env:PASSWORD
      	- --password=file:/path/to/my/password.txt (takes the first line only)
      	- --password=stdin (takes the first line only)

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLES
  node:forging enable 647aac1e2df8a5c870499d7ddc82236b1e10936977537a3844a6b05ea33f9ef6
  node:forging disable 647aac1e2df8a5c870499d7ddc82236b1e10936977537a3844a6b05ea33f9ef6
```

### Get Node

Gets information about a node.

```bash
USAGE
  $ lisk node:get

OPTIONS
  -j, --[no-]json   Prints output in JSON format. You can change the default behaviour in your config.json file.

  --forging-status  Additionally provides information about forging status.

  --[no-]pretty     Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                    can change the default behaviour in your config.json file.

EXAMPLES
  node:get
  node:get --forging-status
```

**Example JSON Output**
```json
{
	"build": "v13:05:01 23/10/2018\n",
	"commit": "1785110b343fc42955e46fb5321092b470c686bc",
	"epoch": "2016-05-24T17:00:00.000Z",
	"fees": {
		"send": "10000000",
		"vote": "100000000",
		"secondSignature": "500000000",
		"delegate": "2500000000",
		"multisignature": "500000000",
		"dappRegistration": "2500000000",
		"dappWithdrawal": "10000000",
		"dappDeposit": "10000000"
	},
	"nethash": "da3ed6a45429278bac2666961289ca17ad86595d33b31037615d4b8e8f158bba",
	"nonce": "HrWgya299whkyh8b",
	"milestone": "2",
	"reward": "300000000",
	"supply": "12877201600000000",
	"version": "1.1.1-rc.1",
	"broadhash": "5d72de80e8bee2d447ff1683c34e1298dde70a1e5a43e045aaea29aefb82af89",
	"consensus": 91,
	"height": 6592831,
	"loaded": true,
	"networkHeight": 6592831,
	"syncing": false,
	"transactions": {
		"confirmed": 862234,
		"unconfirmed": 0,
		"unprocessed": 0,
		"unsigned": 0,
		"total": 862234
	}
}
```

## Passphrase

Commands relating to Lisk passphrases.

### Decrypt Passphrase

Decrypts your secret passphrase using the password which was provided at the time of encryption.

This command decrypts your secret passphrase after being encrypted with the encrypt passphrase command. You will need the password you used to encrypt the secret passphrase as well as the initialisation vector (IV) which was randomly generated at the time of encryption.

> **Important:** Since the secret passphrase is a sensitive input, it can be provided using one of the available methods described in the [Sensitive Inputs section](sensitive-inputs.md). 
> The encrypted message can be provided either directly as an argument, or by specifying a source with the --message option. 
> If both the secret passphrase and the encrypted message are provided via stdin, the secret passphrase must be given in the first line and the encrypted message must be given in the subsequent lines.

```bash
USAGE
  $ lisk passphrase:decrypt [ENCRYPTEDPASSPHRASE]

ARGUMENTS
  ENCRYPTEDPASSPHRASE  Encrypted passphrase to decrypt.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -w, --password=password
      Specifies a source for your secret password. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --password=prompt (default behaviour)
      	- --password=pass:password123 (should only be used where security is not important)
      	- --password=env:PASSWORD
      	- --password=file:/path/to/my/password.txt (takes the first line only)
      	- --password=stdin (takes the first line only)

  --passphrase=passphrase
      Specifies a source for providing an encrypted passphrase to the command. If a string is provided directly as an
      argument, this option will be ignored. The encrypted passphrase must be provided via an argument or via this option.
      Sources must be one of `file` or `stdin`. In the case of `file`, a corresponding identifier must also be provided.

      	Note: if both an encrypted passphrase and the password are passed via stdin, the password must be the first line.

      	Examples:
      		- --passphrase file:/path/to/my/encrypted_passphrase.txt (takes the first line only)
      		- --passphrase stdin (takes the first line only)

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLES
  passphrase:decrypt "iterations=1000000&cipherText=9b1c60&iv=5c8843f52ed3c0f2aa0086b0&salt=2240b7f1aa9c899894e528cf5b600e9c&tag=23c01112134317a63bcf3d41ea74e83b&version=1"
  passphrase:decrypt "iterations=1000000&cipherText=9b1c60&iv=5c8843f52ed3c0f2aa0086b0&salt=2240b7f1aa9c899894e528cf5b600e9c&tag=23c01112134317a63bcf3d41ea74e83b&version=1" --passphrase file:./path/to/encrypted_passphrase.txt
  $ echo testing123 | passphrase:decrypt "iterations=1000000&cipherText=9b1c60&iv=5c8843f52ed3c0f2aa0086b0&salt=2240b7f1aa9c899894e528cf5b600e9c&tag=23c01112134317a63bcf3d41ea74e83b&version=1" --passphrase stdin
```

**Example JSON Output**
```json
{
	"passphrase": "minute omit local rare sword knee banner pair rib museum shadow juice"
}
```

### Encrypt Passphrase

Encrypts your secret passphrase under a password.

This command uses AES-256-CBC to encrypt your secret passphrase under a password you provide using a randomly generated initialisation vector (IV). In order to decrypt the secret passphrase later you will need both the IV and the password.

> **Important:** Since the secret passphrase is a sensitive input, it can be provided using one of the available methods described in the [Sensitive Inputs section](sensitive-inputs.md). 
> The encrypted message can be provided either directly as an argument, or by specifying a source with the --message option. 
> If both the secret passphrase and the encrypted message are provided via stdin, the secret passphrase must be given in the first line and the encrypted message must be given in the subsequent lines.

```bash
USAGE
  $ lisk passphrase:encrypt

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  -w, --password=password
      Specifies a source for your secret password. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --password=prompt (default behaviour)
      	- --password=pass:password123 (should only be used where security is not important)
      	- --password=env:PASSWORD
      	- --password=file:/path/to/my/password.txt (takes the first line only)
      	- --password=stdin (takes the first line only)

  --outputPublicKey
      Includes the public key in the output. This option is provided for the convenience of node operators.

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLE
  passphrase:encrypt
```

**Example JSON Output**
```json
{
	"encryptedPassphrase": "iterations=1000000&cipherText=9b1c60&iv=5c8843f52ed3c0f2aa0086b0&salt=2240b7f1aa9c899894e528cf5b600e9c&tag=23c01112134317a63bcf3d41ea74e83b&version=1"
}
```

## Signature

Commands relating to signatures for Lisk transactions from multisignature accounts.

### Broadcast Signature

Broadcasts a signature for a transaction from a multisignature account.

This command broadcast signature to the network. The command takes one required parameters:

- transaction as string in JSON format

```bash
USAGE
  $ lisk signature:broadcast [SIGNATURE]

ARGUMENTS
  SIGNATURE  Signature to broadcast.

OPTIONS
  -j, --[no-]json  Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.

DESCRIPTION
  Broadcasts a signature for a transaction from a multisignature account.
  Accepts a stringified JSON signature as an argument, or a signature can be piped from a previous command.
  If piping make sure to quote out the entire command chain to avoid piping-related conflicts in your shell.

EXAMPLES
  signature:broadcast '{"transactionId":"abcd1234","publicKey":"abcd1234","signature":"abcd1234"}'
  $ echo '{"transactionId":"abcd1234","publicKey":"abcd1234","signature":"abcd1234"}' | lisk signature:broadcast
```

**Example JSON Output**
```json
{
	"meta": {
		"status": true
	},
	"data": {
		"message": "Signature(s) accepted"
	},
	"links": {}
}
```

### Create Signature

Create a signature object for a transaction from a multisignature account.

Accepts a stringified JSON transaction as an argument.

```bash
USAGE
  $ lisk signature:create [TRANSACTION]

ARGUMENTS
  TRANSACTION  Transaction in JSON format.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLE
  signature:create
  '{"amount":"10","recipientId":"8050281191221330746L","senderPublicKey":"3358a1562f9babd523a768e700bb12ad58f230f8403105
  5802dc0ea58cef1e1b","timestamp":59353522,"type":0,"asset":{},"signature":"b84b95087c381ad25b5701096e2d9366ffd04037dcc9
  41cd0747bfb0cf93111834a6c662f149018be4587e6fc4c9f5ba47aa5bbbd3dd836988f153aa8258e604"}'
```

## Transaction

Commands relating to Lisk transactions.

### Broadcast Transaction

Broadcasts a transaction to the network via the node specified in the current config.

Accepts a stringified JSON transaction as an argument, or a transaction can be piped from a previous command.

If piping make sure to quote out the entire command chain to avoid piping-related conflicts in your shell.

```bash
USAGE
  $ lisk transaction:broadcast [TRANSACTION]

ARGUMENTS
  TRANSACTION  Transaction to broadcast in JSON format.

OPTIONS
  -j, --[no-]json  Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.

EXAMPLES
  transaction:broadcast '{"type":0,"amount":"100",...}'
  echo '{"type":0,"amount":"100",...}' | lisk transaction:broadcast
```

**Example JSON Output**
```json
{
	"meta": {
		"status": true
	},
	"data": {
		"message": "Transaction(s) accepted"
	},
	"links": {}
}
```

### Create Transaction

Creates a transaction object.

```bash
USAGE
  $ lisk transaction:create

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  -s, --second-passphrase=second-passphrase
      Specifies a source for your second secret passphrase. For certain commands a second passphrase is necessary, in
      which case Lisk Commander will prompt you for it if this option is not set. Otherwise, Lisk Commander will assume
      you want to use one passphrase only.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --second-passphrase=prompt (to force a prompt even when a second passphrase is not always necessary)
      	- --second-passphrase='pass:my second secret passphrase' (should only be used where security is not important)
      	- --second-passphrase=env:SECOND_SECRET_PASSPHRASE
      	- --second-passphrase=file:/path/to/my/secondPassphrase.txt (takes the first line only)
      	- --second-passphrase=stdin (takes one line only)

  -t, --type=0|transfer|1|second-passphrase|2|delegate|3|vote|4|multisignature
      (required) type of transaction to create

  --no-signature
      Creates the transaction without a signature. Your passphrase will therefore not be required.

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

  --unvotes=unvotes
      Specifies the public keys for the delegate candidates you want to remove your vote from. Takes either a string of
      public keys separated by commas, or a path to a file which contains the public keys.
      	Examples:
      	- --unvotes=publickey1,publickey2
      	- --unvotes=file:/path/to/my/unvotes.txt (every public key should be on a new line)

  --votes=votes
      Specifies the public keys for the delegate candidates you want to vote for. Takes either a string of public keys
      separated by commas, or a path to a file which contains the public keys.
      	Examples:
      	- --votes=publickey1,publickey2
      	- --votes=file:/path/to/my/votes.txt (every public key should be on a new line)

EXAMPLES
  transaction:create --type=0 100 13356260975429434553L
  transaction:create --type=delegate lightcurve
```

#### Transfer Transaction

Creates a transaction which will transfer the specified amount to an address if broadcast to the network.

This command creates and signs a type 0 transaction, which will transfer a Lisk balance to a provided address if broadcast to the network. 

```bash
USAGE
  $ lisk transaction:create:transfer AMOUNT ADDRESS

ARGUMENTS
  AMOUNT   Amount of LSK to send.
  ADDRESS  Address of the recipient.

OPTIONS
  -d, --data=data
      Optional UTF8 encoded data (maximum of 64 bytes) to include in the transaction asset.
      	Examples:
      	- --data=customInformation
      	
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  -s, --second-passphrase=second-passphrase
      Specifies a source for your second secret passphrase. For certain commands a second passphrase is necessary, in
      which case Lisk Commander will prompt you for it if this option is not set. Otherwise, Lisk Commander will assume
      you want to use one passphrase only.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --second-passphrase=prompt (to force a prompt even when a second passphrase is not always necessary)
      	- --second-passphrase='pass:my second secret passphrase' (should only be used where security is not important)
      	- --second-passphrase=env:SECOND_SECRET_PASSPHRASE
      	- --second-passphrase=file:/path/to/my/secondPassphrase.txt (takes the first line only)
      	- --second-passphrase=stdin (takes one line only)

  --no-signature
      Creates the transaction without a signature. Your passphrase will therefore not be required.

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLE
  transaction:create:transfer 100 13356260975429434553L
```

**Example JSON Output**
```json
{
	"amount": "10000000000",
	"recipientId": "13356260975429434553L",
	"senderPublicKey": "caf0f4c00cf9240771975e42b6672c88a832f98f01825dda6e001e2aab0bc0cc",
	"timestamp": 64769338,
	"type": 0,
	"fee": "10000000",
	"recipientPublicKey": null,
	"asset": {},
	"signature": "097bbb6a740a2b90f44b903c0370a6c7ccca86eda6447998e85c745e77f82c2efaf80d9396de5c7a5d7be39a3e9029402b081f8c6f45dde67066d7668b75de05",
	"id": "17042051520078129298"
}
```

#### Second Passphrase Transaction

Creates a transaction which will register a second passphrase for the account if broadcast to the network.

This command creates and signs a type 1 transaction, which will register a second passphrase for the account if broadcast to the network.

```bash
USAGE
  $ lisk transaction:create:second-passphrase

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  -s, --second-passphrase=second-passphrase
      Specifies a source for your second secret passphrase. For certain commands a second passphrase is necessary, in
      which case Lisk Commander will prompt you for it if this option is not set. Otherwise, Lisk Commander will assume
      you want to use one passphrase only.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --second-passphrase=prompt (to force a prompt even when a second passphrase is not always necessary)
      	- --second-passphrase='pass:my second secret passphrase' (should only be used where security is not important)
      	- --second-passphrase=env:SECOND_SECRET_PASSPHRASE
      	- --second-passphrase=file:/path/to/my/secondPassphrase.txt (takes the first line only)
      	- --second-passphrase=stdin (takes one line only)

  --no-signature
      Creates the transaction without a signature. Your passphrase will therefore not be required.

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLE
  transaction:create:second-passphrase
```

**Example JSON Output**
```json
{
	"type": 1,
	"amount": 0,
	"fee": 500000000,
	"recipientId": null,
	"senderPublicKey": "6e0f31cd09bd602bf71960e4da1930ccd39b817d0a73986a09c344204ee1ec6b",
	"timestamp": 48028699,
	"asset": {
		"signature": {
			"publicKey": "a8ef35a53220246cce763ec98dbcf335b30b72d980e3e5cfe1cfcabd68581358"
		}
	},
	"signature": "5ad889263397837b52c7bedaa3bb0c906494a35ef940a410493cd5df1d654b0dbf6561d3a597f0463e5d88cdd8b9e87379266a1b351623cf9760875a2e575f0f",
	"id": "17851553801824463168"
}
```

#### Delegate Registration Transaction

Creates a transaction which will register the account as a delegate candidate if broadcast to the network.

This command creates and signs a type 2 transaction, which will register the account as a delegate candidate if broadcast to the network. It has one required parameter which is the delegate username to be registered.

```bash
USAGE
  $ lisk transaction:create:delegate USERNAME

ARGUMENTS
  USERNAME  Username to register as a delegate.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  -s, --second-passphrase=second-passphrase
      Specifies a source for your second secret passphrase. For certain commands a second passphrase is necessary, in
      which case Lisk Commander will prompt you for it if this option is not set. Otherwise, Lisk Commander will assume
      you want to use one passphrase only.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --second-passphrase=prompt (to force a prompt even when a second passphrase is not always necessary)
      	- --second-passphrase='pass:my second secret passphrase' (should only be used where security is not important)
      	- --second-passphrase=env:SECOND_SECRET_PASSPHRASE
      	- --second-passphrase=file:/path/to/my/secondPassphrase.txt (takes the first line only)
      	- --second-passphrase=stdin (takes one line only)

  --no-signature
      Creates the transaction without a signature. Your passphrase will therefore not be required.

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLE
  transaction:create:delegate lightcurve
```

**Example JSON Output**
```json
{
	"amount": "0",
	"recipientId": "",
	"senderPublicKey": "a4465fd76c16fcc458448076372abf1912cc5b150663a64dffefe550f96feadd",
	"timestamp": 64793730,
	"type": 2,
	"fee": "2500000000",
	"asset": {
		"delegate": {
			"username": "username"
		}
	},
	"signature": "4ef0dedacd5deba50785e115afca48d3db2427e8436e6fe8edb291ab420978cea75814ca58aac1a745da61c1cd5912103e3b8b8f2aed650622eb39d66b98bb01",
	"id": "12587307250270871466"
}
```

#### Cast Votes Transaction

Creates a transaction which will cast votes (and/or unvotes) for delegate candidates using their public keys if broadcast to the network.

This command creates and signs a type 3 transaction, which will cast votes or unvotes for delegates if broadcast to the network. The command requires at least one of the --votes and/or --unvotes options. 

These options can be specified either by a list of public key strings (corresponding to the delegates to be voted for/unvoted) separated by commas, or via a path to a file containing the public keys (where the public keys can be separated by commas or new lines).

```bash
USAGE
  $ lisk transaction:create:vote

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  -s, --second-passphrase=second-passphrase
      Specifies a source for your second secret passphrase. For certain commands a second passphrase is necessary, in
      which case Lisk Commander will prompt you for it if this option is not set. Otherwise, Lisk Commander will assume
      you want to use one passphrase only.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --second-passphrase=prompt (to force a prompt even when a second passphrase is not always necessary)
      	- --second-passphrase='pass:my second secret passphrase' (should only be used where security is not important)
      	- --second-passphrase=env:SECOND_SECRET_PASSPHRASE
      	- --second-passphrase=file:/path/to/my/secondPassphrase.txt (takes the first line only)
      	- --second-passphrase=stdin (takes one line only)

  --no-signature
      Creates the transaction without a signature. Your passphrase will therefore not be required.

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

  --unvotes=unvotes
      Specifies the public keys for the delegate candidates you want to remove your vote from. Takes either a string of
      public keys separated by commas, or a path to a file which contains the public keys.
      	Examples:
      	- --unvotes=publickey1,publickey2
      	- --unvotes=file:/path/to/my/unvotes.txt (every public key should be on a new line)

  --votes=votes
      Specifies the public keys for the delegate candidates you want to vote for. Takes either a string of public keys
      separated by commas, or a path to a file which contains the public keys.
      	Examples:
      	- --votes=publickey1,publickey2
      	- --votes=file:/path/to/my/votes.txt (every public key should be on a new line)

DESCRIPTION
  Creates a transaction which will cast votes (or unvotes) for delegate candidates using their public keys if broadcast
  to the network.

EXAMPLE
  transaction:create:vote --votes 215b667a32a5cd51a94c9c2046c11fffb08c65748febec099451e3b164452bca,922fbfdd596fa78269bbcadc67ec2a1cc15fc929a19c462169568d7a3df1a1aa --unvotes e01b6b8a9b808ec3f67a638a2d3fa0fe1a9439b91dbdde92e2839c3327bd4589,ac09bc40c889f688f9158cca1fcfcdf6320f501242e0f7088d52a5077084ccba
```

**Example JSON Output**
```json
{
	"amount": "0",
	"recipientId": "12475940823804898745L",
	"senderPublicKey": "a4465fd76c16fcc458448076372abf1912cc5b150663a64dffefe550f96feadd",
	"timestamp": 64793558,
	"type": 3,
	"fee": "100000000",
	"asset": {
		"votes": [
			"+669efbe70b10c6c5d2b45465b0cb1e96edc66130a01de199185e5dba5da5aac0",
			"+215b667a32a5cd51a94c9c2046c11fffb08c65748febec099451e3b164452bca"
		]
	},
	"signature": "1d45d794fbf78d0bec828b6876568cbbdc5cfb70eeb0c46d5278771c9db7fcb9fa3c80fb38c57bb57619ea6bb216dbcf7986afc5532dbf52e640407fbf7b6802",
	"id": "12646851302759999136"
}
```

#### Multisignature Account Registration

Creates a transaction which will register the account as a multisignature account if broadcast to the network, using the following arguments:

```bash
USAGE
  $ lisk transaction:create:multisignature LIFETIME MINIMUM KEYSGROUP

ARGUMENTS
  LIFETIME   Number of hours the transaction should remain in the transaction pool before becoming invalid.
  MINIMUM    Minimum number of signatures required for a transaction from the account to be valid.
  KEYSGROUP  Public keys to verify signatures against for the multisignature group.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  -s, --second-passphrase=second-passphrase
      Specifies a source for your second secret passphrase. For certain commands a second passphrase is necessary, in
      which case Lisk Commander will prompt you for it if this option is not set. Otherwise, Lisk Commander will assume
      you want to use one passphrase only.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --second-passphrase=prompt (to force a prompt even when a second passphrase is not always necessary)
      	- --second-passphrase='pass:my second secret passphrase' (should only be used where security is not important)
      	- --second-passphrase=env:SECOND_SECRET_PASSPHRASE
      	- --second-passphrase=file:/path/to/my/secondPassphrase.txt (takes the first line only)
      	- --second-passphrase=stdin (takes one line only)

  --no-signature
      Creates the transaction without a signature. Your passphrase will therefore not be required.

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLE
  transaction:create:multisignature 24 2
  215b667a32a5cd51a94c9c2046c11fffb08c65748febec099451e3b164452bca,922fbfdd596fa78269bbcadc67ec2a1cc15fc929a19c462169568
  d7a3df1a1aa
```

**Example JSON Output**
```json
{
	"amount": "0",
	"recipientId": "",
	"senderPublicKey": "a4465fd76c16fcc458448076372abf1912cc5b150663a64dffefe550f96feadd",
	"timestamp": 64793668,
	"type": 4,
	"fee": "1500000000",
	"asset": {
		"multisignature": {
			"min": 2,
			"lifetime": 24,
			"keysgroup": [
				"+215b667a32a5cd51a94c9c2046c11fffb08c65748febec099451e3b164452bca",
				"+922fbfdd596fa78269bbcadc67ec2a1cc15fc929a19c462169568d7a3df1a1aa"
			]
		}
	},
	"signature": "e82cf02e51db6d815fc1d2e0fa33099e1662f7e463d628d060a5155446e8497266260b00868fba8c61faf140291e9be9826401338bf80a74739e0f4ccca47209",
	"id": "17552046565394161055"
}
```

### Get Transaction

Gets transaction information from the blockchain.

```bash
USAGE
  $ lisk transaction:get IDS

ARGUMENTS
  IDS  Comma-separated transaction ID(s) to get information about.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -s, --state=unsigned|unprocessed
      Get transactions based on a given state. Possible values for the state are 'unsigned' and 'unprocessed'.
      	Examples:
      	- --state=unsigned
      	- --state=unprocessed

  --limit=limit
      [default: 10] Limits the returned transactions array by specified integer amount. Maximum is 100.

  --offset=offset
      [default: 0] Offsets the returned transactions array by specified integer amount.

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

  --sender-id=sender-id
      Get transactions based by senderId which is sender's lisk address'.
      	Examples:
      	- --sender-id=12668885769632475474L

  --sort=amount:asc|amount:desc|fee:asc|fee:desc|type:asc|type:desc|timestamp:asc|timestamp:desc
      [default: timestamp:asc] Fields to sort results by.

DESCRIPTION
  Gets transaction information from the blockchain.

EXAMPLES
  transaction:get 10041151099734832021
  transaction:get 10041151099734832021,1260076503909567890
  transaction:get 10041151099734832021,1260076503909567890 --state=unprocessed
  transaction:get 10041151099734832021 --state=unsigned --sender-id=1813095620424213569L
  transaction:get --state=unsigned --sender-id=1813095620424213569L
  transaction:get --sender-id=1813095620424213569L
  transaction:get --limit=10 --sort=amount:desc
  transaction:get --limit=10 --offset=5
```

**Example JSON Output**
```json
[
	{
		"id": "6504066991503372206",
		"height": 6588235,
		"blockId": "15628722186106902609",
		"type": 0,
		"timestamp": 76726802,
		"senderPublicKey": "f4852b270f76dc8b49bfa88de5906e81d3b001d23852f0e74ba60cac7180a184",
		"senderId": "6076671634347365051L",
		"recipientId": "6711723025288195737L",
		"recipientPublicKey": "",
		"amount": "10000000000",
		"fee": "10000000",
		"signature": "61bda4cdd6b91110184feb9ff99b02e5085a69c8d810fc0a4c71fb5e3731a25ade828f7fe5dbfcc4b6ffc6a658e2fadaa130193725fc9428bf7a59671af32409",
		"signatures": [],
		"confirmations": 4929,
		"asset": {}
	}
]
```

### Sign Transaction

Sign a transaction using your secret passphrase.

> **Important:** Since the secret passphrase is a sensitive input, it can be provided using one of the available methods described in the [Sensitive Inputs section](sensitive-inputs.md). 
> The encrypted message can be provided either directly as an argument, or by specifying a source with the --message option. 
> If both the secret passphrase and the encrypted message are provided via stdin, the secret passphrase must be given in the first line and the encrypted message must be given in the subsequent lines.

```bash
USAGE
  $ lisk transaction:sign [TRANSACTION]

ARGUMENTS
  TRANSACTION  Transaction to sign in JSON format.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  -p, --passphrase=passphrase
      Specifies a source for your secret passphrase. Lisk Commander will prompt you for input if this option is not set.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --passphrase=prompt (default behaviour)
      	- --passphrase='pass:my secret passphrase' (should only be used where security is not important)
      	- --passphrase=env:SECRET_PASSPHRASE
      	- --passphrase=file:/path/to/my/passphrase.txt (takes the first line only)
      	- --passphrase=stdin (takes one line only)

  -s, --second-passphrase=second-passphrase
      Specifies a source for your second secret passphrase. For certain commands a second passphrase is necessary, in
      which case Lisk Commander will prompt you for it if this option is not set. Otherwise, Lisk Commander will assume
      you want to use one passphrase only.
      	Source must be one of `prompt`, `pass`, `env`, `file` or `stdin`. For `pass`, `env` and `file` a corresponding
      identifier must also be provided.
      	Examples:
      	- --second-passphrase=prompt (to force a prompt even when a second passphrase is not always necessary)
      	- --second-passphrase='pass:my second secret passphrase' (should only be used where security is not important)
      	- --second-passphrase=env:SECOND_SECRET_PASSPHRASE
      	- --second-passphrase=file:/path/to/my/secondPassphrase.txt (takes the first line only)
      	- --second-passphrase=stdin (takes one line only)

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

EXAMPLE
  transaction:sign
  '{"amount":"100","recipientId":"13356260975429434553L","senderPublicKey":null,"timestamp":52871598,"type":0,"fee":"100
  00000","recipientPublicKey":null,"asset":{}}'
```

**Example JSON Output**
```json
{
	"amount": "10000000000",
	"recipientId": "13356260975429434553L",
	"senderPublicKey": "a4465fd76c16fcc458448076372abf1912cc5b150663a64dffefe550f96feadd",
	"timestamp": 64872831,
	"type": 0,
	"fee": "10000000",
	"recipientPublicKey": null,
	"asset": {},
	"signature": "0700e70310e4cd4fcb2bb1ec7527b760cc60f90b2629e270ecebd70affb8f6be3c163eda29e8e5ccedcae5f3401e7afd40244a30217aa0d435e762c874a63f00",
	"id": "15637644919032010963"
}
```

### Verify Transaction

Verifies a transaction has a valid signature.

This command verify a transaction after being signed with the sign transaction command or create transaction command. 

You may specify second public key if the transaction has second signature.

```bash
USAGE
  $ lisk transaction:verify [TRANSACTION]

ARGUMENTS
  TRANSACTION  Transaction to verify in JSON format.

OPTIONS
  -j, --[no-]json
      Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty
      Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You can change the
      default behaviour in your config.json file.

  --second-public-key=second-public-key
      Specifies a source for providing a second public key to the command. The second public key must be provided via this
      option. Sources must be one of `file` or `stdin`. In the case of `file`, a corresponding identifier must also be
      provided.

      	Note: if both transaction and second public key are passed via stdin, the transaction must be the first line.

      	Examples:
      	- --second-public-key file:/path/to/my/message.txt
      	- --second-public-key 790049f919979d5ea42cca7b7aa0812cbae8f0db3ee39c1fe3cef18e25b67951

EXAMPLES
  transaction:verify '{"type":0,"amount":"100",...}'
  transaction:verify '{"type":0,"amount":"100",...}' --second-public-key=647aac1e2df8a5c870499d7ddc82236b1e10936977537a3844a6b05ea33f9ef6
  transaction:verify '{"type":0,"amount":"100",...}' --second-public-key file:/path/to/my/message.txt
```

**Example JSON Output**
```json
{
	"verified": true
}
```

## Warranty

Displays warranty notice.

```bash
USAGE
  $ lisk warranty

OPTIONS
  -j, --[no-]json  Prints output in JSON format. You can change the default behaviour in your config.json file.

  --[no-]pretty    Prints JSON in pretty format rather than condensed. Has no effect if the output is set to table. You
                   can change the default behaviour in your config.json file.

DESCRIPTION
  Displays warranty notice.

EXAMPLE
  warranty
```
