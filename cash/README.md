# cash

> A simple money converter that will convert an amount of money to many other currencies


## Usage: Convert cash amount to other currencies

To convert money to other currencies on a command prompt, you need to be on the bin repository of the cash module (`cd .../yourpath/3-musketeers/cash/bin`) and enter one of the following commands:

  1. `node index.js` : Converts money using the default currencies.
  2. `node index.js <amount>` : Converts money by using the default currencies and specifying the amount to be converted.
- `<amount>` (int, float) - The amount of money to convert.
  3. `node index.js <amount> <from> <to>` : Converts money by specifying the amount, its currency and the currencies to be converted into.
- `<amount>` (int, float) - The amount of money to convert.
- `<from>` (string) - The currency of the amount to convert. See more on `cash/lib/currencies.json`
- `<to>` (string) - The currencies in which the amount will be converted into.  See more on `cash/lib/currencies.json`

```js
const Conf = require('conf');
const meow = require('meow');
const chalk = require('chalk');
const cash = require('./cash.js');

const config = new Conf();
const argv = process.argv.slice(2);

const {DEFAULT_TO_CURRENCIES} = require('./constants');


const command = {
	amount: parseFloat(argv[0]) || 1,
	from: argv[1] || config.get('defaultFrom', 'USD'),
	to: (argv.length > 2) ? process.argv.slice(4) : config.get('defaultTo', DEFAULT_TO_CURRENCIES)
};

cash(command);
```

For example, running `node index.js 10 eur usd` will result in the output:

```
√ 11.383 (USD) United States Dollar

Conversion of EUR 10
```


## Usage: Setting default currencies

You can set default currencies. To do so, you need to be on the bin repository of the cash module (`cd .../yourpath/3-musketeers/cash/bin`) and enter the following command:

`node index.js [-s / --save] <from> <to>`
  - `<from>` (string) - The currency of the amount to convert.  See more on `cash/lib/currencies.json`
  - `<to>` (string) - The currencies in which the amount will be converted into.  See more on `cash/lib/currencies.json`

```js
if (argv.indexOf('--save') !== -1 || argv.indexOf('-s') !== -1) {
	config.set('defaultFrom', argv[1] || config.get('defaultFrom', 'USD'));
	config.set('defaultTo', (argv.length > 2) ? process.argv.slice(4) : config.get('defaultTo', DEFAULT_TO_CURRENCIES));
	console.log(chalk.green('Saved default currencies to ' + config.path));
	process.exit(0);
}
```

For example, running `node index.js --save eur krw` will result in the output:

```
Saved default currencies to C:\Users\User\AppData\Local\cash-nodejs\Config\config.json
```

When running `node index.js` again, the output will be:

```
√ 1282.120 (KRW) South Korean Won

Conversion of EUR 1
```


## API

```js
const cash = require('./cash.js');
```

#### cash(command)

Call the cash function with the parameter `command`.

`command` is a constant containing three items: `amount` (int, float), `from` (string) and `to` ([string]).


## Install

Fork the [cash module](https://github.com/92bondstreet/3-musketeers) from github and open a command prompt:

```
cd /path/to/workspace
git clone git@github.com:YOUR_USERNAME/3-musketeers.git
```

With [npm](https://npmjs.org/) installed, run:

```
cd /path/to/workspace/3-musketeers/cash
npm i
```
