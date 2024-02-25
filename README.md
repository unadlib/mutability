# Mutability

![Node CI](https://github.com/unadlib/mutability/workflows/Node%20CI/badge.svg)
[![npm version](https://badge.fury.io/js/mutability.svg)](http://badge.fury.io/js/mutability)

A JavaScript library for transactional mutable updates

## Motivation

When we want to perform transactional updates on a mutable object, if an error is caught during the update process, the mutable update will not be applied at all. Otherwise, the mutable update will be applied to the mutable object. Therefore, we need a tool to implement this functionality.

## Installation

```sh
yarn add mutability
```

## Usage

```ts
import { mutate } from 'mutability';

test('base - mutate', () => {
  const baseState = {
    a: {
      c: 1,
    },
  };
  mutate(baseState, (draft) => {
    draft.a.c = 2;
  });
  expect(baseState).toEqual({ a: { c: 2 } });
});

test('base - mutate with error', () => {
  const baseState = {
    a: {
      c: 1,
    },
    b: {
      c: 1,
    },
  };
  try {
    mutate(baseState, (draft) => {
      draft.a.c = 2;
      throw new Error('error');
      draft.b.c = 2;
    });
  } catch (e) {
    //
  }
  expect(baseState).toEqual({
    a: {
      c: 1,
    },
    b: {
      c: 1,
    },
  });
});
```

## License

Mutability is [MIT licensed](https://github.com/unadlib/mutability/blob/main/LICENSE).
