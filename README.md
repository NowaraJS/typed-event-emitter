# 🎯 NowaraJS - TypedEventEmitter

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
- 🔄 **Familiar API**: Extends EventEmitter with the same familiar methods
- 📦 **Zero Dependencies**: 0 dependencies

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

You can find the complete API reference documentation for `TypedEventEmitter` at:

- [Reference Documentation](https://nowarajs.github.io/typed-event-emitter/)

## ⚖️ License

Distributed under the MIT License. See [LICENSE](./LICENSE) for more information.

## 📧 Contact

- GitHub: [NowaraJS](https://github.com/NowaraJS)
- Package: [@nowarajs/typed-event-emitter](https://www.npmjs.com/package/@nowarajs/typed-event-emitter)


