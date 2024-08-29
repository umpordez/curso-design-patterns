# Mapper
An object that sets up a communication between two independent objects.

## Problem)

```javascript

const pricingMap = {
    100: { intallment: 1, fee: 0.5 },
    200: { intallment: 2, fee: 0.7 },
    300: { intallment: 3, fee: 1 }
};

function pay(value) {
    let fee = 0;
    let installment = 0;

    if (value === 100) {
        fee = 0.5;
        installment = 1;
    }

    if (value === 200) {
        fee = 0.7;
        installment = 2;
    }

    if (value === 300) {
        fee = 1;
        installment = 3;
    }

    return axios('payment', { fee, installment, value });
}

(async () => {
    await pay(200);
});

```
