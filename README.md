# MongoDb
Microsoft Windows [Version 10.0.26100.4061]
(c) Microsoft Corporation. All rights reserved.

C:\Users\Minfy>mongosh
Current Mongosh Log ID: 6836e9bda4c0f239826c4bcf
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.5.1
Using MongoDB:          8.0.9
Using Mongosh:          2.5.1

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/

------
   The server generated these startup warnings when booting
   2025-05-28T12:30:11.787+05:30: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
------

test> show dbs
Todo         144.00 KiB
admin         40.00 KiB
config       108.00 KiB
fatherFamiy   72.00 KiB
local         40.00 KiB
test> use Todo
switched to db Todo
Todo> use todoApp;
...
... db.createCollection("todoLists", {
...   validator: {
...     $jsonSchema: {
...       bsonType: "object",
...       required: ["title", "createdAt", "tasks"],
...       properties: {
...         title: {
...           bsonType: "string"
...         },
...         createdAt: {
...           bsonType: "date"
...         },
...         tasks: {
...           bsonType: "array",
...           items: {
...             bsonType: "object",
...             required: ["title", "status"],
...             properties: {
...               title: { bsonType: "string" },
...               description: { bsonType: "string" },
...               status: { bsonType: "bool" }, // default will be set manually
...               dueDate: { bsonType: "date" },
...               priority: { enum: ["low", "medium", "high"] }
...             }
...           }
...         }
...       }
...     }
...   }
... });
...
switched to db todoApp;
todoApp;> show collections

todoApp;> use todoApp;
...
... db.todoApp.createCollection("todoLists", {
...   validator: {
...     $jsonSchema: {
...       bsonType: "object",
...       required: ["title", "createdAt", "tasks"],
...       properties: {
...         title: {
...           bsonType: "string"
...         },
...         createdAt: {
...           bsonType: "date"
...         },
...         tasks: {
...           bsonType: "array",
...           items: {
...             bsonType: "object",
...             required: ["title", "status"],
...             properties: {
...               title: { bsonType: "string" },
...               description: { bsonType: "string" },
...               status: { bsonType: "bool" }, // default will be set manually
...               dueDate: { bsonType: "date" },
...               priority: { enum: ["low", "medium", "high"] }
...             }
...           }
...         }
...       }
...     }
...   }
... });
...
already on db todoApp;
todoApp;> show collections

todoApp;> db.todApp.find({})

todoApp;> db.todoLists.insertOne({
...   title: "Wednesday Tasks",
...   createdAt: new Date(),
...   tasks: [
...     {
...       _id: ObjectId(),  // generate a unique ID manually
...       title: "Read a book",
...       description: "Read 20 pages of a novel",
...       status: false,
...       dueDate: new Date("2025-06-01"),
...       priority: "low"
...     },
...     {
...       _id: ObjectId(),
...       title: "Workout",
...       description: "30 minutes cardio",
...       status: false,
...       dueDate: new Date("2025-06-01"),
...       priority: "medium"
...     }
...   ]
... });
...
{
  acknowledged: true,
  insertedId: ObjectId('6836eae0a4c0f239826c4bd2')
}
todoApp;> db.todoLists.updateOne(
...   { "tasks._id": ObjectId("66562564d66fd3a5ebea1234") },
...   { $set: { "tasks.$.status": true } }
... );
...
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
todoApp;> db.todoLists.find({ "tasks._id": ObjectId("66562564d66fd3a5ebea1234") }).pretty();

