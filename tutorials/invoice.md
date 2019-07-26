# Invoice App

A simple application which enables service providers to send invoice requests to their clients.                           

It implements 2 custom transaction types:

- **InvoiceTransaction:** for sending an invoice request.
- **PaymentTransaction:** for fulfilling/paying the received invoice.

Additionally, we will build a simple web-interface for convenient usage of the application. 

The Invoice App implementation goes as following:

- __Steps 1-5__ describe the node-side implementation of the blockchain application.
- __Step 6__ showcases, how to build a user interface to interact with the application.
- __Step 7__ explains how to override specific config values.

> Check out the __full code example__ of the [Invoice App on Github](https://github.com/LiskHQ/lisk-sdk-examples/tree/development/invoice).

## 1. Set up the project

First, let's create the root folder for the Invoice App and initialize the project:

```bash
mkdir invoice # create the root folder for the blockchain application
cd invoice # navigate into the root folder
```

As next step, we want to install the `lisk-sdk` package and add it to our projects' dependencies.

### Supported Platforms

- Ubuntu 16.04 (LTS) x86_64
- Ubuntu 18.04 (LTS) x86_64
- MacOS 10.13 (High Sierra)
- MacOS 10.14 (Mojave)

### Dependencies

| Dependencies     | Version |
| ---------------- | ------- |
| Node.js          | 10.15.3 |
| PostgreSQL       | 10+     |
| Redis (optional) | 5+      |
| Python           | 2       |


> If you miss some of the dependencies, please go to [Lisk SDK - Pre-Install](../../lisk-sdk/setup.md#pre-installation) and follow the pre-installation steps for the SDK.

```bash
npm init --yes # initialize the manifest file of the project
npm install --save lisk-sdk # install lisk-sdk as dependency for the node server side
npm install --save @liskhq/lisk-validator @liskhq/lisk-cryptography @liskhq/lisk-transactions @liskhq/lisk-constants # install lisk-elements dependencies for the client side scripts
```

Make sure to start with a fresh database:
```bash
psql
> DROP DATABASE lisk_dev;
> CREATE DATABASE lisk_dev OWNER lisk;
> \q
```

Create the file `index.js`, which will hold the logic to initialize and start the blockchain application.

```bash
touch index.js # create the index file
```

## 2. Configure the application

Next, let's configure the application, to provide basic information about the app we are going to build:

```js
//index.js
const { Application, genesisBlockDevnet, configDevnet } = require('lisk-sdk'); // require application class, the default genesis block and the default config for the application

configDevnet.app.label = 'Invoice-blockchain-application'; // change the label of the app

const app = new Application(genesisBlockDevnet, configDevnet); // create the application instance

// the code block below starts the application and doesn't need to be changed
app
    .run()
    .then(() => app.logger.info('App started...'))
    .catch(error => {
        console.error('Faced error in application', error);
        process.exit(1);
    });
```

> *See the complete file on Github: [invoice/index.js](https://github.com/LiskHQ/lisk-sdk-examples/tree/development/invoice/index.js).*

In the `line 2`, we require the needed dependencies from the `lisk-sdk` package.
The most important one is the `Application` class, which is used in `line 6` to create the application instance.
The application instance will start the whole application at the bottom of `index.js`.

In `line 6` , the application instance gets initialized.
By passing the parameters for the [genesis block](../../lisk-sdk/configuration.md#the-genesis-block) and the [configuration template](https://github.com/LiskHQ/lisk-sdk/blob/development/sdk/src/samples/config_devnet.json), the application is configured with most basic configurations to start the node.

> If you want to change any of the values for `configDevnet`, check out the [full list of configurations](../../lisk-sdk/configuration.md#list-of-configuration-options) for Lisk SDK and overwrite them like described in [step 8](#8-customize-the-default-configuration)

At this point, you already can start the node and the network, to verify that the setup was successful:

```bash
node index.js | npx bunyan -o short
```
`node index.js` will start the node, and `| npx bunyan -o short` will pretty-print the logs in the console.

If everything is ok, the following logs will be displayed:
```
$ node index.js | npx bunyan -o short
14:01:39.384Z  INFO lisk-framework: Booting the application with Lisk Framework(0.1.0)
14:01:39.391Z  INFO lisk-framework: Starting the app - helloWorld-blockchain-application
14:01:39.392Z  INFO lisk-framework: Initializing controller
14:01:39.392Z  INFO lisk-framework: Loading controller
14:01:39.451Z  INFO lisk-framework: Old PID: 7707
14:01:39.452Z  INFO lisk-framework: Current PID: 7732
14:01:39.467Z  INFO lisk-framework: Loading module lisk-framework-chain:0.1.0 with alias "chain"
14:01:39.613Z  INFO lisk-framework: Event network:bootstrap was subscribed but not registered to the bus yet.
14:01:39.617Z  INFO lisk-framework: Event network:bootstrap was subscribed but not registered to the bus yet.
14:01:39.682Z  INFO lisk-framework: Modules ready and launched
14:01:39.683Z  INFO lisk-framework: Event network:event was subscribed but not registered to the bus yet.
14:01:39.684Z  INFO lisk-framework: Module ready with alias: chain(lisk-framework-chain:0.1.0)
14:01:39.684Z  INFO lisk-framework: Loading module lisk-framework-network:0.1.0 with alias "network"
14:01:39.726Z  INFO lisk-framework: Blocks 1886
14:01:39.727Z  INFO lisk-framework: Genesis block matched with database
14:01:39.791Z ERROR lisk-framework: Error occurred while fetching information from 127.0.0.1:5000
14:01:39.794Z  INFO lisk-framework: Module ready with alias: network(lisk-framework-network:0.1.0)
14:01:39.795Z  INFO lisk-framework: Loading module lisk-framework-http-api:0.1.0 with alias "http_api"
14:01:39.796Z  INFO lisk-framework: Module ready with alias: http_api(lisk-framework-http-api:0.1.0)
14:01:39.797Z  INFO lisk-framework:
  Bus listening to events [ 'app:ready',
    'app:state:updated',
    'chain:bootstrap',
    'chain:blocks:change',
    'chain:signature:change',
    'chain:transactions:change',
    'chain:rounds:change',
    'chain:multisignatures:signature:change',
    'chain:multisignatures:change',
    'chain:delegates:fork',
    'chain:loader:sync',
    'chain:dapps:change',
    'chain:registeredToBus',
    'chain:loading:started',
    'chain:loading:finished',
    'network:bootstrap',
    'network:event',
    'network:registeredToBus',
    'network:loading:started',
    'network:loading:finished',
    'http_api:registeredToBus',
    'http_api:loading:started',
    'http_api:loading:finished' ]
14:01:39.799Z  INFO lisk-framework:
  Bus ready for actions [ 'app:getComponentConfig',
    'app:getApplicationState',
    'app:updateApplicationState',
    'chain:calculateSupply',
    'chain:calculateMilestone',
    'chain:calculateReward',
    'chain:generateDelegateList',
    'chain:updateForgingStatus',
    'chain:postSignature',
    'chain:getForgingStatusForAllDelegates',
    'chain:getTransactionsFromPool',
    'chain:getTransactions',
    'chain:getSignatures',
    'chain:postTransaction',
    'chain:getDelegateBlocksRewards',
    'chain:getSlotNumber',
    'chain:calcSlotRound',
    'chain:getNodeStatus',
    'chain:blocks',
    'chain:blocksCommon',
    'network:request',
    'network:emit',
    'network:getNetworkStatus',
    'network:getPeers',
    'network:getPeersCountByFilter' ]
14:01:39.800Z  INFO lisk-framework: App started...
14:01:39.818Z  INFO lisk-framework: Validating current block with height 1886
14:01:39.819Z  INFO lisk-framework: Loader->validateBlock Validating block 10258884836986606075 at height 1886
14:01:40.594Z  INFO lisk-framework: Lisk started: 0.0.0.0:4000
14:01:40.600Z  INFO lisk-framework: Verify->verifyBlock succeeded for block 10258884836986606075 at height 1886.
14:01:40.600Z  INFO lisk-framework: Loader->validateBlock Validating block succeed for 10258884836986606075 at height 1886.
14:01:40.600Z  INFO lisk-framework: Finished validating the chain. You are at height 1886.
14:01:40.601Z  INFO lisk-framework: Blockchain ready
14:01:40.602Z  INFO lisk-framework: Loading 101 delegates using encrypted passphrases from config
14:01:40.618Z  INFO lisk-framework: Forging enabled on account: 8273455169423958419L
14:01:40.621Z  INFO lisk-framework: Forging enabled on account: 12254605294831056546L
14:01:40.624Z  INFO lisk-framework: Forging enabled on account: 14018336151296112016L
14:01:40.627Z  INFO lisk-framework: Forging enabled on account: 2003981962043442425L
[...]
```

## 3. Create the new transaction types

Now that the SDK is setup successfully, we want to create 2 new transaction types:

- InvoiceTransaction: For sending invoices to the network.
- PaymentTransaction: For paying a particular invoice.

## InvoiceTransaction

The InvoiceTransaction requires an `asset` field with the following properties. 

> Note: The `requestedAmount` input is expressed in Beddows (1 LSK = 10^8 Beddows).

```js
const tx = new InvoiceTransaction({ 
    asset: {
      "client": "World GmbH",
      "requestedAmount": `${transactions.utils.convertLSKToBeddows(10)}`,
      "description": "Test invoice"  
    },
    recipientId: '123L',
    fee: transactions.utils.convertLSKToBeddows('1'),
    timestamp: getTimestamp()
});
```

First, let's create a folder which will store the new transaction types:

```bash
mkdir transactions
touch transactions/invoice_transaction.js
```

Now, we create the InvoiceTransaction by extending the `BaseTransaction` interface:

```js
//transactions/invoice_transaction.js
const { BaseTransaction, TransactionError } = require('@liskhq/lisk-transactions');

class InvoiceTransaction extends BaseTransaction {
    
    /**
    * Set the `InvoiceTransaction` transaction TYPE to `13`.
    * Every time a transaction is received, it gets differentiated by the type.
    * The first 10 types, from 0-9 is reserved for the default Lisk Network functions. 
    */
	static get TYPE () {
		return 13;
	}
	
    /**
    * Set the `InvoiceTransaction` transaction FEE to 1 LSK.
    * Every time a user posts a transaction to the network, the transaction fee is paid to the delegate who includes the transaction into the block that the delegate forges.
    */
	static get FEE () {
		return `${10 ** 8}`;
	}
	
    /**
    * Prepares the necessary data for the `apply` and `undo` step.
    */
	async prepare(store) {
		await store.account.cache([
			{
				address: this.senderId,
			},
		]);
	}
	
    /**
    * Validation of the values of the transaction parameters, defined by the `InvoiceTransaction` transaction signer.
    */
	validateAsset() {
		const errors = [];
		if (!this.asset.client || typeof this.asset.client !== 'string') {
			errors.push(
				new TransactionError(
					'Invalid "asset.client" defined on transaction',
					this.id,
					'.asset.client',
					this.asset.client,
					'A string value',
				)
			);
		}
		if (!this.asset.requestedAmount || typeof this.asset.requestedAmount !== 'string') {
			errors.push(
				new TransactionError(
					'Invalid "asset.requestedAmount" defined on transaction',
					this.id,
					'.asset.requestedAmount',
					this.asset.requestedAmount,
					'A string value',
				)
			);
		}
		if (!this.asset.description || typeof this.asset.description !== 'string') {
			errors.push(
				new TransactionError(
					'Invalid "asset.description" defined on transaction',
					this.id,
					'.asset.description',
					this.asset.description,
					'A string value',
				)
			);
		}
		return errors;
	}
	
    /**
    * applyAsset() is where the custom logic of the InvoiceTransaction is implemented. 
    * Here we can store additional information about accounts using the `asset` field.
    * If it's the first invoice, the account is sending, two new properties `invoiceCount` and `invoicesSent` are added to the account assets.
    * If at least one other invoice has already been sent by this account, it would increment `invoiceCount` and add the Transaction ID of the InvoiceTransaction to the `invoicesSent` list.
    */
	applyAsset(store) {
		const sender = store.account.get(this.senderId);
		
		// Save invoice count and IDs
		sender.asset.invoiceCount = sender.asset.invoiceCount === undefined ? 1 : sender.asset.invoiceCount++;
		sender.asset.invoicesSent = sender.asset.invoicesSent === undefined ? [this.id] : [...sender.asset.invoicesSent, this.id];
		store.account.set(sender.address, sender);
		return [];
	}
	
    /**
    * Inverse of `applyAsset`.
    * Undoes the changes made in applyAsset() step.
    */
	undoAsset(store) {
		const sender = store.account.get(this.senderId);
		
		// Rollback invoice count and IDs
		sender.asset.invoiceCount = sender.asset.invoiceCount === 1 ? undefined : sender.asset.invoiceCount--;
		sender.asset.invoicesSent = sender.asset.invoicesSent.splice(
			sender.asset.invoicesSent.indexOf(this.id),
			1,
		);
		store.account.set(sender.address, sender);
		return [];
	}
	
}

module.exports = InvoiceTransaction;
```
> *See the file on Github: [invoice/transactions/invoice_transaction.js](https://github.com/LiskHQ/lisk-sdk-examples/tree/development/invoice/transactions/invoice_transaction.js).*

## PaymentTransaction

The InvoiceTransaction requires an `asset` field with the following properties. 

> Note: The `requestedAmount` input is expressed in Beddows (1 LSK = 10^8 Beddows).

```js
const tx = new PaymentTransaction({ 
    asset: {
      "data": "InvoiceTransaction-ID" 
    },
    recipientId: '456L',
    fee: transactions.utils.convertLSKToBeddows('0.1'),
    timestamp: getTimestamp()
});
```

Now, let's create a folder which will store the new transaction types:

```bash
mkdir transactions
touch transactions/invoice_transaction.js
```

Now, let's the PaymentTransaction by extending the already existing trasnaction type `TransferTransaction` interface:


```bash
touch transactions/payment_transaction.js
```

```js
//transactions/payment_transaction.js
const { TransferTransaction, TransactionError } = require('@liskhq/lisk-transactions');

class PaymentTransaction extends TransferTransaction {
    
    /**
    * Set the `PaymentTransaction` transaction TYPE to `14`.
    * Every time a transaction is received, it gets differentiated by the type.
    * The first 10 types, from 0-9 is reserved for the default Lisk Network functions. 
    */
	static get TYPE () {
		return 14;
	}
	
    /**
    * Prepares the necessary data for the `apply` and `undo` step.
    */
	async prepare(store) {
		await super.prepare(store);
		await store.transaction.cache([
			{
				id: this.asset.data,
			},
		]);
	}
	
    /**
    * applyAsset() is where the custom logic of the PaymentTransaction is implemented. 
    * The database is searched for the existance of an InvoiceTransaction with the ID that is set in the `asset.data` field of the PaymentTransaction.
    * If the transaction is found, the `requestedAmount` in the `asset` field is compared to the PaymentTransaction amount.
    * If the transaction amount is equal or higher than the `requestedAmount` in the corresponding InvoiceTransaction, the PaymentTransaction gets accepted.
    * Note, that we are not verifying at this point, if the sender has already paid the invoice or not, to keep this example simple.
    */
	applyAsset(store) {
		super.applyAsset(store);
		const errors = [];
		const transaction = store.transaction.find(
			transaction => transaction.id === this.asset.data
		); // Find related invoice in transactions for invoiceID
		
		if (transaction) {
			if (this.amount.lt(transaction.asset.requestedAmount)) {
				errors.push(
					new TransactionError(
						'Paid amount is lower than amount stated on invoice',
						this.id,
						'.amount',
						transaction.requestedAmount,
						'Expected amount to be equal or greated than `requestedAmount`',
					)
				);
			}
		} else {
			errors.push(
				new TransactionError(
					'Invoice does not exist for ID',
					this.id,
					'.asset.invoiceID',
					this.asset.data,
					'Existing invoiceID registered as invoice transaction',
				)
			);
		}
		
		return errors;
	}
	
    /**
    * Inverse of `applyAsset()`.
    * No rollback needed as there is only validation happening in applyAsset().
    * The implementation of sending the tokens back to the sender is already implemented in the TransferTransaction class.
    */
	undoAsset(store) {
		super.undoAsset(store); 
	
		return [];
	}
	
}

module.exports = PaymentTransaction;
```
> *See the file on Github: [invoice/transactions/payment_transaction.js](https://github.com/LiskHQ/lisk-sdk-examples/tree/development/invoice/transactions/payment_transaction.js).*

## 4. Register the new transaction types

Right now, your project should have the following file structure:

```
invoice
├── transactions
| ├── invoice_transaction.js
| └── payment_transaction.js
├── index.js
├── node_modules
└── package.json
```

Add the new transaction types to your application, by registering them to the application instance:

```js
//index.js
const { Application, genesisBlockDevnet, configDevnet} = require('lisk-sdk'); // require application class, the default genesis block and the default config for the application
const InvoiceTransaction = require('./transactions/invoice_transaction'); // require the newly created transaction type 'InvoiceTransaction'
const PayemntTransaction = require('./transactions/payment_transaction'); // require the newly created transaction type 'PayemntTransaction'

configDevnet.app.label = 'invoice-blockchain-application'; // customize the application label

const app = new Application(genesisBlockDevnet, configDevnet); // create the application instance

app.registerTransaction(InvoiceTransaction); // register the 'InvoiceTransaction' 
app.registerTransaction(PayemntTransaction); // register the 'PayemntTransaction' 

// the code block below starts the application and doesn't need to be changed
app
    .run()
    .then(() => app.logger.info('App started...'))
    .catch(error => {
        console.error('Faced error in application', error);
        process.exit(1);
    });
```
> *See the file on Github: [invoice/index.js](https://github.com/LiskHQ/lisk-sdk-examples/tree/development/invoice/index.js).*

## 5. Start the network

Now, let's start our customized blockchain network for the first time.

The parameter `configDevnet`, which we pass to our `Application` instance in [step 3](#3-create-the-new-transaction-types), is preconfigured to start the node with a set of dummy delegates, that have enabled forging by default.
These dummy delegates stabilize the new network and make it possible to test out the basic functionality of the network with only one node immediately.

This creates a simple Devnet, which is beneficial during development of the blockchain application.
The dummy delegates can be replaced by real delegates later on.

To start the network, execute the following command:

```bash
node index.js | npx bunyan -o short
```

Check the logs, to verify the network has started successfully.

If something went wrong, the process should stop and an error with debug information is displayed.

## 6. Interact with the network

Now that the network is started, we want to create a simple web interface for the Invoice application.

As first step, create the transaction object.

```bash
mkdir client # create the folder for the client-side scripts
cd client # navigate into the client folder
touch print_sendable_hello-world.js # create the file that will hold the code to create the transaction object
```

```js
//client/print_sendable_hello-world.js
const HelloTransaction = require('../hello_transaction');
const transactions = require('@liskhq/lisk-transactions');
const { EPOCH_TIME } = require('@liskhq/lisk-constants');

const getTimestamp = () => {
	// check config file or curl localhost:4000/api/node/constants to verify your epoc time
	const millisSinceEpoc = Date.now() - Date.parse(EPOCH_TIME); 
	const inSeconds = ((millisSinceEpoc) / 1000).toFixed(0);
	return  parseInt(inSeconds);
}

let tx =  new HelloTransaction({ // the desired transaction gets created and signed
	asset: {
		hello: 'world', // we save the string 'world' into the 'hello' asset
	},
	fee: `${transactions.utils.convertLSKToBeddows('1')}`, // we set the fee to 1 LSK
	recipientId: '10881167371402274308L', // address of dummy delegate genesis_100
	timestamp: getTimestamp(),
});

tx.sign('wagon stock borrow episode laundry kitten salute link globe zero feed marble');

console.log(tx.stringify()); // the transaction is displayed as JSON object in the console
process.exit(1); // stops the process after the transaction object has been printed
```
> *See the complete file on Github: [hello_world/client/print_sendable_hello-world.js](https://github.com/LiskHQ/lisk-sdk-examples/blob/development/hello_world/client/print_sendable_hello-world.js).*
