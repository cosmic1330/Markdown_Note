# 上傳 Plesk Server地雷
## 1. IIS無法讀取附加的語言檔案格式
 > 出現以下錯誤訊息，請依指示操作

![錯誤訊息](https://user-images.githubusercontent.com/13773041/38497073-54f7ba70-3bef-11e8-8ccc-0dcc75abd625.PNG)

**更改web.config或.htaccess檔**，
在`<system.webServer>`中添加`<staticContent>內的tag`
```php
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <staticContent>
            <mimeMap fileExtension=".apk" mimeType="application/vnd.android.package-archive" />
            <mimeMap fileExtension=".properties" mimeType="text/x-java-properties" />
            <mimeMap fileExtension=".bcmap" mimeType="image/svg+xml" />
        </staticContent>
    </system.webServer>
</configuration>
```


## 2. IIS不支援.htaccess只支援web.config
以下是完整的web.config內容
```php
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <rewrite>
            <rules>
                <rule name="Rewrite to index.php">
                    <match url="index.php|robots.txt|images|test.php" />
                    <action type="None" />
                </rule>
                <rule name="Rewrite CI Index">
                    <match url=".*" />
                    <conditions>
                        <add input="{REQUEST_FILENAME}" pattern="css|js|jpg|jpeg|png|gif|ico|htm|html" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="index.php/{R:0}" />
                </rule>
            </rules>
        </rewrite>
        <staticContent>
            <mimeMap fileExtension=".apk" mimeType="application/vnd.android.package-archive" />
            <mimeMap fileExtension=".properties" mimeType="text/x-java-properties" />
            <mimeMap fileExtension=".bcmap" mimeType="image/svg+xml" />
        </staticContent>
    </system.webServer>
</configuration>
```

## 3. 前台xhr無法判定https直接像http請求
> 如果警告訊息顯示以下

`Mixed Content: The page at 'https://page.com' was loaded over HTTPS, but requested an insecure XMLHttpRequest endpoint 'http://XX.XXX.XX.XXX/vicidial/non_agent_api.php?queries=query=data'. This request has been blocked; the content must be served over HTTPS.`

則在`<head>`中增加`<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests"> `