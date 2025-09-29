# အခန်း (၃): အခြေခံ CRUD Operations
CRUD ဆိုတာ data တွေကို Create, Read, Update, Delete လုပ်တာကို ဆိုလိုပါတယ်။ mongosh ကိုသုံးပြီး CRUD operations တွေကို လေ့လာကြည့်ပါမယ်။

အရင်ဆုံး`testDB`ဆိုတဲ့ database တစ်ခုကိုသုံးပြီး`users`ဆိုတဲ့ collection တစ်ခုနဲ့ အလုပ်လုပ်ပါမယ်။
```shell
// testDB ကို အသုံးပြုရန်
use testDB

// collection list ကို ကြည့်ရန်
show collections
```

#### Create: Document များထည့်သွင်းခြင်း
`insertOne()` နဲ့ document တစ်ခု၊ `insertMany()` နဲ့ document အများကြီးကို collection ထဲထည့်နိုင်ပါတယ်။

```javaScript
// Document တစ်ခုထည့်ခြင်း
db.users.insertOne({
  name: "Hla Hla",
  age: 25,
  status: "active"
})

// Document အများကြီးထည့်ခြင်း
db.users.insertMany([
  { name: "Mya Mya", age: 32, status: "active" },
  { name: "Kyaw Kyaw", age: 28, status: "inactive" }
])
```
 #### Read: Document များ ရှာဖွေခြင်း
`find()`နဲ့ collection ထဲက document တွေကိုရှာနိုင်ပါတယ်။ ဘာ condition မှမใส่ရင် document အားလုံးကိုပြန်ပေးပါတယ်။ `findOne()`ကတော့ ရှာတွေ့တဲ့ ပထမဆုံး document တစ်ခုကိုပဲ ပြန်ပေးပါတယ်။
```javascript
// users collection ထဲက document အားလုံးကိုရှာခြင်း
db.users.find()

// age က 25 ထက်ကြီးတဲ့ user တွေကိုရှာခြင်း
db.users.find({ age: { $gt: 25 } })

// name က "Hla Hla" ဖြစ်တဲ့ user ကိုရှာခြင်း (တစ်ခုတည်း)
db.users.findOne({ name: "Hla Hla" })
```

#### Update: Document များပြင်ဆင်ခြင်း
`UpdateOne()` နဲ့ condition နဲ့ကိုက်ညီတဲ့ ပထမဆုံး document ကို update လုပ်နိုင်ပြီး၊ `updateMany()` နဲ့ကိုက်ညီတဲ့ document အားလုံးကို update လုပ်နိုင်ပါတယ်။
```javascript
// name က "Kyaw Kyaw" ဖြစ်တဲ့ user ရဲ့ status ကို "active" ပြောင်းခြင်း
db.users.updateOne(
  { name: "Kyaw Kyaw" },
  { $set: { status: "active", age: 29 } }
)

// status က "active" ဖြစ်တဲ့ user အားလုံးကို "verified" field အသစ်ထပ်ထည့်ခြင်း
db.users.updateMany(
  { status: "active" },
  { $set: { verified: true } }
)
```
`$set` operator က သတ်မှတ်ထားတဲ့ field ကို update လုပ်ပေးထားပါတယ်။

#### Delete: Document များဖျက်ခြင်း
`deleteOne()` နဲ့ condition နဲ့ကိုက်ညီတဲ့ ပထမဆုံး document ကိုဖျက်ပြီး၊ `deleteMany()` နဲ့  ကိုက်ညီတဲ့ document အားလုံးကို ဖျက်နိုင်ပါတယ်။
```javascript
// name က "Mya Mya" ဖြစ်တဲ့ user ကိုဖျက်ခြင်း
db.users.deleteOne({ name: "Mya Mya" })

// status က "inactive" ဖြစ်တဲ့ user အားလုံးကိုဖျက်ခြင်း
db.users.deleteMany({ status: "inactive" })
```
