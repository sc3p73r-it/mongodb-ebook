# အခန်း (၂): MongoDB Installation နှင့် Setup
MongoDB ကို စတင်အသုံးပြုဖို့အတွက် ကိုယ့်ရဲ့ computer မှာအရင်ဆုံး install လုပ်ဖို့လိုအပ်ပါတယ်။

#### Windows, macOS, Linux တို့တွင် MongoDB ထည့်သွင်းခြင်း
- တရားဝင် Website: https://www.mongodb.com/try/download/community မှာကိုယ့်ရဲ့ Operating System နဲ့ကိုက်ညီတဲ့ Community Server version ကို download ဆွဲပြီး install လုပ်နိုင်ပါတယ်။

- Installation Guide: တစ်ဆင့်ချင်းပြုလုပ်ပုံကို တရားဝင် documentation မှာ အသေးစိတ် လေ့လာနိုင်ပါတယ်။

#### MongoDB Shell (mongosh) ကို အသုံးပြုခြင်း
Install လုပ်ပြီးသွားရင် MongoDB server ကို run ပြီး command line/terminal ကနေ`mongosh`ဆိုတဲ့ command ကိုရိုက်ပြီး MongoDB Shell ကိုစတင်အသုံးပြုနိုင်ပါတယ်။`mongosh`ကနေ database တွေကို တိုက်ရိုက် query လုပ်နိုင်၊ data ထည့်နိုင်၊ ပြင်နိုင်ပါတယ်။

```shell
mongosh
```

Shell ထဲရောက်သွားရင်`show dbs`လို့ရိုက်ပြီး လက်ရှိ database တွေကို ကြည့်နိုင်ပါတယ်။`use <database_name>`နဲ့ database အသစ်ဆောက် (သို့) ရှိပြီးသား database ကို သုံးနိုင်ပါတယ်။

#### MongoDB Compass (GUI) နှင့် ချိတ်ဆက်ခြင်း
MongoDB Compass ဆိုတာ MongoDB အတွက် graphical user interface (GUI) tool တစ်ခုဖြစ်ပါတယ်။ Command line နဲ့ အသုံးမပြုချင်တဲ့သူတွေအတွက် data တွေကို အလွယ်တကူ ကြည့်ရှု၊ ပြင်ဆင်နိုင်အောင် ကူညီပေးပါတယ်။
- Download: https://www.mongodb.com/try/download/compass မှာ download လုပ်နိုင်ပါတယ်။
- Connection: Compass ကိုဖွင့်ပြီး connection string (ဥပမာ - mongodb://localhost:27017) ကိုထည့်ပြီး MongoDB server နဲ့ ချိတ်ဆက်နိုင်ပါတယ်။


