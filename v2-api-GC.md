<div dir="rtl">

# احراز هویت
برای دسترسی به API، ابتدا باید داخل وبسایت لاگین کنید و بعد می توانید از داخل پنل کاربری(داشبورد) با کلیک کردن بر روی گزینه  API وارد قسمت مربوطه شوید و توکن اعتبارسنجی(Authorization Token) خود را دریافت کنید.

توکن اعتبار سنجی دریافت شده را باید داخل هدر درخواست ها به شکل زیر قرار دهید

<div dri="ltr">

```
Authorization: Token <your authorization token>
```
</div>


<div dir="rtl">

# گرفتن اطلاعات توکن

</div>

```
import requests

headers = {
    "Authorization": "Token 1234567890qwertyuiopasdfghjkldududuuzxcvbnm",
    "Content-Type": "application/json"
}

request = request.get(
    url = "https://gray-city.ir/api/v2/user/token/",
    headers=headers
)

```

<div dir="rtl">

# گرفتن اطلاعات یوزر مانند موجودی و تعداد سفارش

</div>

```
import requests

headers = {
    "Authorization": "Token 1234567890qwertyuiopasdfghjkldududuuzxcvbnm",
    "Content-Type": "application/json"
}

request = request.get(
    url = "https://gray-city.ir/api/v2/user/info/",
    headers=headers
)

```

#### لطفاً اطمینان حاصل کنید که توکن اعتبارسنجی شما معتبر است، در غیر این صورت ممکن است با خطاهای زیر روبرو شوید.

<div dir="ltr">

#### Error Code
| استتوس کد | توضیحات |
| ------------| -------------|
| 403         | توکن نامعتبر است
| 403         | اطلاعات احراز هویت ارائه نشده است

</div>

<br>



# اندپوینت ها
---

<details>
<summary><h4>لیست دست بندی ها</h4></summary>

#### درخواست
---
برای دریافت دسته بندی های داخل سایت، یک درخواست GET را به آدرس زیر ارسال کنید:
<div dir="ltr">

```
import requests

headers = {
    "Authorization": "Token 1234567890qwertyuiopasdfghjkldududuuzxcvbnm",
    "Content-Type": "application/json"
}

request = request.get(
    url = "https://gray-city.ir/api/v2/categories/",
    headers=headers
)

```
</div>

> **نکته:** به صورت پیشفرض در هر صفحه حداقل 20 دسته بندی نمایش داده می شود و حد اکثر 30 عدد، برای گرفتن دسته بندی ها بیشتر در هر صفحه و یا پجینیشن میتوانید از پارامتر های زیر استفاده کنید 

#### پارامتر ها
---
<div dir="ltr">

| پارامتر   |  نوع دیتا |      توضیحات      |
| ----------- | --------| ------------|
| page        | int     | شماره پیج
| page_size   | int     | تعداد دسته بندی نمایش داده شده در هر پیج، ماکسیموم 20 عدد

</div>
<br>

#### پاسخ
---
برای این درخواست، پاسخی به شکل زیر ارسال می‌شود که شامل لیست محصولات است:

```json
{
    "count": 7,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 2,
            "title": "لایک اپارات"
        },
        {
            "id": 3,
            "title": "ویو اپارات"
        }
    ]
}
```
</details>


<details>
<summary><h2>ثبت سفارش</h2></summary>

<details>
<summary><h4>ثبت سفارش لایک و ویو</h4></summary>
<br>

> **نکته:** دقت داشته باشید که حتما باید هدر `Content-Type: application/json` را برای درخواست های POST ست کرده باشید 


#### درخواست
---
برای ثبت سفارش لایک و ویو، میتوانید یک درخواست POST را به آدرس های زیر ارسال کنید:

<div dir="ltr">

    POST: /api/v2/order/create/
```
import requests

headers = {
    "Authorization": "Token 1234567890qwertyuiopasdfghjkldududuuzxcvbnm",
    "Content-Type": "application/json"
}
data = {
    "category": 2, // ایدی کتگوری
    "link": "https://www.aparat.com/v/hashd", // آدرس ویدیو
    "count": 50
}

request = request.post(
    url = "https://gray-city.ir/api/v2/order/create/",
    headers = headers,
    data = data
)

```
</div>

### ریکوئست بادی
#### 
---
```json
{
    "category": 2, // ایدی کتگوری
    "link": "https://www.aparat.com/v/hashd", // آدرس ویدیو
    "count": 50
}
```

