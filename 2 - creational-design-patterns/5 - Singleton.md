# Singleton
Ensures a class has only one instance, and provides a global point of
access to it.

## Problem)

```javascript
class Database {
    constructor(config) {
        const knex = knexModule({ config });
    }

    execute(stmt) { return knex.raw(stmt); }
}


const config = require('./config');
app.get('/users', async () => {
    const db = new Database(config)
    const users = await db.execute('select * from users');

    res.status(200).json({ users });
});

app.get('/'accounts, async () => {
    const db = new Database(config)
    const accounts = await db.execute('select * from accounts');

    res.status(200).json({ accounts });
});
```

## Solution)

```javascript

let _database;
class Database {
    constructor(config) {
        const knex = knexModule({ config });
    }

    static getInstance() { return _database; }
    execute(stmt) { return knex.raw(stmt); }
}

const config = require('./config');
(() => {
    _database = new Database(config);
});

app.get('/users', async () => {
    const db = Database.getInstance();
    const users = await db.execute('select * from users');

    res.status(200).json({ users });
});

app.get('/'accounts, async () => {
    const db = Database.getInstance();
    const accounts = await db.execute('select * from accounts');

    res.status(200).json({ accounts });
});
