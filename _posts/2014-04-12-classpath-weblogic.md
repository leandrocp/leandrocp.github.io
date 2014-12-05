---
layout: post
title: classpath Weblogic 12
---

Arquivo:
wls12120\user_projects\domains\mydomain\bin\startWebLogic.cmd

Procurar:
```
set SAVE_JAVA_OPTIONS=%JAVA_OPTIONS%
```

Alterar:
```
set JAVA_OPTIONS=%JAVA_OPTIONS% -verbose:class
```

Init:
```

```

WL_HOME/server/lib/wls-cat.war


[http://c2.com/cgi/wiki?ClasspathHell](http://c2.com/cgi/wiki?ClasspathHell "http://c2.com/cgi/wiki?ClasspathHell")

[https://blogs.oracle.com/LuzMestre/entry/classloading_errors_in_weblogic_server](https://blogs.oracle.com/LuzMestre/entry/classloading_errors_in_weblogic_server "https://blogs.oracle.com/LuzMestre/entry/classloading_errors_in_weblogic_server")

[http://docs.oracle.com/cd/E24329_01/web.1211/e24368/classloading.htm#WLPRG495](http://docs.oracle.com/cd/E24329_01/web.1211/e24368/classloading.htm#WLPRG495 "http://docs.oracle.com/cd/E24329_01/web.1211/e24368/classloading.htm#WLPRG495")