# SW-Lab5

امیرمهدی کوششی

امیرحسین عرب‌زاده

احمدرضا خناری

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



