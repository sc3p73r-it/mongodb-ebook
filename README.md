# MongoDB Deep Dive Ebook
---
MongoDB Documentation ကို အခြေခံပြီးတော့ MongoDB Deep Dive Ebook ကို Google Gemini Pro AI နဲ့ မြန်မာလို အသေးစိတ်ရေးသားထားပါတယ်။ ဒီ Ebook မှာ MongoDB ရဲ့ အခြေခံကနေစပြီး အဆင့်မြင့်တဲ့ အကြောင်းအရာတွေအထိ အခန်းလိုက်အခန်းလိုက် နားလည်လွယ်အောင် ရှင်းပြပေးသွားမှာ ဖြစ်ပါတယ်။

### MongoDB Deep Dive: မြန်မာလို လေ့လာကြမယ်
**မာတိကာ**
- အခန်း (၁): MongoDB နှင့် NoSQL Databases
    - [MongoDB ဆိုတာဘာလဲ?](/Chapter1.md)
    - [SQL vs NoSQL: ဘာတွေကွာခြားလဲ?](https://github.com/sc3p73r-it/mongodb-ebook/blob/main/Chapter1.md#sql-vs-nosql-%E1%80%98%E1%80%AC%E1%80%90%E1%80%BD%E1%80%B1%E1%80%80%E1%80%BD%E1%80%AC%E1%80%81%E1%80%BC%E1%80%AC%E1%80%B8%E1%80%9C%E1%80%B2)
    -MongoDB ရဲ့ အားသာချက်များ
    - JSON/BSON Data Model အကြောင်း

- အခန်း (၂): MongoDB Installation နှင့် Setup
  -[Windows, macOS, Linux တို့တွင် MongoDB ထည့်သွင်းခြင်း](/Chapter2.md)
  - MongoDB Shell (mongosh) ကို အသုံးပြုခြင်း
  - MongoDB Compass (GUI) နှင့် ချိတ်ဆက်ခြင်း

- အခန်း (၃): အခြေခံ CRUD Operations
  - Database, Collection များ တည်ဆောက်ခြင်း
  - Create: Document များ ထည့်သွင်းခြင်း (insertOne, insertMany)
  - Read: Document များ ရှာဖွေခြင်း (find, findOne)
  - Update: Document များ ပြင်ဆင်ခြင်း (updateOne, updateMany, replaceOne)
  - Delete: Document များ ဖျက်ခြင်း (deleteOne, deleteMany)

- အခန်း (၄): Data ရှာဖွေခြင်း (Querying) အဆင့်မြင့်
  - Query Operators (Comparison, Logical, Element, Evaluation)
  - $eq, $ne, $gt, $lt, $gte, $lte
  - $and, $or, $not, $nor
  - $in, $nin
  - Array များအတွင်း Query လုပ်ခြင်း
  - Projection: လိုအပ်တဲ့ Fields တွေပဲ ရွေးထုတ်ခြင်း

- အခန်း (၅): Indexing for Performance
  - Indexing ဆိုတာဘာလဲ? ဘာကြောင့်အရေးကြီးတာလဲ?
  - Single Field Index တည်ဆောက်ခြင်း
  - Compound Index တည်ဆောက်ခြင်း
  - Indexing Strategies နှင့် Best Practices

- အခန်း (၆): Aggregation Framework
  - Aggregation Pipeline ဆိုတာဘာလဲ?
  - အသုံးများသော Stages များ ($match, $group, $sort, $project, $limit, $skip)
  - လက်တွေ့ဥပမာများဖြင့် Aggregation အသုံးပြုပုံ

- အခန်း (၇): Data Modeling နှင့် Schema Design
  - Relational Data ကို MongoDB မှာ ဘယ်လိုသိမ်းမလဲ?
  - Embedding vs Referencing (Linking)
  - Schema Design Patterns (Attribute, Polymorphic, etc.)
  - One-to-One, One-to-Many, Many-to-Many Relationships

- အခန်း (၈): Mongoose (Node.js အတွက်)
  - Mongoose ဆိုတာဘာလဲ?
  - Schema နှင့် Model တည်ဆောက်ခြင်း
  - Mongoose ဖြင့် CRUD Operations များ ပြုလုပ်ခြင်း
  - Validation နှင့် Middleware အသုံးပြုပုံ

- နောက်ဆက်တွဲ
  - MongoDB Atlas (Cloud Database) အကြောင်း
  - Backup and Restore ပြုလုပ်ခြင်း