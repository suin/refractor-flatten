# @suin/refractor-flatten

A utility to transform [Refractor](https://github.com/wooorm/refractor) ASTs to flat arrays.

## Installation

```bash
yarn add @suin/refractor-flatten
# or
npm install @suin/refractor-flatten
```

## Usage

### Basic Usage

```typescript
import refractor from "refractor";
import flatten from "@suin/refractor-flatten";

const tree = refractor.highlight("`${value}`", "js");
const flat = flatten(tree);
```

The structure of `tree` is:

```
root[1]
└─0 element<span>[3]
    │ properties: {"className":["token","template-string"]}
    ├─0 element<span>[1]
    │   │ properties: {"className":["token","template-punctuation","string"]}
    │   └─0 text "`"
    ├─1 element<span>[3]
    │   │ properties: {"className":["token","interpolation"]}
    │   ├─0 element<span>[1]
    │   │   │ properties: {"className":["token","interpolation-punctuation","punctuation"]}
    │   │   └─0 text "${"
    │   ├─1 text "value"
    │   └─2 element<span>[1]
    │       │ properties: {"className":["token","interpolation-punctuation","punctuation"]}
    │       └─0 text "}"
    └─2 element<span>[1]
        │ properties: {"className":["token","template-punctuation","string"]}
        └─0 text "`"
```

The structure of the `flat` above becomes:

```
root[5]
├─0 element<span>[1]
│   │ properties: {"className":["token","template-string","template-punctuation","string"]}
│   └─0 text "`"
├─1 element<span>[1]
│   │ properties: {"className":["token","template-string","interpolation","interpolation-punctuation","punctuation"]}
│   └─0 text "${"
├─2 element<span>[1]
│   │ properties: {"className":["token","template-string","interpolation"]}
│   └─0 text "value"
├─3 element<span>[1]
│   │ properties: {"className":["token","template-string","interpolation","interpolation-punctuation","punctuation"]}
│   └─0 text "}"
└─4 element<span>[1]
    │ properties: {"className":["token","template-string","template-punctuation","string"]}
    └─0 text "`"
```

## API Reference

https://suin.github.io/refractor-flatten/
