# OpenSSL utilities

This project collects some of the most useful commands available in the OpenSSL library



## Certificate utilities

##### GENERATE CERTIFICATE SIGNING REQUEST AND PRIVATE KEY

This command allows to generate a csr and a private key file

```
openssl req -out [FILE.csr] -new -newkey rsa:2048 -nodes -keyout [FILE.key]
```

##### GENERATE SELF SIGNED CERTIFICATE

This command allows to generate a self signed certificate along with private key

```
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout [FILE.key] -out [FILE.crt]
```

##### GENERATE PKCS12 FROM CRT AND PRIMARY KEY

This command allows to generate a PKCS#12 keystore from X.509 certificate and related private key

```
openssl pkcs12 -export -in [FILE.crt] -inkey [FILE.key] -out [KEYSTORE.p12] -name [ALIASNAME]
```

##### VIEW MD5 HASH MODULUS OF CRT, PRIVATE KEY OR CSR

This command is useful to ensure if certificate matches with csr or private key. The hash of crt, csr and private key must be the same

```
For SSL certificate: openssl x509 –noout –modulus –in [FILE.crt] | openssl md5
For RSA private key: openssl rsa –noout –modulus –in [FILE.key] | openssl md5
For CSR file: openssl req -noout -modulus -in [FILE.csr] | openssl md5
```



## File utilities

##### ENCODE FILE IN BASE64

This command allows to encode the content of file in base64

```
openssl base64 -in [INPUTFILE] -out [OUTPUTFILE]
```

##### DECODE FILE FROM BASE64 

This command allows to decode a base64 file in the original file 

```
openssl base64 -d -in [INPUTENCODEDFILE] -out [OUTPUTDECODEDFILE]
```

##### ENCRYPT FILE USING RSA 

This commands allows to encrypt a file using RSA algorithm (RSA public/private keys)

```
openssl rsautl -encrypt -in [INPUTFILE] -out [OUTPUTENCRYPTEDFILE] -inkey [RSAPUBLICKEY] -pubin
```

##### DECRYPT FILE USING RSA 

This commands allows to decrypt a file previously encrypted using RSA algorithm (RSA public/private keys)

```
openssl rsautl -decrypt -in [INPUTENCFILE] -out [OUTPUTDECRYPTEDFILE] -inkey [RSAPRIVATEKEY]
```



## Keystore utilities

##### CONVERT PKCS12 to JKS

This command allows to convert a PKCS#12 to a Java Key Store

```
keytool -importkeystore -srckeystore [KEYSTORE.p12] -srcstoretype pkcs12 -destkeystore [KEYSTORE.jks] -deststoretype jks -name [ALIASNAME]
```



##### VIEW KEYSTORE

This command allows to view content of a keystore

```
keytool -v -list -keystore [KEYSTORE] -storetype [KEYSTORE TYPE, default=JKS]
```



[OpenSSL library]: https://www.openssl.org/
[Typora editor]: https://typora.io/





