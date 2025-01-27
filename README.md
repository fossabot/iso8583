# ISO8583 JS

ISO 8583 is an international standard for financial transaction card originated interchange messaging. It is the International Organization for Standardization standard for systems that exchange electronic transactions initiated by cardholders using payment cards.

This library help you for wrapping message into ISO8583 and parse the message

## Installation

```sh
npm install iso8583-js
```

## Features

- Wrapping message into ISO8583
- Parse the message

## Usage

Example :

```js
let x = new ISO8583({
  header: 'ISO015000017'
});

// Init the structure
x.init([
  ['PRIMARY_ACCOUNT_NUMBER', { bitmap: 2, length: 18 }],
  ['LOCAL_DATE', { bitmap: 13, length: 4 }]
]);

// Set the value
x.set('PRIMARY_ACCOUNT_NUMBER', '366577921569117691');
x.set('LOCAL_DATE', '112406');

// Wrap the message
console.log(x.wrapMsg()); // -> 4008000000000000366577921569117691112406

// Unwrap the message
console.log(x.unWrapMsg('4008000000000000366577921569117691112406'));
```

## API Reference

Initialize new ISO8583

```js
const ISO8583 = require('iso8583-js');
```

### Constructor

```js
const merchant = new ISO8583([options]);
```

#### Options

- `header` : Set the message header if exist
- `mti` : The message type indicator is a four-digit numeric field which indicates the overall function of the message. This option will read the incoming message of first four-digit as mti. Default : `true` . See the [usage]() 

### Init

Initialization of ISO8583 structure.

```js
merchant.init([[key, options]]);
```

#### Options

Currently, these options are mandatory

- `bitmap` : Bitmap for referencing a key
- `length` : Length of message

#### Example

```js
merchant.init([
  ['PRIMARY_ACCOUNT_NUMBER', { bitmap: 2, length: 18 }],
  ['LOCAL_DATE', { bitmap: 13, length: 4 }]
]);
```

### set

Set the value by referencing to your key

```js
merchant.set(key, value);
```

### WrapMsg

Wrapping message into ISO8583

```js
merchant.wrapMsg(mtiType); //string
```

#### mtiType - optional


You can set the value of MTI Type. For example : 

```js
/**
 * - 0800 : Echo 
 * For more, please refer to https://en.wikipedia.org/wiki/ISO_8583 
*/
merchant.wrapMsg(0800);

```


### unWrapMsg

Unwrapping the message and returning as Map structure

```js
let X = merchant.unWrapMsg(hex); //Map [[key, value]]
X.get(key);

console.log(X);
```

## To-Do (Currently not supported yet)

- Initialization should being optional
- Bitmap on init method should ordered by ascending
- Checking set `key` when `key` not listed on init
- Add options output as (Object or Map) in unWrap method
- Add MTI meaning in wrap message
- Attributes enhancement

[![All Contributors](https://img.shields.io/badge/all_contributors-1-orange.svg?style=flat-square)](#contributors)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fadefirmanf%2Fiso8583.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fadefirmanf%2Fiso8583?ref=badge_shield)

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
<table><tr><td align="center"><a href="http://adefirmanf.github.io"><img src="https://avatars0.githubusercontent.com/u/23324722?v=4" width="100px;" alt="Ade Firman F"/><br /><sub><b>Ade Firman F</b></sub></a><br /><a href="https://github.com/adefirmanf/iso8583/commits?author=adefirmanf" title="Code">💻</a> <a href="https://github.com/adefirmanf/iso8583/commits?author=adefirmanf" title="Documentation">📖</a> <a href="https://github.com/adefirmanf/iso8583/commits?author=adefirmanf" title="Tests">⚠️</a> <a href="#example-adefirmanf" title="Examples">💡</a></td></tr></table>

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fadefirmanf%2Fiso8583.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fadefirmanf%2Fiso8583?ref=badge_large)