[toc]

## ddos

## 中间人攻击

## cors

## csrf

## 安全

1. 始终使用 HTTPS
2. 使用密码哈希
3. 永远不要公开 URL 的信息
4. 考虑 OAuth
5. 考虑在请求中添加时间戳
6. 输入|出参数验证

## 哈希[摘要] & 加密

- 对称加密{aes/des/des3} & 非对称加密{rsa}
- 摘要算法: sha256/md5

0. 对称加密与非对称加密: 都可以解密

   - 对称加密: 加密方/解密方 都使用同一个密钥, DES/AES
   - 非对称加密: 加密方使用公钥加密, 解密方使用私钥解密{只}, RSA

1. 哈希是将目标文本转换成具有**相同长度**的, **不可逆**的杂凑字符串

   - hash 算法
   - md5
   - sha128/256
   - 漏洞: 暴力枚举法 + 字典法 + `彩虹表`
   - 解决: 加盐{在特定位置插入特定的字符串}
   - Bcrypt: 自适应性{加密速度一定} + 内部自己实现了随机加盐处理 + 每次密文不一样

     1. hash 产生过程: 先随机生成 salt, salt 跟 password 进行 hash
     2. 下次校验时, 从 hash 中取出 salt, salt 跟 password 进行 hash, 结果与 db 对比

     ```shell
     $2b$[cost]$[22 character salt][31 character hash]

     $2a$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy
     \__/\/ \____________________/\_____________________________/
     Alg Cost      Salt                        Hash

     $2a$ 表示的hash算法的唯一标志: 这里表示的是Bcrypt算法
     10 表示的是代价因子, 这里是2的10次方, 也就是1024轮
     ```

2. 加密是将目标文本转换成具有不同长度的, **可逆**的密文

   - 对称加密: aes/des/des3
   - 非对称加密: rsa
