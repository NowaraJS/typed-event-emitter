# 🎯 TypedEventEmitter

## 📌 Table of Contents

- [🎯 TypedEventEmitter](#-typedeventemitter)
  - [📌 Table of Contents](#-table-of-contents)
  - [📝 Description](#-description)
  - [✨ Features](#-features)
  - [🔧 Installation](#-installation)
  - [⚙️ Usage](#-usage)
  - [📚 API Reference](#-api-reference)
  - [⚖️ License](#-license)
  - [📧 Contact](#-contact)

## 📝 Description

> A TypeScript library that provides a strongly typed event emitter for type-safe event handling.

**TypedEventEmitter** extends `EventEmitter` with full TypeScript support, allowing developers to define custom events with specific payloads while ensuring complete type safety and reducing runtime errors in event-driven applications.

## ✨ Features

- 🔒 **Type Safety**: Full TypeScript support with strongly typed event names and payloads
- 🧩 **Generic Design**: Define custom event maps for your specific use cases
- 🔄 **Familiar API**: Extends Node.js EventEmitter with the same familiar methods
- 📦 **Zero Dependencies**: No external runtime dependencies
- 🚀 **Modern**: Built with modern TypeScript and supports ESM
- 🧪 **Well Tested**: Comprehensive test suite included

## 🔧 Installation

```bash
bun add @nowarajs/typed-event-emitter
```

## ⚙️ Usage

### Basic Usage

```typescript
import { TypedEventEmitter } from '@nowarajs/typed-event-emitter';

// Define your event map
interface MyEvents {
  userLogin: [{ userId: string; timestamp: Date }];
  userLogout: [{ userId: string }];
  dataUpdate: [{ id: number; data: any }];
  error: [Error];
}

// Create a typed event emitter
const emitter = new TypedEventEmitter<MyEvents>();

// Type-safe event listening
emitter.on('userLogin', (payload) => {
  // payload is automatically typed as { userId: string; timestamp: Date }
  console.log(`User ${payload.userId} logged in at ${payload.timestamp}`);
});

// Type-safe event emission
emitter.emit('userLogin', { 
  userId: 'user123', 
  timestamp: new Date() 
});
```

### Advanced Usage

```typescript
import { TypedEventEmitter } from '@nowarajs/typed-event-emitter';

// Multiple parameters
interface Events {
  move: [x: number, y: number];
  click: [button: 'left' | 'right', x: number, y: number];
  keypress: [key: string, modifiers: string[]];
}

const input = new TypedEventEmitter<Events>();

// Multiple parameters are fully typed
input.on('move', (x, y) => {
  console.log(`Mouse moved to ${x}, ${y}`);
});

input.on('click', (button, x, y) => {
  console.log(`${button} click at ${x}, ${y}`);
});

// Emit with multiple arguments
input.emit('move', 100, 200);
input.emit('click', 'left', 50, 75);
```

## 📚 API Reference

The `TypedEventEmitter` class extends Node.js's `EventEmitter` with the following typed methods:

### Methods

- `emit<K>(event: K, ...args: Events[K]): boolean` - Emit a typed event
- `on<K>(event: K, listener: (...args: Events[K]) => void): this` - Add a typed event listener
- `once<K>(event: K, listener: (...args: Events[K]) => void): this` - Add a one-time typed event listener
- `off<K>(event: K, listener: (...args: Events[K]) => void): this` - Remove a typed event listener
- `addListener<K>(event: K, listener: (...args: Events[K]) => void): this` - Alias for `on`
- `removeListener<K>(event: K, listener: (...args: Events[K]) => void): this` - Alias for `off`
- `listenerCount<K>(event: K): number` - Get the number of listeners for an event
- `listeners<K>(event: K): ((...args: Events[K]) => void)[]` - Get all listeners for an event
- `rawListeners<K>(event: K): ((...args: Events[K]) => void)[]` - Get raw listeners for an event
- `prependListener<K>(event: K, listener: (...args: Events[K]) => void): this` - Add listener to beginning
- `prependOnceListener<K>(event: K, listener: (...args: Events[K]) => void): this` - Add one-time listener to beginning

All methods provide full TypeScript intellisense and compile-time type checking.

## ⚖️ License

Distributed under the MIT License. See [LICENSE](./LICENSE) for more information.

## 📧 Contact

NowaraJS - [GitHub Organization](https://github.com/NowaraJS)

[Project Link](https://github.com/NowaraJS/typed-event-emitter)

