# راهنمای ساخت APK (اندروید)

## گزینه A: Android Studio و WebView
1. Android Studio را نصب و یک پروژه Empty Views Activity با Kotlin بسازید.
2. فایل‌های `www/index.html`، `manifest.webmanifest` و `sw.js` را به `app/src/main/assets/` کپی کنید.
3. در Activity یک WebView بسازید و `webView.settings.javaScriptEnabled = true` را تنظیم کنید؛ سپس `webView.loadUrl("file:///android_asset/index.html")` را اجرا کنید.
4. برای این نمونه آفلاین، مجوز اینترنت لازم نیست؛ اگر بعداً API OCR اضافه شد، مجوز INTERNET و سیاست حریم خصوصی لازم است.
5. از منوی Build گزینه Build APK(s) را انتخاب کنید. خروجی آزمایشی در مسیر `app/build/outputs/apk/` خواهد بود.
6. برای توزیع بیرون از محیط توسعه، نسخه release را با کلید امضای خودتان امضا کنید. کلید خصوصی را با کسی به اشتراک نگذارید.

نمونه Kotlin برای Activity:

```kotlin
package com.example.yarriazi

import android.os.Bundle
import android.webkit.WebView
import android.webkit.WebViewClient
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val webView = WebView(this)
        webView.webViewClient = WebViewClient()
        webView.settings.javaScriptEnabled = true
        setContentView(webView)
        webView.loadUrl("file:///android_asset/index.html")
    }
}
```

اگر پروژه از AndroidX/AppCompat استفاده نمی‌کند، Activity را با `android.app.Activity` پیاده کنید یا وابستگی AppCompat را اضافه کنید.

## گزینه B: Capacitor
با نصب Node.js و Android Studio، یک پروژه Capacitor بسازید، محتوای پوشه `www` را در پوشه وب پروژه کپی کنید، سپس `npx cap add android` و `npx cap open android` را اجرا کنید. دستورات دقیق ممکن است بسته به نسخه Capacitor تغییر کنند؛ راهنمای رسمی نسخه نصب‌شده را بررسی کنید.

## محدودیت
این مخزن سورس وب و راهنما را دارد، نه APK باینری ساخته‌شده. محیط فعلی Android SDK/Gradle برای کامپایل و امضای APK در اختیار ندارد.
