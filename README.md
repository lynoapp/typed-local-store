# typed-local-storage [![Tests Actions Status](https://github.com/gcascio/typed-local-store/workflows/Tests/badge.svg)](https://github.com/gcascio/typed-local-store/actions)

A wrapper to provide type safe access to the localStorage and sessionStorage.

## Installation

```bash
npm install typed-local-store
# or
yarn add typed-local-store
```

## Usage

Create a schema of your desired storage structure:

```typescript
interface Schema {
  counter: number;
  message: string;
  user: {
    id: string;
    name: string;
    email: string;
    isAdmin: boolean;
  };
  posts: string[];
}
```

Then create your storage using the defined schema:

```typescript
import TypedLocalStore from 'typed-local-store';

const typedStorage = new TypedLocalStore<Schema>();
```

### Options

The constructor can receive a options object to configure the store.

#### `options`

| Property | Required | Default        | Description                                                 |
| -------- | -------- | -------------- | ----------------------------------------------------------- |
| storage  | false    | "localStorage" | Choose the storage type, "localStorage" or "sessionStorage" |

## API

The API of typed-local-store mimics the Storage API except for one exception, the Storage APIs length property is implemented as a method.

### getItem

The `getItem` method has three retrieval modes, whereas `'fail'` is the default mode

| Mode | Description                                                                                      |
| ---- | ------------------------------------------------------------------------------------------------ |
| fail | If a something to be restored from the store can not be parsed by `JSON.parse` a error is thrown |
| raw  | If parsing of the retrieval value fails, the unparsed value is returned                          |
| safe | If parsing of the retrieval value fails, `null` is returned                                      |