### پاسخ
---
جزئیات سفارش ثبت شده برگشت داده خواهد شد.

```json
{
"category": 6,
"link": "https://www.aparat.com/v/hCc0O",
"user": "adamak.tnh@gmail.com",
"status": "در صف⊷",
"tracking_id": "d6a10c3c7fbf",
"created": "2024-01-10 18:18:14",
"count": 50
}

```

#### استتوس کد ها
---
<div dir="ltr">

| استتوس کد |      توضیحات           |
| ------------| ------------------ |
| 200         | موفقیت آمیرز، نمایش جزئیات سفارش 
| 400         | پارامتر لینک یافت نشد
| 400         | لینک ارسال شده نامعبتر است
| 400         | تایپ ولیو پارامتر category نا معتبر است
| 400         | ایدی محصول ارسال شده مربوط به این دسته بندی نمی باشد
| 404         | محصول یافت نشد
| 403         | موجودی کافی نیست

</div>
</details>



<details>
<summary><h4>ثبت سفارش کامنت</h4></summary>
<br>

> **نکته:** دقت داشته باشید که حتما باید هدر `Content-Type: application/json` را برای درخواست های POST ست کرده باشید 


#### درخواست
---
برای ثبت سفارش لایک، میتوانید یک درخواست POST را به آدرس زیر ارسال کنید:

<div dir="ltr">

    POST: /api/order/create/

</div>

### ریکوئست بادی
---
برای جدا کردن هر کامنت از n\ استفاده کنید

```jsonc
{
    "category": 6, // ایدی محصول
    "link": "https://www.aparat.com/v/hashd", // آدرس ویدیو
    "comment": ["test","test2","test3","test4"], // کامنت ها
    "count": 20
}
```

### پاسخ
---
جزئیات سفارش ثبت شده برگشت داده خواهد شد.

```json
{
  "category": 6,
  "link": "aparat.com/v/YYYyY",
  "user": "Test@gmail.com",
  "status": "در صف⊷",
  "tracking_id": "c15c700ec6c3",
  "created": "2023-04-30 20:58:52",
  "comments": ["test","test2","test3","test4"]
}

```

#### استتوس کد ها
---
<div dir="ltr">

| استتوس کد |      توضیحات           |
| ------------| ------------------ |
| 200         | موفقیت آمیرز، نمایش جزئیات سفارش
| 400         | پارامتر لینک یافت نشد
| 400         | لینک ارسال شده نامعبتر است
| 400         | تایپ ولیو پارامتر category نا معتبر است
| 400         | ایدی کتگوری ارسال شده مربوط به این دسته بندی نمی باشد
| 400         | پارامتر کامنت یافت نشد
| 404         | کتگوری یافت نشد
| 403         | موجودی کافی نیست

</div>
</details>


<details>
<summary><h4>ثبت سفارش واچ تایم</h4></summary>
<br>

> **نکته:** دقت داشته باشید که حتما باید هدر `Content-Type: application/json` را برای درخواست های POST ست کرده باشید 

> **نکته:** دقت داشته باشید که تایم ویدیو باید بیشتر از 2 دقیقه باشد و همچنین عدد count نیز تعداد ساعت درخواستی میباشد


#### درخواست
---
برای ثبت سفارش واچ تایم، میتوانید یک درخواست POST را به آدرس زیر ارسال کنید:

<div dir="ltr">

    POST: /api/order/watch-time/create/

</div>

### ریکوئست بادی
---

```jsonc
{
    "category": 9, // ایدی محصول
    "link": "https://www.aparat.com/v/hashd", // آدرس ویدیو,
    "count": 50
}
```

### پاسخ
---
جزئیات سفارش ثبت شده برگشت داده خواهد شد.

```json
{
  "category": 9,
  "link": "aparat.com/v/YYYY",
  "user": "Test@gmail.com",
  "status": "در صف⊷",
  "tracking_id": "c15c700ec6c3",
  "created": "2023-04-30 20:58:52",
}

```

#### استتوس کد ها
---
<div dir="ltr">

| استتوس کد |      توضیحات           |
| ------------| ------------------ |
| 200         | موفقیت آمیرز، نمایش جزئیات سفارش
| 400         | پارامتر لینک یافت نشد
| 400         | لینک ارسال شده نامعبتر است
| 400         | تایپ ولیو پارامتر category نا معتبر است
| 400         | ایدی کتگوری ارسال شده مربوط به این دسته بندی نمی باشد
| 400         | تایم ویدیو کمتر از مقدار گفته شده میباشد
| 404         | کتگوری یافت نشد
| 403         | موجودی کافی نیست

