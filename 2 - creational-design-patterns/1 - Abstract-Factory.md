# Abstract Factory
Provides an interface for creating families of related or dependent objects
without specifying their concrete classes.

## Problem)

```javascript
class PaypalCustomer {
    create(name) {
        return fetch('paypal/customer/create', { name });
    }
}

// abstract class
class PaymentGateway {
    get _endpointUrl() { throw new Error('Not implemented'); }

    pay(customer, value) {
        await this.recordEvent('start-payment', { value });
        const order = await this.db.orders.insert({ value });

        const res = fetch(this._endpointUrl, { customer, value });

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
    get _endpointUrl() { return 'paypal/pay'; }
}

class PagseguroCustomer {
    create(name) {
        return fetch('pagseguro/customer/create', { name });
    }
}

class PagseguroPaymentGateway extends PaymentGateway {
    get _endpointUrl() { return 'pagseguro/pay'; }
}

class PaypalOrderModel {
    createPaymentCustomerInstance() {
        return new PaypalCustomer();
    }

    createPaymentGatewayInstance() {
        return PaypalGateway();
    }
}

class PagseguroOrderModel {
    createPaymentCustomerInstance() {
        return new PagseguroCustomer();
    }

    createPaymentGatewayInstance() {
        return PagseguroPaymentGateway();
    }
}

class OrderModel {
    constructor(gateway) {
        this.gateway = gateway;
    }

    get gatewayOrderModel () {
        if (this.gateway === 'pagseguro') {
            return new PagseguroOrderModel();
        }

        return new PaypalOrderModel();
    }

    pay(name, value) {
        const gatewayOrderModel = this.gatewayOrderModel;

        const customerInstance = gatewayOrderModel
            .createPaymentCustomerInstance(gateway);

        await customerInstance.create(name);

        const paymentGatewayInstance = gatewayOrderModel
            .createPaymentGatewayInstance(gateway);

        await paymentGatewayInstance.pay(customerInstance, value);
    }
}

app.post('/pay', async (req, res) => {
    const { value, name, gateway } = req.body;

    const order = new OrderModel(gateway);
    await order.pay(name, value);
});
```

Como podemos aplicar o pattern de modo a não duplicar o nosso código?

## Solution)

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
    _doPayOnGateway(value) {
        return fetch('paypal/pay', { value });
    }
}

class PagseguroGateway extends PaymentGateway {
    _doPayOnGateway(value) {
        return fetch('pagseguro/pay', { value });
    }
}

const instance = gateway === 'pagseguro' ? new PagseguroGateway() :
    new PaypalGateway();

await instance.pay(100);
```