todoApp;> db.todoLists.find({})
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  }
]
todoApp;> use todoApp;
...
... db.createCollection("todoLists", {
...   validator: {
...     $jsonSchema: {
...       bsonType: "object",
...       required: ["title", "createdAt", "updatedAt", "tasks"],
...       properties: {
...         title: { bsonType: "string" },
...         createdAt: { bsonType: "date" },
...         updatedAt: { bsonType: "date" },
...         tasks: {
...           bsonType: "array",
...           items: {
...             bsonType: "object",
...             required: ["title", "status", "createdAt", "updatedAt"],
...             properties: {
...               _id: { bsonType: "objectId" },
...               title: { bsonType: "string" },
...               description: { bsonType: "string" },
...               status: { bsonType: "bool" },
...               dueDate: { bsonType: "date" },
...               priority: { enum: ["low", "medium", "high"] },
...               createdAt: { bsonType: "date" },
...               updatedAt: { bsonType: "date" }
...             }
...           }
...         }
...       }
...     }
...   }
... });
...
already on db todoApp;
todoApp;> db.todoLists.insertOne({
...   title: "Thursday Tasks",
...   createdAt: new Date(),
...   updatedAt: new Date(),
...   tasks: [
...     {
...       _id: ObjectId(),
...       title: "Learn MongoDB",
...       description: "Watch tutorial videos",
...       status: false,
...       dueDate: new Date("2025-06-05"),
...       priority: "medium",
...       createdAt: new Date(),
...       updatedAt: new Date()
...     },
...     {
...       _id: ObjectId(),
...       title: "Go jogging",
...       description: "Jog for 30 minutes",
...       status: false,
...       dueDate: new Date("2025-06-05"),
...       priority: "high",
...       createdAt: new Date(),
...       updatedAt: new Date()
...     }
...   ]
... });
...
{
  acknowledged: true,
  insertedId: ObjectId('6836ebb5a4c0f239826c4bd5')
}
todoApp;> const taskId = ObjectId("PUT_YOUR_TASK_OBJECTID_HERE");
...
... db.todoLists.updateOne(
...   { "tasks._id": taskId },
...   {
...     $set: {
...       "tasks.$.status": true,
...       "tasks.$.updatedAt": new Date(),
...       updatedAt: new Date()   // update the parent document updatedAt too
...     }
...   }
... );
...
BSONError: input must be a 24 character hex string, 12 byte Uint8Array, or an integer
todoApp;> todoApp;> const taskId = ObjectId("6836ebb5a4c0f239826c4bd5'");
... ...
... ... db.todoLists.updateOne(
... ...   { "tasks._id": taskId },
... ...   {
... ...     $set: {
... ...       "tasks.$.status": true,
... ...       "tasks.$.updatedAt": new Date(),
... ...       updatedAt: new Date()   // update the parent document updatedAt too
... ...     }
... ...   }
... ... );
... ...
... BSONError: input must be a 24 character hex string, 12 byte Uint8Array, or an integer
... todoApp;>
Uncaught:
SyntaxError: Unexpected token (1:8)