</div>
</details>


<details>
<summary><h4>ثبت سفارش فالور عادی و فالور پرو</h4></summary>
<br>

> **نکته:** دقت داشته باشید که حتما باید هدر `Content-Type: application/json` را برای درخواست های POST ست کرده باشید 

#### درخواست
---
برای ثبت سفارش فالور عادی و فالور پرو، میتوانید یک درخواست POST را به آدرس های زیر ارسال کنید:

<div dir="ltr">

    POST: /api/order/follower/create/
    POST: /api/order/follower-pro/create/

</div>

### ریکوئست بادی
---

```jsonc
{
    "product": 10, // ایدی محصول
    "link": "https://www.aparat.com/UserName", // آدرس حساب کاربری
}
```

### پاسخ
---
جزئیات سفارش ثبت شده برگشت داده خواهد شد.

```json
{
  "product": 7,
  "link": "aparat.com/UserName",
  "user": "Test@gmail.com",
  "status": "در صف⊷",
  "tracking_id": "c15c700ec6c3",
  "created": "2023-04-30 20:58:52",
}

```

#### استتوس کد ها
---
<div dir="ltr">

| استتوس کد |      توضیحات           |
| ------------| ------------------ |
| 200         | موفقیت آمیرز، نمایش جزئیات سفارش
| 400         | پارامتر لینک یافت نشد
| 400         | لینک ارسال شده نامعبتر است
| 400         | تایپ ولیو پارامتر product نا معتبر است
| 400         | ایدی محصول ارسال شده مربوط به این دسته بندی نمی باشد
| 404         | محصول یافت نشد
| 403         | موجودی کافی نیست

</div>
</details>



<details>
<summary><h4>ثبت سفارش تبلیغ</h4></summary>
<br>

> **نکته:** دقت داشته باشید که حتما باید هدر `Content-Type: application/json` را برای درخواست های POST ست کرده باشید 

#### درخواست
---
برای ثبت سفارش تبلیغات، میتوانید یک درخواست POST را به آدرس زیر ارسال کنید:

<div dir="ltr">

    POST: /api/order/ads/create/

</div>

### ریکوئست بادی
---

```jsonc
{
    "product": 10, // ایدی محصول
    "description": "Ads Description", // متن تبلیغات
}
```

### پاسخ
---
جزئیات سفارش ثبت شده برگشت داده خواهد شد.

```json
{
  "product": 7,
  "user": "Test@gmail.com",
  "status": "در صف⊷",
  "tracking_id": "c15c700ec6c3",
  "created": "2023-04-30 20:58:52",
  "description": "Ads Description"
}

```

#### استتوس کد ها
---
<div dir="ltr">

| استتوس کد |      توضیحات           |
| ------------| ------------------ |
| 200         | موفقیت آمیرز، نمایش جزئیات سفارش 
| 400         | تایپ ولیو پارامتر product نا معتبر است
| 400         | ایدی محصول ارسال شده مربوط به این دسته بندی نمی باشد
| 400         | متن تبلیغ یافت نشد
| 404         | محصول یافت نشد
| 403         | موجودی کافی نیست

</div>
</details>
<br>
<br>
</details>






<details>
<summary><h2>پیگیری سفارش</h2></summary>
<br>

#### درخواست
---
برای پیگیری وضعیت یک سفارش میتوانید درخواست GET را به آدرس زیر ارسال کنید:

<div dir="ltr">

    GET: /api/order/tracking/?tracking_id={tracking_id}

</div>

#### پارامتر ها
---
<div dir="ltr">

| پارامتر   | نوع دیتا |      توضیحات      |
| ----------- | -------| ------------|
| tracking_id | int    | ایدی پیگیری سفارش

</div>
<br>

#### پاسخ
---

```json
{
  "Type": "view",
  "link": "aparat.com/v/.....",
  "status": "Done",
  "initialize_count": 100,
  "uniq_id": "624e15a6f29ea",
  "date": "2023-04-30 23:00:00"
}
```

#### استتوس کد ها
---
<div dir="ltr">

| استتوس کد       | توضیحات |
| ------------| -------------|
| 200         | موفقیت آمیز، نمایش جزئیات سفارش
| 400         | ایدی پیگیری سفارش یافت نشد
| 400         | پارامتر ارسالی نامبعتر است
| 500         | خطای داخلی سرور 

</div>
<br>
<br>
</details>
</div>
