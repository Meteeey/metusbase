# metusbase
This package is an NPM module that makes using JSON and Mongo fast, secure and easy

_____________________________________________________________________________________________________________

```
npm install metusbase

or

pnpm install metusbase
```

_____________________________________________________________________________________________________________

Developers: [Mete](https://github.com/Meteeey) [Ibrahim](https://github.com/softyagmur)

Support: https://discord.gg/medya

NPM Page: https://www.npmjs.com/metusbase

_____________________________________________________________________________________________________________

# 🏅 Example Usage

**CommonJS:**

```js
const { Database, MongoDatabase } = require("metusbase");
const mongoose = require("mongoose");
```

**ESM:**

```js
import { Database, MongoDatabase } from "metusbase";
import mongoose from "mongoose";
```

# 📦 Database settings (JSON)

```ts
const db = new Database("path.json"); // not required

db.set("key.object1.object2", "value"); // result: { key: { object1: { object2: "value" } } }
db.add("key", "value"); // result: { key: { list: ["item"] } }

db.get("key"); // result: { object1: { object2: "value" } }
db.get("key.object1"); // result: { object2: "value" }
db.get("key.object1.object2"); // result: "value"
db.getAll(); // result: { key: { object1: { object2: "value" } } } => all keys

db.push("key.array", "value1"); // result: { key: { array: ["value1"] } }
db.push("key.array", "value2"); // result: { key: { array: ["value1", "value2"] } }
db.unpush("key.array", "value1"); // result: { key: { array: ["value2"] } }
db.unpush("key.array"); // result: { key: {} } removes the entire array

db.has("key.object1.object2"); // result: true
db.delete("key.object1.object2"); // result: { key: { object1: {} } }
db.delete("key.object1"); // result: { key: {} }
db.delete("key"); // result: {}
db.deleteAll(
  "You are fully responsible for the data in your project. This data will be deleted. Do you confirm? (I confirm)"
); // result: {} => deletes all data in the database
```
# 📦 Database settings (Mongo)
```ts
const db = new MongoDatabase();

const mongo = "mongodburl";
(async () => {
  await mongoose
    .connect(mongo)
    .then(() => {
      console.log("Mongodb connection successful!");
    })
    .catch((e) => {
      console.error(e);
    });
})();

(async () => {
  db.set("key", "mete52"); // result: {value: "mete52"}
  db.set("key2", { name: "mete52", age: 21 }); // result: {"value": {name:"mete52",age:21}}

  await db.get("key"); // result: mete52
  await db.get("key2"); // result: {name:"mete52",age:21}
  await db.getAll(); // result: {key:"mete52",key2:{name:"mete52",age:21}}

  db.push("newKey", "value1"); // result: ["value1"]
  db.unpush("newKey"); // result: []
  db.unpush("newKey", "value1"); // result []

  db.has("key"); // result: true
  db.delete("key"); // result: {}
  db.delete("key2"); // result: {}
  db.deleteAll(
    "Projenizdeki verilerden tamamen siz sorumlusunuz. Bu veriler silinecektir. Onaylıyor musunuz? (onaylıyorum)"
  ); // result: {} => deletes all data in the database
})();
```


_____________________________________________________________________________________________________________

🛡️ Telif Hakkı ve Lisans

Projenin içeriğinin veya görsellerin izinsiz kopyalanması, yeniden dağıtılması veya herhangi bir şekilde kullanılması yasaktır. Tespit edilmesi durumunda gerekli yasal işlemler başlatılır.

_____________________________________________________________________________________________________________
