# Convert JSON to CSV or CSV to JSON

[![Build Status](https://travis-ci.org/mrodrig/json-2-csv.svg?branch=master)](https://travis-ci.org/mrodrig/json-2-csv)
![David - Dependency Checker Icon](https://david-dm.org/mrodrig/json-2-csv.png "json-2-csv Dependency Status")
[![Downloads](http://img.shields.io/npm/dm/json-2-csv.svg)](https://www.npmjs.org/package/json-2-csv)
[![NPM version](https://img.shields.io/npm/v/json-2-csv.svg)](https://www.npmjs.org/package/json-2-csv)
[![bitHound Score](https://www.bithound.io/github/mrodrig/json-2-csv/badges/score.svg)](https://www.bithound.io/github/mrodrig/json-2-csv)

This node module will convert an array of JSON documents to a CSV string.
Column headings will be automatically generated based on the keys of the JSON documents. Nested documents will have a '.' appended between the keys.

It is also capable of converting CSV of the same form back into the original array of JSON documents.
The columns headings will be used as the JSON document keys.  All lines must have the same exact number of CSV values.

## Installation

```bash
$ npm install json-2-csv
```

## Usage

```javascript
var converter = require('json-2-csv');
```

### API

#### json2csv Documentation (Wiki)

[json2csv API Documentation (Link)](https://github.com/mrodrig/json-2-csv/wiki/json2csv-Documentation)

#### csv2json(csv, callback, options)

[csv2json API Documentation (Link)](https://github.com/mrodrig/json-2-csv/wiki/csv2json-Documentation)

## Tests

```bash
$ npm test
```

_Note_: This requires `mocha`, `should`, `async`, and `underscore`.

To see test coverage, please run:
```bash
$ npm run coverage
```

Current Coverage is:
```
Statements   : 96.69% ( 175/181 )
Branches     : 93.48% ( 129/138 )
Functions    : 100% ( 33/33 )
Lines        : 97.63% ( 165/169 )
```

## Features

- Header Generation (per document keys)
- Allows for conversion of specific keys in both json2csv and csv2json via the options.KEYS parameter (as of 1.1.2)
- Verifies all documents have same schema (schema field order does not matter as of 1.1.0)
- Supports sub-documents natively
- Supports arrays as document values for both json2csv and csv2json
- Custom ordering of columns (see F.A.Q. for more information)
- Ability to re-generate the JSON documents that were used to generate the CSV (including nested documents)
- Allows for custom field delimiters, end of line delimiters, etc.
- Promisifiable via bluebird's .promisify(<function>) and .promisifyAll(<object>) (as of 1.1.1)
- Wrapped value support for json2csv and csv2json (as of 1.3.0)
- Support for multiple different schemas (as of 1.4.0)

## F.A.Q.

- Can the order of the keys be changed in the output?
__Yes.__ Currently, changing the order of the keys in the JSON document will also change the order of the columns. (Tested on Node 10.xx)

- Can I specify the keys that I would like to have converted to CSV or JSON?
__Yes.__ This is currently supported for both json2csv and csv2json.  Specify the keys in options.KEYS. For example,

```javascript
var converter = require('json-2-csv');

var options = {
    KEYS : ['info.name', 'year']
};

var documents = [
    {
        "info": {
            "name": "Mike"
        },
        "coursesTaken": ["CS2500", "CS2510"],
        "year": "Sophomore"
    },
    {
        "info": {
            "name": "John"
        },
        "coursesTaken": ["ANTH1101", "POL2312", "MATH2142", "POL3305", "LAW2100"],
        "year": "Senior"
    },
    {
        "info": {
                    "name": "Joe"
        },
        "coursesTaken": [],
        "year": "Freshman"
    }
];

converter.json2csv(documents, function (err, csv) {
    if (!err) {
        return console.log(csv);
    }
    throw err;
}, options);
```

This prints out:

```csv
info.name,year
Mike,Sophomore
John,Senior
Joe,Freshman

```

## Milestones
 - Created: Apr 23, 2014
 - 1K Downloads/Month: January 15, 2015
