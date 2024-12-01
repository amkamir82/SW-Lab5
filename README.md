# SW-Lab5

امیرمهدی کوششی - 98171053

امیرحسین عرب‌زاده - 98105908

احمدرضا خناری - 99170412

## بررسی کلاس JavaCup

ابتدا کلاس JavaCup را با استفاده از ابزار Yourkit مانیتور کردیم. نتایج در عکس‌های زیر آمده است.

![Screenshot from 2024-11-30 12-15-57](https://github.com/user-attachments/assets/dd9fba87-666a-40f9-928b-9f8f135ae5f9)

![Screenshot from 2024-11-30 12-16-05](https://github.com/user-attachments/assets/30e8926c-37fe-4b33-8f2d-9dbb7c06e73b)

همانطور که مشاهده می‌کنید، بعد از دادن ۳ عدد ورودی، مصرف منابع به صورت صعودی رشد می‌کند و بعد از مدتی خطای heap داده می‌شود.


طمابق کد می‌توان متوجه شد که اکثر استفاده‌ی کدی که از منابع است، تیکه کد تابع `temp()` می‌باشد. حال ما قصد داریم پیاده‌سازی این تابع را به نحوی عوض کنیم که نسبت به قبل بهتر شود.

کد قبل:

![image](https://github.com/user-attachments/assets/e74c59c0-adbc-4d43-810d-679935539177)


کد بعد:

![image](https://github.com/user-attachments/assets/24a146c1-773b-495b-b463-3cfaae8d43ba)

با تغییر دادن ArrayList به یک آرایه‌ی استاتیک، خطایی که قبلا بخاطر  heap می‌خوردیم را دیگر نمی‌خوریم. همچنین بر خلاف کد قبل، به خروجی نیز دست پیدا می‌کنیم.

![photo_2024-12-01_18-15-23](https://github.com/user-attachments/assets/238c3a21-98b9-4b10-bb53-0032503a023b)

مطابق عکس‌های زیر، profiling کد جدید بعد از تغییر تابع temp به شکل زیر می‌باشد:

![photo_2024-12-01_18-17-51](https://github.com/user-attachments/assets/8f8eeaff-4823-4a74-b9e8-b0f66a85ea64)

![photo_2024-12-01_18-17-57](https://github.com/user-attachments/assets/0e09944f-b8c9-44ac-9089-61330d9c118a)



---
## قسمت دوم

برای این قسمت، ما یک برنامه پیاده‌سازی کردیم که بر اساس آن بزرگ‌ترین عدد مربع کامل کوچک‌تر از بزرگ‌ترین مقدار مجاز int در java (یعنی 2147483647) را پیدا کنیم. برای این کار، مطابق شکل زیر، ما یک حلقه داریم و تمامی i * iها را تا قبل از این مقدار چک می‌کنیم.


![image](https://github.com/user-attachments/assets/f67ffe95-d605-4d8c-80d6-d7ad4741aa7c)

مطابق شکل زیر، profiling ابزار yourkit مشخص است.

![image](https://github.com/user-attachments/assets/1b2d6c67-38d6-403c-b187-37ba9cd3301b)

![image](https://github.com/user-attachments/assets/55f562c0-3eb8-41a8-886a-c89afd8fcc61)

مطابق کد، ما توان ۲ی اعداد را تا قبل از خود مقدار بزرگ‌ترین عدد int در جاوا ادامه می‌دهیم، در صورتی که می‌دانیم که می‌توانیم این حلقه را تا کمتر از Square بزرگ‌ترین عدد ادامه دهیم. زیرا مقدار i به صورتی که i>square(max int) باشد، قطعا i*i نیز بزرگ‌تر از max int می‌باشد. پس کد را ویرایش می‌کنیم. کد پس از ویرایش عبات است از:


![image](https://github.com/user-attachments/assets/d1a12607-1eff-4440-8dda-4aed3621887c)

حال profiling را پس از اپتیمایز کردن این کد مشاهده می‌کنیم.

![image](https://github.com/user-attachments/assets/2d9706db-87ef-413a-a409-a1623042dfad)


ما برای اینکه بتوانیم کد اپتیمایز شده را profile کنیم، ابتدا یک wait هم گذاشتیم. به همین دلیل است که ابتدا مقدار CPU بالا است. پس از آن زمانی که به ادامه‌ی کد می‌رسد، مقدار cpu usage به شدت کم می‌شود و خروجی کد تقریبا ۱۰ برابر سریع‌تر (از نظر زمانی) نسبت به کد قبل چاپ می‌شود.
