# Factory Method
Define an interface for creating an object, but lets subclasses decide which
class to instantiate.

## Problem)

```javascript
class PaymentGateway {
    _doPayOnGateway(value) { throw new Error('Not Implemented'); }

    pay(value) {
        await this.recordEvent('start-payment', { value });
        const order = await this.db.orders.insert({ value });

        const res = this._doPayOnGateway(value);

        await this.db
            .orders
            .update({ gateway_id: res.id })
            .where({ id: order.id });

        await this.recordEvent('payment-done', { value });
        return order;
    }

    recordEvent(eventName, obj) {
        await this.db.events.insert({ eventName, obj });
    }
}

class PaypalGateway extends PaymentGateway {
    _doPayOnGateway(value) { return fetch('paypal/pay', { value }); }
}

class PagseguroGateway extends PaymentGateway {
    _doPayOnGateway(value) { return fetch('pagseguro/pay', { value }); }
}

class StripeGateway extends PaymentGateway {
    _doPayOnGateway(value) { return fetch('stripe/pay', { value }); }
}

const instance = gateway === 'pagseguro' ? new PagseguroGateway() :
    gateway === 'stripe' ? new StripeGateway() : new PaypalGateway();

await instance.pay(100);
```

Como podemos aplicar o pattern de modo a não duplicar o nosso código?

## Solution)

```javascript
// ...
function getPaymentGateway(paymentGateway) {
    const ClassByPaymentGateway = {
        paypal: PaypalGateway,
        pagseguro: PagseguroGateway,
        stripe: StripeGateway
    };

    return new ClassByPaymentGateway[PaymentGateway]();
}

const instance = getPaymentGateway(paymentGateway);
await instance.pay(100);
```
