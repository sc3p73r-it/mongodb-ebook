# အခန်း (၈): Mongoose with NodeJS Application
Node.js application တွေနဲ့ MongoDB ကို ချိတ်ဆက်အလုပ်လုပ်တဲ့အခါ၊ MongoDB native driver ကို တိုက်ရိုက်သုံးနိုင်သလို၊ Mongoose လို့ခေါ်တဲ့ library ကိုလည်း ကြားခံအဖြစ် အသုံးများကြပါတယ်။ Mongoose က MongoDB နဲ့ အလုပ်လုပ်ရတာကို ပိုမိုလွယ်ကူပြီး structure ကျစေပါတယ်။

#### Mongoose ဆိုတာဘာလဲ?
Mongoose ဆိုတာ Node.js ပေါ်မှာအလုပ်လုပ်တဲ့ Object Data Modeling (ODM) library တစ်ခုဖြစ်ပါတယ်။ သူက MongoDB ထဲမှာရှိတဲ့ data တွေကို JavaScript object တွေအနေနဲ့ ကိုယ်စားပြုပြီး အလွယ်တကူကိုင်တွယ်နိုင်အောင် ကူညီပေးပါတယ်။

Mongoose ကို ဘာကြောင့်သုံးသင့်လဲ?

1. Schema Validation: Collection ထဲကို data မထည့်ခင်၊ ကိုယ်သတ်မှတ်ထားတဲ့ ပုံစံ (structure) နဲ့ ကိုက်ညီရဲ့လားဆိုတာကို အလိုအလျောက် စစ်ဆေးပေးပါတယ်။ ဒါကြောင့် data consistency ကို ထိန်းသိမ်းရလွယ်ကူစေပါတယ်။

2. Business Logic Hooks (Middleware): Data တစ်ခုကို မသိမ်းခင် (pre-save) ဒါမှမဟုတ် သိမ်းပြီးနောက် (post-save) မှာ ကိုယ်လိုချင်တဲ့ function တွေ (ဥပမာ - password hashing) ကို အလိုအလျောက် run ခိုင်းလို့ရပါတယ်။

3. Data Type Casting: String ကို Number အဖြစ်၊ ဒါမှမဟုတ် သတ်မှတ်ထားတဲ့ data type အတိုင်း အလိုအလျောက် ပြောင်းလဲပေးပါတယ်။

4. Query Building: ရှုပ်ထွေးတဲ့ query တွေကို ရေးရတာ ပိုလွယ်ကူစေပါတယ်။

#### Mongoose Setup နှင့် Database ချိတ်ဆက်ခြင်း
ပထမဆုံး Node.js project တစ်ခုထဲမှာ Mongoose ကို install လုပ်ဖို့လိုပါတယ်။
```shell
npm install mongoose
```
ပြီးရင် ကိုယ့်ရဲ့ JavaScript file ထဲမှာ Mongoose ကို import လုပ်ပြီး MongoDB database ကို ချိတ်ဆက်နိုင်ပါတယ်။
```javascript
// mongoose ကို import လုပ်ခြင်း
const mongoose = require('mongoose');

// MongoDB Atlas (cloud) or local database ကို ချိတ်ဆက်ခြင်း
// 'myNewDB' ဆိုတာက ကိုယ်သုံးမယ့် database ရဲ့ နာမည်ဖြစ်ပါတယ်
const connectionString = 'mongodb://127.0.0.1:27017/myNewDB';

async function connectToDb() {
  try {
    await mongoose.connect(connectionString);
    console.log('Successfully connected to MongoDB!');
  } catch (error) {
    console.error('Error connecting to MongoDB:', error);
  }
}

// function ကို ခေါ်ပြီး database ချိတ်ဆက်ခြင်း
connectToDb();
```

`async/await` ကိုသုံးပြီး database connection ကို စောင့်ဆိုင်းပြီးမှ ဆက်အလုပ်လုပ်တာက best practice တစ်ခုဖြစ်ပါတယ်။

#### Schema နှင့် Model တည်ဆောက်ခြင်း
Mongoose ရဲ့ အဓိက အရေးကြီးဆုံးအစိတ်အပိုင်းနှစ်ခုက Schema နဲ့ Model ဖြစ်ပါတယ်။
1. Schema: Collection တစ်ခုထဲမှာရှိမယ့် document တွေရဲ့ ဖွဲ့စည်းပုံ (structure)၊ data type တွေနဲ့ validation rule တွေကို သတ်မှတ်ပေးတဲ့ blueprint တစ်ခုဖြစ်ပါတယ်။
2. Model: အဲဒီ Schema blueprint ကိုအသုံးပြုပြီး တကယ့် database collection နဲ့ တိုက်ရိုက် အပြန်အလှန် အလုပ်လုပ်ပေးမယ့် constructor တစ်ခုဖြစ်ပါတယ်။ Model ကနေတဆင့် data တွေရှာခြင်း၊ သိမ်းခြင်း၊ ဖျက်ခြင်းတွေ ပြုလုပ်ရပါတယ်။

ဥပမာ - User Schema နှင့် Model တည်ဆောက်ခြင်း

