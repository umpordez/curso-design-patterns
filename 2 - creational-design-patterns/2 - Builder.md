# Builder
Separate the construction of a complex object from its representation
allowing the same construction process to create various representations.

## Problem)

```javascript
class Order {
    constructor({ customer, address }) {
        this.customer = customer;
        this.address = address;
    }

    pay(creditCardId, value) {
        const creditCard = await this.db.credit_cards.oneRow({
            id: creditCardId
        });

        const order = await this.db.orders.insert({ customer, value });

        await this.paymentGateway.pay({
            orderId: order.id
            customer: this.customer,
            creditCard,
            value
        });
    }
}

const customer = await db.customers.oneRow({ id: customerId });
const order = new Order({ customer });

await order.pay(123, 100);
```

Como podemos aplicar o pattern de modo a não duplicar o nosso código?

## Solution)

```javascript
class Order {
    async buildCustomer(customerId) {
        this.customer = await this.db.customers.oneRow({ id: customerId });
        this.buildAddress(customerId);
    }

    async buildAddress(customerId) {
        this.address = await this.db.addresses.where({ customerId });
    }

    async buildCreditCard(creditCardId) {
        this.creditCard = await this.db.credit_cards.oneRow({
            id: creditCardId
        });
    }

    async buildOrder(value) {
        this.order = await this.db.orders
            .insert({ customer: this.customer, value });
    }

    pay() {
        await this.paymentGateway.pay({
            orderId: this.order.id
            customer: this.customer,
            creditCard: this.creditCard,
            value: this.order.value
        });
    }
}

const order = new Order();

await order.buildCustomer(customer.id);
await order.buildOrder(100);
await order.pay();
```
