# Adapter
Converts the interface of a class into another interface the clients expects.
Adapter lets classes work together that couldn’t otherwise because of
incompatible interfaces.

# Problem)
```javascript
const Pagseguro = require('pagseguro');
const Paypal = require('paypal');

function getPaymentGateway(gateway) {
    if (gateway === 'pagseguro') { return new Pagseguro(); }

    return new Paypal();
}

async function payOrder(gateway, customer, order, value) {
    const paymentGateway = getPaymentGateway(gateway);

    if (gateway === 'paypal') {
        await paymentGateway.payCard({ customer, order }, value);
    } else {
        await paymentGateway.pay(customer, order, value);
    }

}
```

# Solution
const Pagseguro = require('pagseguro');
const Paypal = require('paypal');

class PagseguroAdapter extends Pagseguro {
    pay({ customer, order, value }) {
        return super.pay(customer, order, value);
    }
}

class PaypalAdapter extends Pagseguro {
    pay({ customer, order, value }) {
        return super.payCard({ customer, order }, value);
    }
}

function getPaymentGateway(gateway) {
    if (gateway === 'pagseguro') { return new PagseguroAdapter(); }

    return new PaypalAdapter();
}

async function payOrder(gateway, customer, order, value) {
    const paymentGateway = getPaymentGateway(gateway);
    await paymentGateway.pay({ customer, order, value });
}
```