```javascript
const mongoose = require('mongoose');
const { Schema } = mongoose;

// User Schema ကို တည်ဆောက်ခြင်း
const userSchema = new Schema({
  username: {
    type: String,
    required: true, // ဒီ field က မဖြစ်မနေထည့်ရမယ်
    unique: true,   // တူတဲ့ username နှစ်ခုရှိလို့မရဘူး
    trim: true      // ရှေ့နောက် space တွေကို ဖျက်ပေးမယ်
  },
  email: {
    type: String,
    required: true,
    unique: true,
    lowercase: true // email ကို အလိုအလျောက် အက္ခရာအသေးပြောင်းပေးမယ်
  },
  age: {
    type: Number,
    min: 18 // အနည်းဆုံး 18 နှစ်ရှိရမယ်
  },
  createdAt: {
    type: Date,
    default: Date.now // data အသစ်ထည့်တိုင်း လက်ရှိအချိန်ကို default ထည့်ပေးမယ်
  }
});

// Schema ကနေ User Model ကို တည်ဆောက်ခြင်း
// 'User' ဆိုတဲ့ နာမည်ကနေ collection name 'users' (plural & lowercase) ကို အလိုအလျောက်တည်ဆောက်ပေးသွားပါလိမ့်မယ်
const User = mongoose.model('User', userSchema);

// အခြား file တွေကနေ ဒီ model ကို ပြန်သုံးနိုင်အောင် export လုပ်ခြင်း
module.exports = User;
```

#### Mongoose ဖြင့် CRUD Operations များ ပြုလုပ်ခြင်း
အပေါ်မှာပြထားတဲ့ User model ကိုသုံးပြီး CRUD operations တွေကို async/await syntax နဲ့ ပြုလုပ်ကြည့်ပါမယ်။
1. Create (Data အသစ်ထည့်ခြင်း)

```javascript
async function createUser() {
  try {
    const newUser = new User({
      username: 'aungkyaw',
      email: 'AungKyaw@example.com', // lowercase ဖြစ်သွားမယ်
      age: 25
    });
    
    const savedUser = await newUser.save(); // database ထဲကို သိမ်းဆည်းခြင်း
    console.log('User created successfully:', savedUser);
  } catch (error) {
    console.error('Error creating user:', error.message);
  }
}
createUser();
```

2. Read (Data ရှာဖွေခြင်း)

```javascript
async function findUsers() {
  try {
    // user အားလုံးကို ရှာခြင်း
    const allUsers = await User.find({});
    console.log('All users:', allUsers);
    
    // username က 'aungkyaw' ဖြစ်တဲ့ user ကို ရှာခြင်း
    const specificUser = await User.findOne({ username: 'aungkyaw' });
    console.log('Specific user:', specificUser);

    // ID ကိုသုံးပြီး ရှာခြင်း
    const userById = await User.findById(specificUser._id);
    console.log('User by ID:', userById);
  } catch (error) {
    console.error('Error finding users:', error.message);
  }
}
findUsers();
```
3. Update (Data ပြင်ဆင်ခြင်း)

```javascript
async function updateUser(username) {
  try {
    // username ကိုသုံးပြီး age ကို update လုပ်ခြင်း
    const updatedUser = await User.updateOne(
      { username: username }, 
      { $set: { age: 30 } }
    );
    
    if (updatedUser.modifiedCount > 0) {
      console.log('User updated successfully!');
    } else {
      console.log('User not found or no changes made.');
    }
  } catch (error) {
    console.error('Error updating user:', error.message);
  }
}
updateUser('aungkyaw');
```
4. Delete (Data ဖျက်ခြင်း)

```javascript
async function deleteUser(username) {
  try {
    const result = await User.deleteOne({ username: username });
    
    if (result.deletedCount > 0) {
      console.log('User deleted successfully!');
    } else {
      console.log('User not found.');
    }
  } catch (error) {
    console.error('Error deleting user:', error.message);
  }
}
deleteUser('aungkyaw');
```
Validation နှင့် Middleware အသုံးပြုပုံ

#### Validation

Schema မှာ `required`, `min`, `max`, `enum` စတဲ့ validation rule တွေထည့်ထားရင် Mongoose က data ကိုမသိမ်းခင် အလိုအလျောက်စစ်ဆေးပေးပါတယ်။ အကယ်၍ rule နဲ့မကိုက်ညီရင် error ပြန်ပေးမှာဖြစ်ပါတယ်။ အပေါ်က `userSchema` ဥပမာမှာ `required`, `unique`, `min` တို့က validation တွေပဲဖြစ်ပါတယ်။

#### Middleware (pre & post hooks)
Middleware ဆိုတာ model တစ်ခုပေါ်မှာ operation တစ်ခု (ဥပမာ - `save`, `remove`) မလုပ်ခင် (`pre`) ဒါမှမဟုတ် လုပ်ပြီး (`post`) မှာ run တဲ့ function တွေဖြစ်ပါတယ်။

ဥပမာ - User password ကို မသိမ်းခင် hash လုပ်ခြင်း

User password ကို database ထဲမှာ plain text အဖြစ် တိုက်ရိုက်မသိမ်းသင့်ပါဘူး။ pre('save') hook ကိုသုံးပြီး password ကို hash လုပ်ပြီးမှ သိမ်းဆည်းနိုင်ပါတယ်။

```javascript
const bcrypt = require('bcrypt');

// userSchema ထဲမှာ password field ထပ်ထည့်ပြီး
// pre-save hook ကို အခုလိုသုံးနိုင်ပါတယ်
userSchema.pre('save', async function(next) {
  // password field က ပြောင်းလဲမှုမရှိရင် ဘာမှမလုပ်ဘဲ ဆက်သွားမယ်
  if (!this.isModified('password')) {
    return next();
  }

  try {
    // password ကို hash လုပ်ခြင်း
    const salt = await bcrypt.genSalt(10);
    this.password = await bcrypt.hash(this.password, salt);
    next();
  } catch (error) {
    next(error);
  }
});
```
ဒီ code က user document အသစ် `save` လုပ်တိုင်း (သို့) ရှိပြီးသား user ရဲ့ password ကို update လုပ်တိုင်း အလိုအလျောက် run ပြီး password ကို hash လုပ်ပေးသွားမှာ ဖြစ်ပါတယ်။