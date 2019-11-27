## Ledger Vault Front - Homework

#### Presentation

The goal of this homework is to build an UI where the user can manage a **list of addresses**.

An "Address" entry is defined by:

- `name` (string): Name of the address (e.g `Client 1`)
- `address` (string): Contains the address (e.g `mtXWDB6k5yC5v7TcwKZHB89SUp85yCKshy`)
- `currency` (CryptoCurrency): The currency of the address. You can check the [type here](https://github.com/LedgerHQ/ledger-live-common/blob/6231469c78fe55267b85b0857f02abd5a54effce/src/types/currencies.js#L50-L82)

You will have to generate a small web project that you will push on GitHub, with instructions on how to run it.

#### Fonctional requirements

The user should be able to:

- Add a new address to the list
- Edit an existing address from the list
- Remove an address from the list

Every currency has a specific format for their address so you need to add a validation to check if the address is correct. You don't have to write the validation yourself, you will use this dummy function. **Note that the validation happens asynchronously (on real world it's a network call).**

```js
const validateAddress = async ({ currency, address }) => {
  // wait 1s to simulate network request
  await new Promise(r => setTimeout(r, 1000));
  if (validators[currency.family]) return validators[currency.family](address);
  return true;
};

// Obviously the validators implemented here are
// dummy and do no reflect the reality
const validators = {
  bitcoin: address => address.length === 12,
  ripple: address => address.length === 24,
  ethereum: address => address.length === 32
};
```

To list all currencies, you will use:

```js
import { listCryptoCurrencies } from "@ledgerhq/live-common/lib/currencies";

const currencies = listCryptoCurrencies();
console.log(currencies);

// [{ type: "CryptoCurrency", id: "aeternity", ... }, ...]
```

##### Troubleshooting

You will probably get this error when using `@ledger/live-common` package:

```
Uncaught ReferenceError: regeneratorRuntime is not defined
```

It's a [known issue](https://github.com/LedgerHQ/ledgerjs/issues/332) currently being patched. To "fix", you have to:

```
yarn add @babel/polyfill
```

(or `npm i @babel/polyfill`)

Then in your entry point file:

```js
import "@babel/polyfill";
```

#### UI / UX

When adding/editing an Address, you need to show a select (for the currency) and two text inputs (name & address). The "Add"/"Save" button must be disabled if any field is empty or if the address is not valid or if validation is pending (cf `validateAddress`).

We don't provide UI guidelines explicitly so you are free to design whatever feels nice and user friendly to you, colors, shapes, etc.

#### Tech stack

- You can use either FlowType or Typescript, but the code must be typed
- You must use ReactJS. Any external lib that you find useful can be added
- Regarding styling you can use whatever you want (css modules/sass/styled-components, etc.)
- You can use any bundler (we recommend using [parcel](https://parceljs.org/))

#### Bonus

Feel free to add anything you want as a bonus (e.g show more/show less, animations...)

![](https://media.giphy.com/media/l49JHz7kJvl6MCj3G/giphy.gif)
