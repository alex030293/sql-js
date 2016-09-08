[![Version](https://img.shields.io/badge/Version-0.0.1-blue.svg)](https://img.shields.io/badge/Version-0.0.1-blue.svg)
[![Build Status](https://travis-ci.org/alex030293/sqljs.svg?branch=master)](https://travis-ci.org/alex030293/sqljs)

# SQLjs
SQL-like interface for JavaScript

# Usage

## Trivial

```javascript
import { query } from 'sqljs';

const characters = [
    { name: 'Han',    profession: 'Smuggler', age: 30 },
    { name: 'Luke',   profession: 'Hero',     age: 32 },
    { name: 'Leia',   profession: 'Princess', age: 32 },
    { name: 'Anakin', profession: 'Jedi',     age: 50 },
    { name: 'Obi',    profession: 'Jedi',     age: 65 },
    { name: 'Chewie', profession: 'Smuggler', age: 30 },
    { name: 'Lando',  profession: 'Smuggler', age: 50 }
];

let resultSet = query()
    .select()
    .from(characters)
    .execute();
```


## The easy way

```javascript
import { query } from 'sqljs';

const characters = [
    { name: 'Han',    profession: 'Smuggler', age: 30 },
    { name: 'Luke',   profession: 'Hero',     age: 32 },
    { name: 'Leia',   profession: 'Princess', age: 32 },
    { name: 'Anakin', profession: 'Jedi',     age: 50 },
    { name: 'Obi',    profession: 'Jedi',     age: 65 },
    { name: 'Chewie', profession: 'Smuggler', age: 30 },
    { name: 'Lando',  profession: 'Smuggler', age: 50 }
];

const isJedi = (person) => person.profession === 'Jedi';
const age = (character) => character.age;

let resultSet = query()
    .select()
    .from(characters)
    .where(isJedi)
    .groupBy(age)
    .execute();
```

## Level Up

```javascript
import { query } from 'sqljs';

const rebels = [
    { name: 'Han',    profession: 'Smuggler', age: 30 },
    { name: 'Luke',   profession: 'Jedi',     age: 32, father: 'Darth Vader' },
    { name: 'Leia',   profession: 'Princess', age: 32 },
    { name: 'Obi',    profession: 'Jedi',     age: 65 },
    { name: 'Chewie', profession: 'Smuggler', age: 30 }
];
const empire = [
    { name: 'Anakin',      profession: 'Jedi',      age: 50 },
    { name: 'Darth Vader', profession: 'Lord Sith', age: 65 },
    { name: 'Lando',       profession: 'Smuggler',  age: 50 }
];

const nameAndFather = (join) => { return { name: join[0].name, father: join[1].name } };
const fatherJoin = (join) => join[0].father === join[1].name;
const isJedi = (join) => join[0].profession === 'Jedi';

let resultSet = query()
    .select(nameAndFather)
    .from(rebels, empire)
    .where(fatherJoin)
    .where(isJedi)
    .execute();
```
