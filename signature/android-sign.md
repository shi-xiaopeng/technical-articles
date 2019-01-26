```
jarsigner -verbose -keystore shangcaixiaoyouhui.jks -signedjar caida_133_signed.apk caida_133_j.apk shangcai


jarsigner -verbose -keystore android.keystore -signedjar signed_name.apk Before_sign.apk alias_name

1）jarsigner是工具名称，-verbose表示将签名过程中的详细信息打印出来，显示在dos窗口中；

2）-keystore android.keystore 表示签名所使用的数字证书和所在位置，这里没有写路径，表示在当前目录下；

3）-signedjar Last_gongs_sign.apk Before_sign.apk 表示给 Before_sign.apk文件签名，签名后的文件名称为Last_gongs_sign.apk；

4）最后面的android.keystore 表示证书的别名
```
- 查看签名信息
-- 查看apk签名信息
jarsigner -verify -verbose -certs <your_apk_path.apk>
-- 查看keystore的信息
keytool -list -keystore demo.keystore -alias mykey -v
-- 查看keystore


