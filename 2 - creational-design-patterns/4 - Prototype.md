# Prototype
Specify the kinds of objects to create using a prototypical instance, and
create new objects by copying this prototype.

## Problem)

```javascript

class Appointment {
    constructor(customer, date) {
        this.customer = customer;
        this.date = date;
    }

    setFee(fee) { this.fee = fee; }

    async create() {
        await fetch('customer', {
            method: 'post',
            body: {
                fee: this.fee,
                customer: this.customer,
                date: this.date
            }
        });
    }
}

(async () => {
    const date = new Date();
    const customer = { name: 'Deividy' };

    const firstAppointment = new Appointment(customer, date);
    firstAppointment.setFee(10);

    await firstAppointment.create();

    const secondAppointment = new Appointment(customer, date);
    secondAppointment.setFee(10);

    await secondAppointment.create();
}))();

```

## Solution)

```javascript

class Appointment {
    constructor(customer, date) {
        this.customer = customer;
        this.date = date;
    }

    setFee(fee) { this.fee = fee; }

    async create() {
        await fetch('customer', {
            method: 'post',
            body: {
                fee: this.fee,
                customer: this.customer,
                date: this.date
            }
        });
    }

    clone() {
        const appt = new Appointment(this.customer, this.date);
        appt.fee = this.fee;

        return appt;
    }
}

(async () => {
    const date = new Date();
    const customer = { name: 'Deividy' };

    const firstAppointment = new Appointment(customer, date);
    firstAppointment.setFee(10);

    await firstAppointment.create();

    const secondAppointment = firstAppointment.clone();
    await secondAppointment.create();
}))();