> 1 | todoApp;> const taskId = ObjectId("6836ebb5a4c0f239826c4bd5'");
    |         ^
  2 | ...
  3 | ... db.todoLists.updateOne(
  4 | ...   { "tasks._id": taskId },

todoApp;> todoApp;> const taskId = ObjectId("6836ebb5a4c0f239826c4bd5'");
... ...
... ... db.todoLists.updateOne(
... ...   { "tasks._id": taskId },
... ...   {
... ...     $set: {
... ...       "tasks.$.status": true,
... ...       "tasks.$.updatedAt": new Date(),
... ...       updatedAt: new Date()   // update the parent document updatedAt too
... ...     }
... ...   }
... ... );
... ...
... BSONError: input must be a 24 character hex string, 12 byte Uint8Array, or an integer
... todoApp;>
Uncaught:
SyntaxError: Unexpected token (1:8)

> 1 | todoApp;> const taskId = ObjectId("6836ebb5a4c0f239826c4bd5'");
    |         ^
  2 | ...
  3 | ... db.todoLists.updateOne(
  4 | ...   { "tasks._id": taskId },

todoApp;>
...  db.todoLists.updateOne(
...    { "tasks._id": "6836ebb5a4c0f239826c4bd5" },
...    {
...      $set: {
...        "tasks.$.status": true,
...        "tasks.$.updatedAt": new Date(),
...        updatedAt: new Date()   // update the parent document updatedAt too
...      }
...    }
...  );
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
todoApp;> db.todoLists.find({})
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T10:55:49.464Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      }
    ]
  }
]
todoApp;> ...  db.todoLists.updateOne(
... ...    { "tasks._id": "6836ebb5a4c0f239826c4bd5" },
... ...    {
... ...      $set: {
... ...        "tasks.$.status": true,
... ...        "tasks.$.updatedAt": new Date(),
... ...        updatedAt: new Date()   // update the parent document updatedAt too
... ...      }
... ...    }
...
Uncaught:
SyntaxError: Unexpected token (1:0)

> 1 | ...  db.todoLists.updateOne(
    | ^
  2 | ...    { "tasks._id": "6836ebb5a4c0f239826c4bd5" },
  3 | ...    {
  4 | ...      $set: {

todoApp;> db.todoLists.updateOne(
... {
... "tasks._id":"683ebb5a4c0f239826c4bd5"},
... {
... $set:{
... "tasks.$.status
Uncaught:
SyntaxError: Unterminated string constant. (6:0)

  4 | {
  5 | $set:{
> 6 | "tasks.$.status
    | ^
  7 |

todoApp;> db.todoLists.updateOne( { "tasks._id":"683ebb5a4c0f239826c4bd5"}, { $set:{ "tasks.$.status":false,"tasks.$.updatedAt":new DDate(),updatedAt:new Date()}}
...
... }
Uncaught:
SyntaxError: Unexpected token, expected "," (3:0)

  1 | db.todoLists.updateOne( { "tasks._id":"683ebb5a4c0f239826c4bd5"}, { $set:{ "tasks.$.status":false,"tasks.$.updatedAt":new Date(),updatedAt:new Date()}}
  2 |
> 3 | }
    | ^
  4 |

todoApp;> db.todoLists.updateOne( { "tasks._id":"683ebb5a4c0f239826c4bd5"}, { $set:{ "tasks.$.status":false,"tasks.$.updatedAt":new Date(),updatedAt:new Date()}} )
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
todoApp;> db.todoLists.find({})
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T10:55:49.464Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      }
    ]
  }
]
todoApp;> db.todoLists.updateOne( { "tasks._id":"683ebb5a4c0f239826c4bd5"}, { $set:{ "tasks.$.status":false,"tasks.$.updatedAt":new Date()} )
Uncaught:
SyntaxError: Unexpected token, expected "," (1:130)

> 1 | db.todoLists.updateOne( { "tasks._id":"683ebb5a4c0f239826c4bd5"}, { $set:{ "tasks.$.status":false,"tasks.$.updatedAt":new Date()} )
    |                                                                                                                                   ^
  2 |

todoApp;> db.todoLists.updateOne( { "tasks._id":"683ebb5a4c0f239826c4bd5"}, { $set:{ "tasks.$.status":false,"tasks.$.updatedAt":new Date()}} )
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
todoApp;> db.todoLists.find({})
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T10:55:49.464Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      }
    ]
  }
]
todoApp;> db.todoLists.updateOne( { "tasks._id":"683ebb5a4c0f239826c4bd5"}, { $set:{ "tasks.$.status":true,"tasks.$.updatedAt":new Date()}} )
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
todoApp;> db.todoLists.find({})
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T10:55:49.464Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      }
    ]
  }
]
todoApp;> db.todoLists.updateOne( { "tasks._id":"683ebb5a4c0f239826c4bd3"}, { $set:{ "tasks.$.status":true,"tasks.$.updatedAt":new Date()}} )
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
todoApp;> db.todoLists.updateOne( { "tasks._id":'6836ebb5a4c0f239826c4bd4'}, { $set:{ "tasks.$.status":true,"tasks.$.updatedAt":new DDate()}} )
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
todoApp;> db.todoLists.find({})
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T10:55:49.464Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      }
    ]
  }
]
todoApp;> db.todoLists.updateOne( { "tasks.$._id":'6836ebb5a4c0f239826c4bd4'}, { $set:{ "tasks.$.status":true,"tasks.$.updatedAt":new Date()}} )
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
todoApp;> db.todoLists.updateOne( { "tasks.$._id":'6836ebb5a4c0f239826c4bd4'}, { $set:{ "tasks.$.statdb.todoLists.updateOne({ "tasks._id": ObjectId("6836ebb5a4c0f239826c4bd4") }, { $set: { "tasks.$.status": true, "tasks.$.updatedAt": new Date(), updatedAt: new Date() } });us":true,"tasks.$.updatedAt":new Date()}} )
Uncaught:
SyntaxError: Unexpected token (1:117)

