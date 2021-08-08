非对称加密算法
需要两个密钥：公开密钥（publickey）和私有密钥（privatekey）。
公开密钥与私有密钥是一对，如果用公开密钥对数据进行加密，只有用对应的私有密钥才能解密；
如果用私有密钥对数据进行加密，那么只有用对应的公开密钥才能解密。
因为加密和解密使用的是两个不同的密钥，所以这种算法叫作非对称加密算法。
注意以上的一个点，公钥加密的数据，只有对应的私钥才能解密

在日常使用中是酱紫的：
将私钥private_key.pem用在服务器端，公钥发放给android跟ios等前端
客户端用公钥加密过后，数据只能被拥有唯一私钥的服务器看懂。


下载开源RSA密钥生成工具openssl（通常Linux系统都自带该程序），解压缩至独立的文件夹，进入其中的bin目录，执行以下命令：

第一条命令生成原始 RSA私钥文件 rsa_private_key.pem
```shell
openssl genrsa -out rsa_private_key.pem 1024
```
第二条命令将原始 RSA私钥转换为 pkcs8格式
```shell
openssl pkcs8 -topk8 -inform PEM -in rsa_private_key.pem -outform PEM -nocrypt -out private_key.pem
```

第三条生成RSA公钥 rsa_public_key.pem
```shell
openssl rsa -in rsa_private_key.pem -pubout -out rsa_public_key.pem
```

上面几个就可以看出：通过私钥能生成对应的公钥