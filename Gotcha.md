This wiki documents all frequent errors and possible fixes on local environment

## 503 Service Unavailable

If you get the above error on first setup, you may need to update your hosts file to include the local URL. Edit `/etc/hosts` to include the following line:

```
127.0.0.1 gettingmarried-local.ampdev.co
```

## Asset manifest file "gettingmarried/public/build/manifest.json" does not exist.
`webpack-encore` creates a `manifest.json` file - this contains every mapping between a file and it's versioned self, which is used as a cachebuster. Although we don't necessarily need to use versioned files locally, this error still occurs; if it does, running `make assets` should generate the file and fix the issue.

As it changes every time the CSS or JS is changed, it doesn't seem ideal to commit this file to the repository.

## Got an unexpected update on notification-url in composer.lock

```diff
--- a/composer.lock
+++ b/composer.lock
@@ -4,7 +4,7 @@
         "Read more about it at https://getcomposer.org/doc/01-basic-usage.md#installing-dependencies",
         "This file is @generated automatically"
     ],
-    "content-hash": "ccfad7e76eebc61da9c3590c467a082f",
+    "content-hash": "991fcf4151a306dc962ec61e6178c65c",
     "packages": [
         {
             "name": "aferrandini/urlizer",
@@ -249,7 +249,7 @@
                     "ApiPlatform\\Core\\": "src/"
                 }
             },
-            "notification-url": "https://repo.packagist.com/ampersandhq/downloads/",
+            "notification-url": "https://packagist.org/downloads/",
             "license": [
                 "MIT"
             ],

```

With a symptoms like above, you should be able to tidy the composer.lock by running:

```bash
rm -rf vendor
composer install --prefer-source --optimize-autoloader
```