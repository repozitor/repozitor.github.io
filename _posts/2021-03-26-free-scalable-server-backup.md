---
title: "پشتیبان(بکاپ) گیری از سرور، راه حل مطمئن و رایگان"

author: repozitor

tags: [sysadmin,system administrator,backup,free,network,security,server,automation]
categories:
    - server
    - network
    - security
    - backup

date: 2017-07-07
comments: true
---

<div class="WordSection1">
  <h2 class="MsoNormal" dir="RTL" style="text-align: right; direction: rtl; unicode-bidi: embed;">
    <span style="font-size: 18pt;"><strong><span lang="FA" style="line-height: 115%; font-family: IRRoya;">مقدمه</span></strong></span>
  </h2>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; text-indent: .5in; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">امروزه<br /> خیلی از کسب‌وکارهای<br /> استارتاپی<br /> وابسته به<br /> سایتی هست که<br /> خدمات اون<br /> استارتاپ از<br /> اون سایت برای<br /> عموم مردم<br /> ارایه می‌شود.<br /> داده‌های<br /> موجود روی<br /> سرور اصلی<br /> برای<br /> استارتاپ‌ها<br /> بسیار مهم<br /> است. این داده‌ها<br /> می‌تواند<br /> اطلاعات حساب<br /> کاربری افراد<br /> شامل سفارش‌ها،<br /> هویت کاربر و &#8230;<br /> باشد. از طرفی<br /> داده‌های خود<br /> استارتاپ‌ها<br /> مانند<br /> اطلاعات<br /> کالاهایی که<br /> توی سایت ثبت<br /> شده (به<br /> عبارتی<br /> محتوای سایت)<br /> و مواردی از این<br /> دست خیلی مهم<br /> هست. از بین<br /> رفتن این داده‌ها<br /> به دلایل<br /> مختلف(!) ضرر‌های<br /> زیادی برای<br /> شرکت‌ها داره.<br /> حتی در بعضی<br /> موارد ممکنه<br /> نیاز بشه که<br /> سریعا سرور را<br /> تعویض کنید.<br /> مثل ما که از<br /> سرویس‌های </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">VPS</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;"> شرکت<br /> افرانت راضی<br /> نبودیم و به<br /> سرویس‌های<br /> شرکت </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">Leaseweb</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;"> کوچ کردیم.<br /> بنابراین یک<br /> راه حل خیلی<br /> ساده نیاز<br /> داشتیم که کل سایت<br /> را درجا </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">copy/paste</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;"> کنیم<br /> روی سرور جدید<br /> در کمتر از<br /> ۵دقیقه تاخیر!<br /> یکی از وظایف<br /> من این بود که<br /> یک سیستم<br /> پشتیبانی(بکاپ)<br /> بسازم که<br /> قابلیت‌های<br /> زیر رو داشته<br /> باشه:</span>
  </p>
  
  <p class="MsoListParagraphCxSpFirst" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">بکاپ(</span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">Backup</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">) از<br /> سایت داشته<br /> باشد.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">بکاپ‌<br /> در هر بار از<br /> کل سایت گرفته<br /> شود. نسخه‌های<br /> افزایشی(</span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">Incremental</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">) گاهی‌<br /> اوقات در<br /> بازگردانی دچار<br /> مشکل می‌شوند،<br /> به طوری که<br /> ساخت مجدد<br /> محتوا بهتر از<br /> ریکاوری آنها ‌هست.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">هیچ<br /> پولی برای<br /> اینکار<br /> پرداخت نشود.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">داده‌ها<br /> در جایی نگه‌داری<br /> شود که نگران<br /> از بین رفتن<br /> داده‌ها<br /> نباشیم.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">راه‌حل<br /> باید بدون صرف<br /> هزینه باشد.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">ورود<br /> به </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">panel</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;"><br /> باید بسیار<br /> امن باشد. چون<br /> کل داده‌ها<br /> یکجا ذخیره می‌شود<br /> و لو رفتن<br /> آنها تبعات<br /> بسیار<br /> ناگواری در پی<br /> دارد!</span>
  </p>
  
  <p class="MsoListParagraphCxSpLast" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">طوری<br /> داده‌ها در<br /> بکاپ ذخیره<br /> شود، که سرویس‌دهنده<br /> ذخیره فایل از<br /> داده‌ها<br /> سؤاستفاده<br /> نکند. به<br /> عبارتی روی<br /> محتوای فایل‌های<br /> شما جاسوسی<br /> نکند.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">به<br /> شما خواننده<br /> گرامی توصیه<br /> می‌شود<br /> چنانچه تمایل<br /> به درک ساختار<br /> مهندسی این روش<br /> بکاپ‌گیری<br /> ندارید،<br /> مستقیما به<br /> سراغ بخش آخر<br /> که نحوه‌<br /> پیاده‌سازی<br /> را تشریح کرده<br /> است، بروید.<br /> اما اگر خواهان<br /> یادگیری<br /> ساختار روش<br /> بکاپ هستید،<br /> کل متن را با<br /> دقت بخوانید. <strong>برای ادامه کلیک کنید.</strong></span>
  </p>
  
  <p>
    <!--more-->
  </p>
  
  <h2 class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <strong><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">نیازسنجی<br /> </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">Backup</span><span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;"> <span lang="FA">و<br /> راهکار ایده‌آل</span></span></strong>
  </h2>
  
  <p class="MsoListParagraphCxSpFirst" dir="RTL" style="margin-left: 0in; text-align: justify; text-indent: .5in; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">اول<br /> که نیاز به<br /> بکاپ برای<br /> استارتاپ ما‌<br /> (</span><span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;"><a href="https://www.wegobazaar.com/"><span dir="LTR">Wegobazaar.com</span></a><span lang="FA">) خیلی<br /> حاد بود خیلی<br /> سریع از سیستم<br /> پشتیبان‌گیری<br /> </span></span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">Bacula</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;"><br /> استفاده<br /> کردیم. بعد<br /> متوجه ۲تا<br /> مشکل خیلی<br /> اساسی شدیم:</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: 'Courier New';">o<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">یکی<br /> اینکه خود<br /> سروری که<br /> اطلاعات بکاپ<br /> توی اون ذخیره<br /> می‌شد، ممکن<br /> بود اطلاعاتش<br /> پاک بشه و به<br /> عبارتی خودش<br /> نیاز به بکاپ<br /> داشت!!!</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: 'Courier New';">o<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">ما<br /> برای این سرور<br /> هزینه پرداخت<br /> می‌کردیم، که<br /> خیلی ایده آل<br /> ما نبود.</span>
  </p>
  
  <p class="MsoListParagraphCxSpLast" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: 'Courier New';">o<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">امکان<br /> داشت خود سرور<br /> بکاپ مورد حمله<br /> قرار بگیرد و<br /> داده‌ها افشا<br /> شود. ما واقعا<br /> داده‌هامون<br /> خیلی حساس<br /> هست! اصلا<br /> نمیخواستم در<br /> این مورد<br /> احساس خطر<br /> بکنم.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; text-indent: .5in; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya;">بعد از<br /> اینکه صاحب یک<br /> سیستم نه‌چندان<br /> امن برای بکاپ<br /> شدیم، حالا با<br /> خیال راحت به<br /> این موضوع فکر<br /> می‌کردیم که<br /> چطوری می‌توانیم<br /> بازم امنیت<br /> این سیستم‌ را<br /> بهبود<br /> بدیم(هنوز<br /> هزینه برای ما<br /> مشکل‌ساز<br /> نشده بود). در<br /> نهایت بعد از<br /> کلی تحقیق<br /> تونستم روشی<br /> رو ابداع کنم<br /> که ویژگی‌های<br /> زیر رو داشته<br /> باشه:</span>
  </p>
  
  <p class="MsoListParagraphCxSpFirst" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">بکاپ<br /> از سایت داشته<br /> باشد. </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">->اینکه<br /> اصلا هیچی!</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">بکاپ‌<br /> در هر بار از<br /> کل سایت گرفته<br /> شود. نسخه‌های<br /> افزایشی(</span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">Incremental</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">)<br /> گاهی‌ اوقات<br /> در بازگردانی<br /> چار مشکل می‌شوند،<br /> به طوری که<br /> ساخت مجدد<br /> محتوا بهتر از<br /> ریکاوری آنها ‌هست.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">هیچ<br /> پولی برای<br /> اینکار<br /> پرداخت نشود. </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">-><br /> طوری تنظیم شد<br /> که در هربار<br /> از کل سایت<br /> بکاپ گرفته<br /> شود.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">داده‌ها<br /> در جایی نگه‌داری<br /> شود که نگران<br /> از بین رفتن<br /> داده‌ها<br /> نباشیم. </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">-><br /> برای اینکار<br /> گوگل درایو را<br /> انتخاب کردیم!</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">راه‌حل<br /> باید بدون صرف<br /> هزینه باشد. </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">-><br /> گوگل درایو تا<br /> سقف ۱۵گیگابایت<br /> فضای رایگان<br /> به کاربران می‌دهد.<br /> البته یک<br /> اشکالی در<br /> سیستم ذخیره سازی<br /> گوگل پیدا<br /> کردم که می‌توانیم<br /> حتی بیشتر از<br /> ۱۵گیگابایت<br /> ذخیره کنیم<br /> بدون اینکه<br /> پول بدیم! اما<br /> چون این روش غیرقانونی<br /> هست نمیشه<br /> اینجا نوشت.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">ورود<br /> به </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">panel</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;"> باید<br /> بسیار امن<br /> باشد. چون کل<br /> داده‌ها یکجا<br /> ذخیره می‌شود<br /> و لو رفتن<br /> آنها تبعات<br /> بسیار<br /> ناگواری در پی<br /> دارد! </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">-> وارد<br /> شدن به حساب‌کاربری<br /> توی گوگل<br /> درایو با رمز<br /> دوم تنظیم می‌شود(منظورمان<br /> همان سیستم </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">2-Step Authentication</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;"> هست).</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">طوری<br /> داده‌ها در<br /> بکاپ ذخیره<br /> شود، که سرویس‌دهنده<br /> ذخیره فایل از<br /> داده‌ها<br /> سؤاستفاده<br /> نکند. به<br /> عبارتی روی<br /> محتوای فایل‌های<br /> شما جاسوسی<br /> نکند. </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">-> روی<br /> داده‌ها اول<br /> یک برنامه<br /> فشرده‌سازی<br /> اعمال کردیم،<br /> بعدش با<br /> الگوریتم </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">AES256</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;"> که<br /> بسیار بسیار<br /> امن هست<br /> رمزگذاری<br /> کردیم.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">پهنای<br /> باند زیادی از<br /> سرور مصرف<br /> نشود(تا جای<br /> ممکن سریع هم<br /> بکاپ تمام<br /> شود) و حجم<br /> زیاد بکاپ<br /> مارا مجبور<br /> نکند که از<br /> سیستم‌های<br /> تجاری و پولی<br /> استفاده کنیم.</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #376092;"><br /> </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">-> استفاده<br /> کردن از<br /> الگوریتم‌های<br /> فشرده‌سازی<br /> بسیار قوی در<br /> لینوکس.</span>
  </p>
  
  <p class="MsoListParagraphCxSpLast" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #17375e;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #17375e;">وجود<br /> حداقل ۱۰۰<br /> نسخه از اخرین<br /> بکاپ‌هایی که<br /> گرفته می‌شود،<br /> که در صورت<br /> نیاز به<br /> هرکدام که<br /> خواستید بتوانید<br /> بازگردید.</span> <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #00b050;">-><br /> اینکار<br /> خودکار توسط<br /> گوگل انجام می‌شود.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="margin-right: .5in; text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #376092;"> </span>
  </p>
  
  <h2 class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span style="font-size: 18pt;"><strong><span lang="FA" style="line-height: 115%; font-family: IRRoya; color: #0d0d0d;">تشریح سیستم<br /> بکاپ، مزایا و<br /> مراحل بکاپ</span></strong></span>
  </h2>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">          در نهایت توانستم<br /> روشی را ابداع<br /> کنم که بکاپ<br /> همه ویژگی‌های<br /> فوق را داشته<br /> باشد. این روش<br /> برای ما خیلی<br /> خوشحال کننده‌<br /> هست. چون<br /> هرچقدر<br /> میخواستیم<br /> میتونیم بکاپ<br /> بگیریم و روی<br /> گوگل درایو<br /> بزارم. اصلا<br /> نگران این نیستیم<br /> که ممکنه هارد<br /> سرور گوگل<br /> بسوزد یا از<br /> بین برود.<br /> همچنین اصلا<br /> نگران این<br /> نیستیم که<br /> داده‌ها مورد<br /> حمله قرار<br /> بگیره و ازشون<br /> سؤاستفاده بشه.<br /> چون رمز دومی<br /> که برای ورود<br /> به حساب گوگل<br /> مورد نیاز هست<br /> رو هکرها بهش<br /> دسترسی<br /> ندارن، پس خیالمون<br /> راحت هست.<br /> همچین داده‌ها<br /> را ما طوری<br /> رمزنگاری<br /> کردیم، که<br /> گوگل به هیچ<br /> وجه نتواند<br /> آنها را باز<br /> کند و مورد<br /> تجزیه و تحلیل<br /> قراردهد.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> </span>
  </p>
  
  <h3 class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span style="font-size: 18pt;"><strong><span lang="FA" style="line-height: 115%; font-family: IRRoya; color: #0d0d0d;">فاز اول<br /> بکاپ‌گیری(تهیه<br /> فشرده‌کردن<br /> فایل‌های<br /> حساس برای<br /> تهیه پشتیبان):</span></strong></span>
  </h3>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">          در این<br /> روشی که عرض<br /> شد خدمت شما،<br /> ما اول همه‌ی<br /> مسیرهای<br /> بحرانی سیستم<br /> را مشخص<br /> کردیم. یعنی تعیین<br /> شد کدام مسیر<br /> در فایل‌سیستم<br /> حاوی داده‌های<br /> ارزشمند هست.<br /> شما هم باید برای<br /> خودتان<br /> اینکارو را<br /> بکنید. بعد از<br /> اینکه مشخص<br /> شد، حالا داده‌های<br /> اون مسیر رو<br /> فشرده با<br /> حداکثر قدرت<br /> فشرده کردیم.<br /> منظور من<br /> استفاده از<br /> الگوریتم‌های<br /> </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">tar.gz</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> هست. این<br /> الگوریتم‌های<br /> فشرده‌سازی<br /> دو مرحله<br /> دارد:</span>
  </p>
  
  <p class="MsoListParagraphCxSpFirst" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">1.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">در<br /> مرحله اول<br /> ابتدا همه‌ی فایل‌های<br /> دایرکتوری<br /> موردنظر شما(فایل‌های<br /> دایرکتوری<br /> مورد<br /> نظرتان+همه‌ی<br /> فایل‌های زیر<br /> دایرکتوری) را<br /> در یک فایل می‌نویسد<br /> به اینکار </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">tar</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><br /> کردن گفته می‌شود.<br /> اینکار هم<br /> ۲دلیل دارد:</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -1.0in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><span style="font: 7.0pt 'Times New Roman';"><br /> </span>I.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">مرحله<br /> بعدی<br /> الگوریتم که<br /> فشرده‌سازی<br /> فایل است، با<br /> یک فایل<br /> سروکار دارد و<br /> پیچیدگی کار<br /> با چند فایل<br /> را ندارد.</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -1.0in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><span style="font: 7.0pt 'Times New Roman';"><br /> </span>II.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">اینکار<br /> خود به خود<br /> حجم نهایی را<br /> کاهش می‌دهد <i>بدون<br /> اینکه فشرده‌سازی<br /> اعمال شود</i>. به<br /> عنوان مثال<br /> اگر ۳فایل را<br /> با </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">tar</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> کنیم، و<br /> حجم هرکدام </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">x1,<br /> x2, x3</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><br /> باشد، حجم<br /> نهایی حتما<br /> کمتر از </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">x1 +<br /> x2 + x3</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><br /> خواهد بود.<br /> برای فهمیدن<br /> دلیل این<br /> موضوع باید ساختار<br /> فایل سیستم و<br /> نحوه ذخیره‌سازی<br /> فایل‌ها روی<br /> دیسک آشنا<br /> باشید(راهنمایی:<br /> نوشتن ۳فایل<br /> روی یک فایل<br /> باعث می‌شود<br /> آخرین بلوک<br /> نیمه خالی هر<br /> فایل حذف شود<br /> و در نهایت<br /> فقط یک بلوک<br /> نیمه خالی<br /> داشته باشیم<br /> که اگه سایز<br /> بلوک‌ها<br /> ۴کیلوبایت<br /> باشد، حداکثر<br /> هدر رفت ما<br /> ۴کیلوبایت<br /> است. ولی<br /> درحالتی که<br /> ۳فایل داشته<br /> باشیم، حداکثر<br /> هدر رفت<br /> ۱۲کیلوبایت<br /> خواهد بود).<br /> اینکار وقتی<br /> تعداد‌ فایل‌ها<br /> زیاد باشد،<br /> بسیار زیاد<br /> حجم فایل<br /> نهایی را کم<br /> می‌کند(که<br /> عموما فایل‌های<br /> یک وب‌سرور هم<br /> تعداد زیادی<br /> دارد).</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">2.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">در<br /> مرحله دوم یک<br /> فایل داریم که</span> <span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">concat<br /> </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> شده‌ی<br /> همه‌ی فایل‌ها<br /> است. حالا<br /> باید<br /> الگوریتم<br /> فشرده‌سازی </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">gz</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> را<br /> اعمال کنیم.<br /> این الگوریتم<br /> در ۲ روش فایل‌ها<br /> را فشرده می‌کند:</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -1.0in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><span style="font: 7.0pt 'Times New Roman';"><br /> </span>I.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">یا<br /> از الگوریتم </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">LZ0-Compression</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><br /> استفاده می‌کند.<br /> این الگوریتم<br /> ابتدا بخش‌های<br /> تکرای متن را<br /> حذف می‌کند و<br /> فقط یک‌بار<br /> آنها را می‌نویسد.<br /> سپس یک<br /> الگوریتم<br /> مشابه کد<br /> هافمن اعمال می‌کند<br /> تا بازهم حجم<br /> فایل‌ها را<br /> کاهش دهد.</span>
  </p>
  
  <p class="MsoListParagraphCxSpLast" dir="RTL" style="text-align: justify; text-indent: -1.0in; direction: rtl; unicode-bidi: embed; margin: 0in 1.0in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><span style="font: 7.0pt 'Times New Roman';"><br /> </span>II.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">یا<br /> از الگوریتم<br /> کدهای هافمن<br /> استفاده می‌شود.<br /> که این روش<br /> دیگر منسوخ<br /> شده و فقط در<br /> موارد خاص که<br /> در پست‌های<br /> بعدی در مورد<br /> آن نوشته<br /> خواهد شود<br /> استفاده می‌شود<br /> تا کاربرد<br /> حیرت‌انگیز<br /> آن را ببینید.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> </span>
  </p>
  
  <h3 class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span style="font-size: 18pt;"><strong><span lang="FA" style="line-height: 115%; font-family: IRRoya; color: #0d0d0d;">فاز دوم<br /> بکاپ گیری(ذخیره‌کردن<br /> تمام اطلاعات<br /> پایگاه داده<br /> در یک فایل):</span></strong></span>
  </h3>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">          در این<br /> مرحله باید از<br /> پایگاه داده‌های<br /> خود نسخه<br /> پشتیبان تهیه<br /> کنید و در<br /> قالب قابل<br /> بازگشت برای<br /> پایگاه داده<br /> خود ذخیره<br /> کنید. برای<br /> اینکار<br /> باتوجه به بخش<br /> تشریح فنی<br /> سیستم می‌توانید<br /> به راحتی با<br /> یک دستور خط<br /> فرمان(دستور ترمینال)<br /> تمام پایگاه‌<br /> داده‌های<br /> سیستم را<br /> خروجی بگیرید<br /> و داخل مسیر<br /> جاری کنار<br /> سایر فایل های<br /> فشرده‌شده<br /> ذخیره کنید.<br /> ما برای<br /> خودمان این<br /> فایل رو فشرده<br /> نمی‌کنیم،<br /> چون حجیم<br /> نیست. ولی شما<br /> اگه خواستید<br /> می‌توانید<br /> همه‌ی مراحل<br /> فوق را برای<br /> آن انجام<br /> دهید.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> </span>
  </p>
  
  <h3 class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span style="font-size: 18pt;"><strong><span lang="FA" style="line-height: 115%; font-family: IRRoya; color: #0d0d0d;">فاز سوم<br /> بکاپ‌گیری(رمزگذاری<br /> رو فایل‌ها به<br /> منظور ایجاد<br /> محرمانگی):</span></strong></span>
  </h3>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; text-indent: .25in; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">اکنون<br /> ما یک فایل<br /> فوق فشرده‌شده<br /> داریم که حاوی<br /> کلیه اطلاعات</span> <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> مسیر مورد<br /> نظر ما هست.<br /> برای همه‌ی<br /> مسیرهای<br /> حیاتی سرور<br /> تان از این<br /> فایل‌ها تهیه<br /> کنید. حال در<br /> این مرحله<br /> باید این فایل<br /> را رمز‌گذاری<br /> کنیم. پیشنهاد<br /> بنده به شما<br /> این است که به<br /> سواد<br /> رمزنگاری<br /> بنده اعتماد<br /> کنید و از<br /> تنظیماتی که<br /> برای<br /> رمزنگاری<br /> فایل پیشنهاد<br /> می‌کنم عیننا<br /> استفاده کنید<br /> تا خطری متوجه<br /> داده‌های شما<br /> نشود.</span> <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">مشخصات<br /> سیستم<br /> رمزنگاری<br /> پیشنهادی<br /> بنده:</span>
  </p>
  
  <p class="MsoListParagraphCxSpFirst" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">1.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">الگوریتم:<br /> </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">AES</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">2.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">نسخه<br /> الگوریتم: </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">256bit</span>
  </p>
  
  <p class="MsoListParagraphCxSpMiddle" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">3.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">حالت<br /> زنجیره: </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">Cipher<br /> Block Chaining (CBC)</span>
  </p>
  
  <p class="MsoListParagraphCxSpLast" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">4.<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">بردارد<br /> اولیه<br /> الگوریتم: در<br /> مورد </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">IV</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> از حالت<br /> پیش‌فرض </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">openssl</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><br /> استفاده ‌کنید.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> </span>
  </p>
  
  <h3 class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span style="font-size: 18pt;"><strong><span lang="FA" style="line-height: 115%; font-family: IRRoya; color: #0d0d0d;">فاز چهارم<br /> بکاپ گیری(آپلود<br /> فایل‌های<br /> بکاپ روی سرور<br /> گوگل برای<br /> نگهداری بکاپ):</span></strong></span>
  </h3>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">          فایل<br /> مورد نظر را<br /> از طریق خط<br /> فرمان (</span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">Command Line</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">) در<br /> گوگل درایو با<br /> </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">token</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><br /> داده‌شده،<br /> آپلود کنید.</span> <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">اینکار<br /> به راحتی قابل<br /> انجام است.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> </span>
  </p>
  
  <h3 class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span style="font-size: 18pt;"><strong><span lang="FA" style="line-height: 115%; font-family: IRRoya; color: #0d0d0d;">فاز پنجم<br /> بکاپ‌گیری(تنظیم<br /> زمان‌بند<br /> سیستم برای<br /> خودکار کردن<br /> مراحل فوق):</span></strong></span>
  </h3>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">          خودکار<br /> کردن مراحل<br /> اول تا سوم<br /> پیشنهادی به<br /> طوری که به<br /> صورت دوره‌ای<br /> در زمان‌های<br /> دلخواه انجام<br /> شود. شما می‌توانید<br /> تنظیم کنید در<br /> هر ساعت، در<br /> هر ۲ساعت، در<br /> هر روز و &#8230;<br /> اینکار انجام<br /> شود.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> </span>
  </p>
  
  <h3 class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span style="font-size: 18pt;"><strong><span lang="FA" style="line-height: 115%; font-family: IRRoya; color: #0d0d0d;">فاز ششم<br /> بکاپ گیری(!):</span></strong></span>
  </h3>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">          یک لیوان<br /> گل‌گاو زبان<br /> برای رفع<br /> خستگی دم ‌و<br /> نوش جان کنید<br /> و در آرامش<br /> خاطر به خدا<br /> عشق بورزید و<br /> به زندگی خود<br /> ادامه دهید</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> </span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> </span>
  </p>
  
  <h2 class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span style="font-size: 18pt;"><strong><span lang="FA" style="line-height: 115%; font-family: IRRoya; color: #0d0d0d;">تشریح<br /> پیاده سازی<br /> فنی سیستم<br /> بکاپ گیری:</span></strong></span>
  </h2>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; text-indent: .5in; direction: rtl; unicode-bidi: embed;">
    <i><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: red;">توجه:</span></i><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: red;"><br /> </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">در هر<br /> مرحله باتوجه<br /> به اینکه<br /> دستورات روی<br /> سرور اصلی<br /> اجرا می‌شود،<br /> دقت کنید که<br /> هیچ اشتباهی رخ<br /> ندهد. هر<br /> اشتباهی که در<br /> این فرآیند رخ<br /> دهد مسئولیت<br /> آن به عهده<br /> شماست و وجود هر<br /> نقصی در روش<br /> پیشنهادی،<br /> کاملا به عهده<br /> شماست و زیانی<br /> متوجه<br /> نویسنده این<br /> مطلب نخواهد<br /> بود.</span>
  </p>
  
  <p class="MsoListParagraphCxSpFirst" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #0d0d0d;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">ابتدا<br /> باید تمام<br /> مسیر‌های<br /> مورد نظر در<br /> فایل‌سیستم<br /> را مشخص کنید<br /> که داده‌های<br /> حساس شما در<br /> آن مسیر قرار<br /> دارد. به<br /> عنوان مثال من<br /> یک مسیر را<br /> پیشنهاد می‌دهدم<br /> و تا پایان<br /> کار با داده‌های<br /> این مسیر<br /> سروکار<br /> خواهیم داشت.<br /> مسیر<br /> پیشنهادی<br /> بنده: </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">/home/repozitor/Desktop/</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> می‌باشد<br /> که حاوی کلیه<br /> داده‌های وب‌سایت<br /> و &#8230; می‌باشد.</span>
  </p>
  
  <p class="MsoListParagraphCxSpLast" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #0d0d0d;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">داده‌های<br /> موجود در مسیر<br /> مشخص شده را<br /> ابتدا </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">tar</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> کنید و سپس </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">gz<br /> </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">کنید. برای<br /> اینکار می‌توانید<br /> از دستور زیر<br /> استفاده کنید:</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">#cd<br /> /home/repozitor/</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">#tar czpvf siteData.tar.gz<br /> /home/repozitor/Desktop/</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d;"> </span>
  </p>
  
  <p class="MsoListParagraph" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #0d0d0d;">·<span style="font: 7.0pt 'Times New Roman';">       </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> از<br /> همه‌ی داده‌های<br /> موجود در<br /> پایگاه داده<br /> نسخه پشتیبان<br /> تهیه کنید.<br /> برای اینکار<br /> توصیه می‌شود<br /> از همه‌ی<br /> پایگاه‌های<br /> داده در فایل<br /> نسخه پشتیبان<br /> بگیرید:</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">#mysqldump<br /> &#8211;defaults-file=/root/backup/dbExport.conf &#8211;all-databases -u root > db.sql</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">اطلاعات<br /> داخل فایل </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">dbExport.conf</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><br /> باید به صورت<br /> زیر باشد تا<br /> به صورت<br /> خودکار وارد<br /> پایگاه داده<br /> شود و خروجی<br /> داده بگیرد:</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #e46c0a; background: black;">[mysqldump]</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #e46c0a; background: black;">host=localhost</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #e46c0a; background: black;">user=root</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #e46c0a; background: black;">password=&#8221;PASSWORD&#8221;</span>
  </p>
  
  <p class="MsoListParagraph" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #0d0d0d;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">الان<br /> همه‌ی داده‌هایی<br /> که برای<br /> پشتیبان<br /> میخواهیم<br /> آماده شده است.<br /> یک رمز عبور<br /> بسیار<br /> وحشتناک<br /> بسازید(نیازی<br /> نیست حفظ کنید<br /> و فقط یک کپی<br /> از آن داشته<br /> باشید کافی<br /> هست) و آن را<br /> داخل فایلی به<br /> نام </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">pass.txt</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> قرار دهید. حالا<br /> باید<br /> اطلاعاتمون<br /> رو رمزگذاری<br /> کنیم:</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #11ff7d; background: black;">#openssl enc -aes-256-cbc -e -pass<br /> file:pass.txt –in db.sql –out db-crypto.sql</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #11ff7d; background: black;">#openssl enc -aes-256-cbc -e -pass<br /> file:pass.txt –in siteData.tar.gz –out  siteData-crypto.tar.gz</span>
  </p>
  
  <p class="MsoListParagraph" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #0d0d0d;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">اکنون<br /> ما ۲ فایل<br /> داریم که یکی<br /> از آنها حاوی<br /> فایل‌های وب‌سایت<br /> است و دیگری<br /> شامل پایگاه<br /> داده‌ی سایت<br /> ما است.<br /> محتوای این<br /> فایل‌ها رمزگذاری<br /> شده است.<br /> اکنون هرجا<br /> فایلهای<br /> رمزگذاری شده‌<br /> را آپلود<br /> کنیم، مشکلی<br /> نخواهیم داشت.<br /> ما می‌خواهیم<br /> آنها را روی<br /> گوگل درایو<br /> آپلود کنیم.<br /> برای انکار<br /> ابتدا باید<br /> ابزار زیر را<br /> روی سرور<br /> دانلود کرده و<br /> سپس نصب نمایید.<br /> برای اینکار<br /> مراحل زیر را<br /> طی کنید(فایل<br /> زیر برای<br /> لینوکس۳۲بیتی<br /> هست. برای<br /> دریافت سایر<br /> نسخه‌ها/توزیع‌های<br /> دیگر لینوکس<br /> می‌توانید به <a href="https://github.com/prasmussen/gdrive"><span style="color: #0d0dff;">صفحه‌ی<br /> نویسنده</span></a><br /> مراجعه کنید و<br /> نسخه مناسب<br /> خود را دریافت<br /> کنید):</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">#wget <a href="https://cdn.repozitor.com/public/gdrive"><span style="color: #11ff7d;">https://cdn.repozitor.com/public/gdrive</span></a></span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">#chmod +x gdrive</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">#sudo<br /> install gdrive /usr/local/bin/gdrive</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">اکنون<br /> دستور زیر را<br /> بزنید:</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">#gdrive list</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #11ff7d; background: black;">Id                            Name       Type   Size      Created</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">0BUPib2t2aVlCYk85em8<br /> <span dir="RTL" lang="AR-SA">    </span>god.mp3      mp3    6.1 MB    2017-07-07<br /> 19:09:58</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">وقتی این<br /> دستور را<br /> بزنید به شما<br /> یک لینک یک‌بار<br /> مصرف می‌دهد.<br /> آن را در<br /> مرورگر خود<br /> کپی کنید و<br /> کلید اینتر را<br /> بزنید.<br /> درخواست<br /> اجازه گوگل را<br /> تایید کنید تا<br /> ترمینال سرور<br /> شما بتواند به<br /> گوگل درایو<br /> متصل شود. حال<br /> که دوباره این<br /> دستور را<br /> بزنید، لیست<br /> همه‌ی فایل‌های<br /> داخل گوگل<br /> درایو را به<br /> شما نمایش می‌دهد.<br /> برای اینکه<br /> بتوانیم فایل‌های<br /> رمزگذاری شده<br /> را داخل گوگل<br /> درایو آپلود‌<br /> کنیم، از<br /> دستور زیر<br /> استفاده می‌کنیم:</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">#gdrive<br /> upload siteData-crypto.tar.gz</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">#gdrive<br /> upload db-crypto.sql</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">حال‌<br /> پشتیبان‌های<br /> شما با موفقیت<br /> آپلود شد. اگر<br /> داخل گوگل<br /> درایو بروید<br /> می‌توانید<br /> ببینید که<br /> فایلها‌تان<br /> آنجا هست.<br /> لیست فایل‌های<br /> آپلود شده را<br /> می‌توانید با<br /> لیست‌گیری هم<br /> ببینید:</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #11ff7d; background: black;">#gdrive<br /> list</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #11ff7d; background: black;">Id                            Name                        Type      Size     Created</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #11ff7d; background: black;">0B3m5DM0xFdVhmRmc             db-crypto.sql               sql       194<br /> MB    2017-07-07 19:16:21</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #11ff7d; background: black;">0B3fiZHVzd0VqWk1RY3M          siteData-crypto.tar.gz      tar.gz    1.8<br /> GB    2017-07-07 19:16:13</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">0BUPib2t2aVlCYk85em8    <span dir="RTL" lang="AR-SA">     </span>god.mp3                     mp3       6.1 MB     2017-07-07<br /> 19:09:58</span>
  </p>
  
  <p class="MsoListParagraph" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #0d0d0d;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">اکنون<br /> شما یک بکاپ با<br /> موفقیت روی<br /> گوگل درایو<br /> آپلود کرده‌اید.<br /> حال می‌خواهیم<br /> فرآیند فوق را<br /> خودکار کنیم، به<br /> طوری که هر<br /> ۶ساعت یکبار<br /> این فرآیند<br /> انجام شود.<br /> برای اینکار<br /> ما نیاز داریم<br /> تا زمان‌بند<br /> کارهای سیستم<br /> را فعال کنیم.<br /> برای اینکار می‌توانید<br /> به سایت </span><span style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><a href="https://crontab-generator.org/"><span dir="LTR" style="color: #0d0dff;">crontab-generator</span></a><span lang="FA"><br /> مراجعه کنید و<br /> </span></span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> Task</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><br /> موردنظر خود<br /> را بسازید. چیزی<br /> که ما ساختیم<br /> آخرش این شد:</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <i><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">کار مربوط<br /> به بکاپ گیری<br /> از پایگاه<br /> داده</span></i><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">:</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #11ff7d; background: black;">0 */6 *<br /> * * /usr/bin/mysqldump &#8211;defaults-file=/home/repozitor/dbExport.conf<br /> &#8211;all-databases -u root | /usr/bin/openssl enc -aes-256-cbc -e -pass<br /> file:/home/repozitor/pass.txt > /home/repozitor/db-crypto.sql &&<br /> /usr/local/bin/gdrive update 0B3m5DM0xFdVhmRmc /home/repozitor/db-crypto.sql</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span dir="RTL" lang="FA" style="font-size: 13.0pt; font-family: 'Arial','sans-serif'; color: #11ff7d; background: black;"> </span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <i><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">کار مربوط<br /> به بکاپ گیری<br /> از فایل‌های<br /> مورد نیاز</span></i><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">:</span>
  </p>
  
  <p class="MsoNormal" style="margin-bottom: .0001pt; line-height: normal; text-autospace: none;">
    <span style="font-size: 13.0pt; font-family: Monaco; color: #11ff7d; background: black;">0 */6 *<br /> * * /bin/tar czpvf &#8211; /home/repozitor/Desktop | /usr/bin/openssl enc -aes-256-cbc<br /> -e -pass file:/home/repozitor/pass.txt > /home/repozitor/siteData-crypto.tar.gz<br /> && gdrive update 0B3fiZHVzd0VqWk1RY3M /home/repozitor/siteData-crypto.tar.gz</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">توجه: ذکر ۲<br /> نکته در مورد<br /> دستورات فوق<br /> ضروری می‌باشد:</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">عملگر </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">&&</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> باعث می‌شود<br /> که اگر فرآیند<br /> رمزگذاری<br /> ناموفق بود تا<br /> هنوز تمام نشده<br /> است، فرآیند<br /> آپلود شروع<br /> نشود(بین ۲<br /> دستور<br /> وابستگی از<br /> نوع ضروری<br /> ایجاد می‌کند).</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">حتما به<br /> جای </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">gdrive upload</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> باید از </span><span dir="LTR" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">gdrive<br /> update</span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"><br /> استفاده کنید<br /> تا نسخه‌های<br /> قبلی پشتیبان<br /> شما حفظ شود.<br /> این دستور<br /> بارها و بارها<br /> اجرا می‌شود.<br /> اما گوگل<br /> درایو فقط<br /> ۱۰۰نسخه‌ی پشتیبان<br /> آخر شما را<br /> حفظ می‌کند.<br /> بنابراین<br /> ۱۰۰*۶ ساعت<br /> زمان اخرین<br /> نسخه از پشتیبان<br /> شما خواهد<br /> بود.</span>
  </p>
  
  <p class="MsoListParagraph" dir="RTL" style="text-align: justify; text-indent: -.25in; direction: rtl; unicode-bidi: embed; margin: 0in .5in 10.0pt 0in;">
    <span style="font-size: 18.0pt; line-height: 115%; font-family: Symbol; color: #0d0d0d;">·<span style="font: 7.0pt 'Times New Roman';"><br /> </span></span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">در<br /> این مرحله<br /> باید دستور<br /> زیر را بزنید<br /> و کارهایی که<br /> ساخته‌اید در<br /> سیستم نصب شود<br /> و در زمان‌های<br /> مشخص اجرا<br /> شود:</span>
  </p>
  
  <p class="MsoNormal" style="text-align: justify;">
    <span style="font-size: 13.0pt; line-height: 115%; font-family: Monaco; color: #11ff7d; background: black;">crontab –e</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">با زدن این<br /> دستور یک محیط<br /> ویرایشگر<br /> متنی باز می‌شود.<br /> ۲کار فوق را<br /> که ساخته اید<br /> در اینجا<br /> بنویسید. سپس<br /> خارج شوید. در<br /> پایان به<br /> هنگام خروج از<br /> ویرایشگر به<br /> شما می‌گوید<br /> که کارها را<br /> روی سیستم نصب<br /> کرده است.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: red;">توجه: </span><span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">چنانچه<br /> در هر مرحله<br /> از پیاده‌سازی<br /> روش فوق برای<br /> شما سوالی پیش<br /> آمد، حتما در<br /> بخش نظرات(انتهای<br /> همین صفحه)<br /> سوال خود را<br /> مطرح کنید.<br /> سوال/پاسخ شما<br /> ممکن‌است<br /> برای دیگران<br /> مفید باشد. از<br /> ارسال ایمیل/پیام<br /> شخصی در این<br /> مورد<br /> بپرهیزید.</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;"> </span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">موفق باشید</span>
  </p>
  
  <p class="MsoNormal" dir="RTL" style="text-align: justify; direction: rtl; unicode-bidi: embed;">
    <span lang="FA" style="font-size: 18.0pt; line-height: 115%; font-family: IRRoya; color: #0d0d0d;">جواد زندی</span>
  </p>
</div>

<!--more-->

<!--more-->

<!--more-->

&nbsp;

&nbsp;