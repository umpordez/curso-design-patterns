# Registry
A well-known object that other objects can use to find common objects and
services.

## Problem)

`webhook.js`
```
import fs from 'node:fs';

function getFee() {
    return fs.readFileSync('fee').toString();
}

function receivePayment(payment) {
    payment.fee = getFee();
    return payment;
}

```

`orders.js`
```
import fs from 'node:fs';

function getFee() {
    return fs.readFileSync('fee').toString();
}

function pay(value) {
    const fee = getFee();
    return fetch('foo-bar', { fee, value };
}
```
