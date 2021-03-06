# schema-normalizer
## Installation
`npm i @playma256/schema-normalizer --save` or `yarn add @playma256/schema-normalizer -S`

## Motivations
Well, i needed a data normalizer, but a simple one which i could say which properties of something i needed and that would be exported.
So i searched the whole internet seeking for a simple solution, which i could not find.

In a nutshell, this is a normalizer/extracter in steroids.

## How to use it
Given an object, i.e, data.

```javascript
{
  prop1: [some array with strings],
  prop2: [{prop21: 'teste', prop22: 'teste2'}],
  prop4: {
    prop41: 'something',
    prop42: 'something2'
  }
}
```

We would like to extract just prop22 from prop2 and everything from prop4, but we would like to have a prop5, empty string, just for normalization purposes, so how do we do that?

First: we create a "pseudo" schema.

```javascript
export default {
  prop2: ['prop22'],
  prop4: "*",
  prop5: ''
}
```

``` javascript
const normalizer = require('@playma256/schema-normalizer');

const data = {
  prop1: [some array with strings],
  prop2: [{prop21: 'teste', prop22: 'teste2'}],
  prop4: {
    prop41: 'something',
    prop42: 'something2'
  }
};

const finalData = normalizer(schema, data);
```

As a result:
```javascript
console.log(finalData);
>> {
  prop2: [{prop22: 'teste2'}],
  prop4: {
    prop41: 'something',
    prop42: 'something2'
  },
  prop5: ''
};
```

This lib has two wildcards that can be used at the moment:
- \* (asterisk) -> this means, everything from the property.
- ! (optional) -> if it has this value, add, if not, omit.

