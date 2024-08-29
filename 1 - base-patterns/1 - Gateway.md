# Gateway
An object that encapsulates access to an external system or resource

## Problem)

```javascript
function createCustomer(apiKey, name) {
    return fetch('payment-gateway/create-customer', {
        headers: {
            'Content-Type': 'application/json',
            'api-key': apiKey
        },
        body: { name }
    });
}

function pay(apiKey, customer, value) {
    return fetch('payment-gateway/pay', {
        headers: {
            'Content-Type': 'application/json',
            'api-key': apiKey
        },
        body: { customer, value }
    });
}

(async () => {
    const myApiKey = 'foo';

    const customer = await createCustomer(myApiKey, 'Deividy');
    await pay(myApiKey, customer, value);
});

```

Como podemos implementar essa solução de forma que o nosso código
fique todo acoplado em um único lugar, de fácil acesso e entendimento?