> 1 | db.todoLists.updateOne( { "tasks.$._id":'6836ebb5a4c0f239826c4bd4'}, { $set:{ "tasks.$.statdb.todoLists.updateOne({ "tasks._id": ObjectId("6836ebb5a4c0f239826c4bd4") }, { $set: { "tasks.$.status": true, "tasks.$.updatedAt": new Date(), updatedAt: new Date() } });us":true,"tasks.$.updatedAt":new Date()}} )
    |                                                                                                                      ^
  2 |

todoApp;> db.todoLists.updateOne({ "tasks._id": ObjectId("6836ebb5a4c0f239826c4bd4") }, { $set: { "tasks.$.status": true, "tasks.$.updatedAt": new Date(), updatedAt: new Date() } });
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
todoApp;> db.todoLists.find({})
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T11:13:08.336Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: true,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T11:13:08.336Z')
      }
    ]
  }
]
todoApp;> db.todoLists.countDocuments();
2
todoApp;> db.todoLists.find().sort({ title: 1 }).pretty();
[
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T11:13:08.336Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: true,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T11:13:08.336Z')
      }
    ]
  },
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  }
]
todoApp;> db.todoLists.find().sort({}).pretty();
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T11:13:08.336Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: true,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T11:13:08.336Z')
      }
    ]
  }
]
todoApp;> db.todoLists.find().sort({status:true}).pretty();
MongoInvalidArgumentError: Invalid sort direction: true
todoApp;> db.todoLists.find().sort({status:1}).pretty();
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T11:13:08.336Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: true,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T11:13:08.336Z')
      }
    ]
  }
]
todoApp;> db.todoLists.find().sort({status:0}).pretty();
MongoInvalidArgumentError: Invalid sort direction: 0
todoApp;> db.todoLists.find().sort({status:1}).pretty();
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ]
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T11:13:08.336Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: true,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T11:13:08.336Z')
      }
    ]
  }
]
todoApp;> db.todoLists.updateMany(
...   {},
...   { $set: { date: new Date() } }
... );
...
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 2,
  upsertedCount: 0
}
todoApp;> db.todoLists.find({})
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ],
    date: ISODate('2025-05-28T11:20:08.694Z')
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T11:13:08.336Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: true,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T11:13:08.336Z')
      }
    ],
    date: ISODate('2025-05-28T11:20:08.694Z')
  }
]
todoApp;> db.todoLists.find({ createdAt: { $gte: new Date(Date.now() - 20 * 60 * 1000) } }).pretty();

todoApp;> db.todoLists.find({ createdAt: { $lte: new Date(Date.now() - 20 * 60 * 1000) } }).pretty();
[
  {
    _id: ObjectId('6836eae0a4c0f239826c4bd2'),
    title: 'Wednesday Tasks',
    createdAt: ISODate('2025-05-28T10:52:16.839Z'),
    tasks: [
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd0'),
        title: 'Read a book',
        description: 'Read 20 pages of a novel',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'low'
      },
      {
        _id: ObjectId('6836eae0a4c0f239826c4bd1'),
        title: 'Workout',
        description: '30 minutes cardio',
        status: false,
        dueDate: ISODate('2025-06-01T00:00:00.000Z'),
        priority: 'medium'
      }
    ],
    date: ISODate('2025-05-28T11:20:08.694Z')
  },
  {
    _id: ObjectId('6836ebb5a4c0f239826c4bd5'),
    title: 'Thursday Tasks',
    createdAt: ISODate('2025-05-28T10:55:49.464Z'),
    updatedAt: ISODate('2025-05-28T11:13:08.336Z'),
    tasks: [
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd3'),
        title: 'Learn MongoDB',
        description: 'Watch tutorial videos',
        status: false,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'medium',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T10:55:49.464Z')
      },
      {
        _id: ObjectId('6836ebb5a4c0f239826c4bd4'),
        title: 'Go jogging',
        description: 'Jog for 30 minutes',
        status: true,
        dueDate: ISODate('2025-06-05T00:00:00.000Z'),
        priority: 'high',
        createdAt: ISODate('2025-05-28T10:55:49.464Z'),
        updatedAt: ISODate('2025-05-28T11:13:08.336Z')
      }
    ],
    date: ISODate('2025-05-28T11:20:08.694Z')
  }
]
todoApp;>
