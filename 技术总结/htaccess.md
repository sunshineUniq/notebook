.htaccess使用方法介绍

1- .htaccess文件使用前提

实现url改写：当浏览器通过url访问到服务器某个文件夹时，这个文件就是描述具体如何处理该URL的

实际应用： 通过友好的url吸引用户，然后用.htaccess把用户带到需要访问的位置。

要想使用这个强大功能，就得开启apache里面的重写模块。

2- 基本语法介绍

开启重写引擎 ```RewriteEngine on```

说明重写的根目录： ``RewriteBase / ``

匹配所有符合条件的请求：```RewriteCond ```

```js
// RewriteBase 因为定义了这个文件夹，所以对应的替换就有了一个参照。
// RewriteCond 定义了一系列规则条件，这个指令可以有一条或者多条，只有用户的url符合这些条件之后，.htaccess才开始接待， 否则用户直接去访问所需要的目录了
```

For example:

用户访问地址 yqb.com 我们通常重定向到www.yqb.com

```javascript
RewriteEngine On
RewriteCond %{HTTP_HOST} ^yqb\.com$[NC] 
RewriteRule ^(.*)$ http://www.yqb.com/${1} [R=301, L]
```

解释

```javascript
%{HTTP_HOST} -- 获取用户访问的URL的主域名 然后后面是一个正则表达式，意思是是否是 yqb.com
如果用户访问的url满足所有RewriteCond提出的条件，那么进行下一步ReriteRule即开始进行引导， 这才开始实现.htaccess文件的重要功能

RewriteRule同样前面是正则表达式，分析用户除了主域名yqb.com之外的URL， ^(.*)$ 意思就是所有的内容，然后空格后面写的是我们引导用户访问的目录，我们带着他走到新的一个域名上。$1 指的是前面括号里匹配url所得到的内容。
```

Exp2:

我们来分析一下 [discuz7.0 搜索引擎优化 htaccess ](http://www.phplamp.org/2009/01/discuz7-htaccess-download/)里面的重写。

RewriteRule ^forum-([0-9]+)-([0-9]+)\.html$  forumdisplay.php?fid=$1&page=$2

首先加入用户通过 nbphp.com/forum-2-3.html 访问discuz论坛，那么先通过.htaccess过滤，看看是否需要.htaccess引导一下用户，如果满足列出的一系列RewriteCond的条件那么就进行重写，discuz的没有列出RewriteCond 所以应该全部都进行重写。所以开始进行转写，forum-2-3.html 这个正好符合 列出的^forum-([0-9]+)-([0-9]+)\.html$ 正则表达式。并且 $1 为 2  ，$2为3 ，所以代入后面，即 forumdisplay.php?fid=2&page=3 加上前面的RewriteBase 指定的文件目录，那么就带他到制定目录的forumdisplay.php?fid=2&page=3 。

3- 常见的.htaccess应用举例

- 防止盗链

  如果来得要访问jpe jpg bmp png结尾的url 用户不是来自我们的网站，那么让他看一张我们网站的展示图片

```
RewriteEngine On
RewriteCond %{HTTP_REFERER} !^http://(.+.)?mysite.com/ [NC]
RewriteCond %{HTTP_REFERER} !^$
RewriteRule .*.(jpe?g|gif|bmp|png)$ /images/nohotlink.jpg [L]
```

- 网站升级的时候，只有特定IP才能访问，其他的用户将看到一个升级页面

```
RewriteEngine on
RewriteCond %{REQUEST_URI} !/upgrade.html$
RewriteCond %{REMOTE_HOST} !^24\.121\.202\.30
RewriteRule $ http://www.nbphp.com/upgrade.html [R=302,L]
```

- 把老域名转向新域名

```
# redirect from old domain to new domain

RewriteEngine On
RewriteRule ^(.*)$ http://www.yourdomain.com/$1[R=301,L]
```

### 4、一些其他功能

#### 4.1 引出错误文档的目录

ErrorDocument 400 /errors/badrequest.html

ErrorDocument 404  http://yoursite/errors/notfound.html

ErrorDocument 401 “Authorization Required

#### 4.2 Blocking users by IP 根据IP阻止用户访问

order allow,deny

deny from 123.45.6.7

deny from 12.34.5. (整个C类地址)

allow from all

#### 4.3 防止目录浏览

\# disable directory browsing

Options All -Indexes

#### 4.4设置默认首页

\# serve alternate default index page

DirectoryIndex about.html

#### 4.5 把一些老的链接转到新的链接上——搜索引擎优化SEO

Redirect 301 /d/file.htmlhttp://www.htaccesselite.com/r/file.html

#### 4.6为服务器管理员设置电子邮件。

ServerSignature EMail

SetEnv SERVER_ADMINdefault@domain.com

5- 项目配置 .htaccess

```
<ifModule mod_rewrite.c>

  # Make apache follow sym links to files
  Options +FollowSymLinks
  # If somebody opens a folder, hide all files from the resulting folder list
  IndexIgnore */*


  # Enable rewriting
  RewriteEngine On

  # If its not HTTPS
  RewriteCond %{HTTPS} off

  # Comment out the RewriteCond above, and uncomment the RewriteCond below if you're using a load balancer (e.g. CloudFlare) for SSL
  # RewriteCond %{HTTP:X-Forwarded-Proto} !https

  # Redirect to the same URL with https://, ignoring all further rules if this one is in effect
  RewriteRule ^(.*) https://%{HTTP_HOST}/$1 [R,L]

  # If we get to here, it means we are on https://

  # If the file with the specified name in the browser doesn't exist
  RewriteCond %{REQUEST_FILENAME} !-f

  # and the directory with the specified name in the browser doesn't exist
  RewriteCond %{REQUEST_FILENAME} !-d

  # and we are not opening the root already (otherwise we get a redirect loop)
  RewriteCond %{REQUEST_FILENAME} !\/$

  # Rewrite all requests to the root
  RewriteRule ^(.*) /

</ifModule>

<IfModule mod_headers.c>
  # Do not cache sw.js, required for offline-first updates.
  <FilesMatch "sw\.js$">
    Header set Cache-Control "private, no-cache, no-store, proxy-revalidate, no-transform"
    Header set Pragma "no-cache"
  </FilesMatch>
</IfModule>

```

