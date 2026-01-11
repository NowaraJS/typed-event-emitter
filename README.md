# 🎯 NowaraJS Typed Event Emitter

Working with `EventEmitter` in TypeScript is painful. You get zero autocomplete, typos in event names fail silently, and your listeners accept `any` because the types don't flow through. I built this to fix that.

## Why this package?

The goal is simple: **Make event-driven code actually type-safe.**

This package wraps `EventEmitter` so that every event name and payload is validated at compile time. No more guessing, no more runtime surprises.

## 📌 Table of Contents

- [Features](#-features)
- [Installation](#-installation)
- [Usage](#-usage)
- [API Reference](#-api-reference)
- [License](#-license)
- [Contact](#-contact)

## ✨ Features

- 🔒 **Full Type Safety**: Event names and payloads are checked at compile time.
- 🧩 **Generic Design**: Define your own event maps for any use case.
- 🔄 **Familiar API**: Same `on`, `emit`, `once` you already know.
- 📦 **Zero Dependencies**: Pure TypeScript, nothing else.

## 🔧 Installation

```bash
bun add @nowarajs/typed-event-emitter
```

## ⚙️ Usage

### Basic Usage

Define an event map interface, then pass it to `TypedEventEmitter`. Everything flows from there.

```ts
import { TypedEventEmitter } from '@nowarajs/typed-event-emitter';

interface MyEvents {
    userLogin: [{ userId: string; timestamp: Date }];
    userLogout: [{ userId: string }];
    error: [Error];
}

const emitter = new TypedEventEmitter<MyEvents>();

// `payload` is inferred as { userId: string; timestamp: Date }
emitter.on('userLogin', (payload) => {
    console.log(`User ${payload.userId} logged in at ${payload.timestamp}`);
});

// TypeScript will yell if you pass the wrong shape
emitter.emit('userLogin', { 
    userId: 'user123', 
    timestamp: new Date() 
});
```

### Multiple Parameters

Events can have multiple arguments, and each one is typed individually.

```ts
import { TypedEventEmitter } from '@nowarajs/typed-event-emitter';

interface Events {
    move: [x: number, y: number];
    click: [button: 'left' | 'right', x: number, y: number];
}

const input = new TypedEventEmitter<Events>();

// x and y are both numbers
input.on('move', (x, y) => {
    console.log(`Mouse moved to ${x}, ${y}`);
});

// button is 'left' | 'right', x and y are numbers
input.on('click', (button, x, y) => {
    console.log(`${button} click at ${x}, ${y}`);
});

input.emit('move', 100, 200);
input.emit('click', 'left', 50, 75);
```

## 📚 API Reference

Full docs: [nowarajs.github.io/typed-event-emitter](https://nowarajs.github.io/typed-event-emitter/)

## ⚖️ License

MIT - Feel free to use it.

## 📧 Contact

- Mail: [nowarajs@pm.me](mailto:nowarajs@pm.me)
- GitHub: [NowaraJS](https://github.com/NowaraJS)
