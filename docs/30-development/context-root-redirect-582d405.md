<!-- loio582d4056ea7c44a7a315e37ca2a5a64b -->

# Context Root Redirect

The SAP Java Buildpack provides a context root redirect functionality.

When you call a Web application without adding its runtime \([Tomcat](application-containers-83d2416.md#loioddfc10180fe844049cc71f6989942dc2), [TomEE](application-containers-83d2416.md#loioa9590c2f5ebc4d1586d9f0f53a60cfdc) or [TomEE 7](application-containers-83d2416.md#loio79c039ab43b946a7b50c5d0326a3b40b)\) context path to the URL, it will be automatically appended.

**Example**:

If you have configured `/test_context_path` as a context path, and the Web application is available on `/test_app`, when you call:

```
<HOST>:<PORT>/test_app
```

you'll be redirected to:

```
<HOST>:<PORT>/test_context_path/test_app
```

The default context path value for Tomcat, TomEE, and TomEE 7 is ***""*** \(Empty String\).

For more information on how to change this default value, see: [Tomcat](application-containers-83d2416.md#loioddfc10180fe844049cc71f6989942dc2), [TomEE](application-containers-83d2416.md#loioa9590c2f5ebc4d1586d9f0f53a60cfdc), and [TomEE 7](application-containers-83d2416.md#loio79c039ab43b946a7b50c5d0326a3b40b).
