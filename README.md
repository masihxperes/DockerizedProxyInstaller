# نصاب پروکسی برای دیواره ی آتش ایران

**اطلاعیه: استفاده از این نصاب یا هرگونه تعلقات آن برای حامیان رژیم جنایتکار و اشغالگر جمهوری اسلامی مطلقا ممنوع و شرعا حرام است!**

این اسکریپت به شما کمک می‌کند چندین پروتکل مختلف پروکسی که در مقابل سیستم فیلترینگ جمهوری فاشیست اسلامی کارایی دارند را بطور همزمان بر روی سرور لینوکس خود راه‌اندازی نمایید.

## ویژگی ها

- استفاده از Docker برای راه اندازی سریع و دستکاری حداقلی فایل های سیستمی
- استفاده از وب سرور Caddy برای مدیریت متمرکز پورت ها و گواهینامه های امنیتی TLS
- امکان مسدودسازی دسترسی به آی‌پی های ایرانی هنگام استفاده از پروکسی برای محافظت از سرور و مخفی ماندن
- امکان مسدودسازی تبلیغات بدون نیاز به نصب نرم افزار از جانب کاربر هنگام استفاده از پروکسی
- سازگاری ترانسپورت های gRPC و Websocket با CDN ها بدون نیاز به تغییر پیکربندی در سمت سرور یا کلاینت
- راه‌اندازی پروکسی VLESS با سه ترانسپورت (TCP, gRPC, Websocket)
- راه‌اندازی پروکسی تروجان با سه ترانسپورت (HTTP2, gRPC, Websocket)
- راه‌اندازی پروکسی Vmess با ترانسپورت Websocket
- راه‌اندازی پروکسی Hysteria با پروتکل UDP
- راه‌اندازی پروکسی تلگرام MTProto
- امکان ارائه صفحات وب به بازدیدکنندگان از دامنه در مرورگر و مخفی ماندن ماهیت سرور

## ملزومات

### ملزومات عمومی

- یک حساب رایگان Cloudflare
- یک دامنه رایگان یا خریداری شده
- یک دامنه یا زیردامنه به ازای هر پروکسی دلخواه در پنل کلادفلر
- یک سرور مجازی لینوکس

### ملزومات فنی سرور

- OS: Debian 11 or Ubuntu 20.04, 22.04
- Memory: Min. 512MB, Recommended 1GB
- Storage: 10GB NVME or SSD
- Virtualization: KVM

## چطور عمل می‌کند؟

پروکسی های ارائه شده مبتنی بر مفهوم TLS عمل کرده و از این رو نیاز به یک دامنه و تعدادی زیردامنه خواهند داشت.
پروکسی ها در یک شبکه ی داخلی درون سرور راه‌اندازی خواهند شد و دسترسی به آنها تنها از طریق وب سرور Caddy مدیریت خواهد شد.
این روش مزیت هایی از قبیل به اشتراک گذاشتن پورت محبوب ۴۴۳ بین تمام پروکسی ها و مدیریت خودکار گواهینامه های امنیتی و همچنین ارائه یک وبسایت نمایشی به بازدیدکنندگان در مرورگر را خواهد داشت. تنها استثنا در این مورد پروکسی Hysteria می‌باشد که مستقیم به کانتینر داکر خود متصل خواهد شد.

همچنین استفاده از Docker این امکان را می‌دهد که پروکسی های دلخواه را بصورت ایزوله شده در یک پردازه به همراه تمام بسته های مورد نیاز داشته باشیم بدون نیاز به نصب بسته ها و دستکاری بر روی سیستم عامل میزبان و احتمال خرابکاری! تنها گزینه هایی که مستلزم تغییر در سیستم عامل میزبان هستند گزینه های مسدودسازی دسترسی به آی‌پی ایرانی و بهینه سازی تنظیمات شبکه می‌باشند که البته اختیاری بوده اما به شدت توصیه می‌شوند!

در صورت تشخیص سرور از سوی سیستم فیلترینگ و مسدود شدن کافیست قابلیت CDN را برای پروکسی هایی با ترانسپورت gRPC و یا Websocket را فعال کنید بدون نیاز به هیچ تغییری از سمت سرور یا کلاینت ها، پروکسی شما از مسدودی آزاد می شود! پوف!

از آنجا که عملکرد پروکسی ها در سرویس‌دهنده های مختلف تفاوت دارند این اسکریپت امکان راه اندازی مجموعا ۷ نوع پروکسی را فراهم آورده تا بلاخره یک گزینه ی کارا در دسترس کاربر باشد.

در انتها با انتخاب گزینه ی چاپ پیوند های اشتراک گذاری پروکسی ها، پیوند تمامی پروکسی هایی که فعال کرده بودید نمایش داده خواهد شد همچنین این پیوندها درون فایل های متنی جداگانه در یک فایل فشرده زیپ به از محل HOME/proxy-clients.zip قابل دانلود خواهد بود.

## نحوه نصب

```
cd ~
git clone https://github.com/0xLem0nade/DockerizedProxyInstaller.git
cd DockerizedProxyInstaller
./installer.sh
```

## نکات

- این مجموعه شامل x-ui یا پنل های گرافیکی برای مدیریت کاربران نمی باشد
- این نصاب پروکسی ها را مستقیما در یک سرور خارجی راه‌اندازی می‌نماید و برای مفهوم زنجیره‌سازی پروکسی بواسطه یک سرور داخلی نیاز به تنظیم و راه‌اندازی سرور ایرانی بطور دستی یا از طریق اسکریپت دیگری دارید. طی کاربرد چند ماهه با همین بستر سرعت خوبی داشته و شخصا نیازی به سرور داخلی نداشتم.

## پشتیبانی

- [کانال تلگرام لیمونت](https://t.me/Lem0net)
- [گروه تلگرام لیمونت](https://t.me/Lem0netDiscussion)
