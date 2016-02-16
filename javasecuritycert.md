# java.security.cert

## Certificate 

管理证书的抽象类，证书可以有多种类型，比如x509, PGP, SDSI。X509Certificates是Certifate的一个具体实现（也是抽象类）

## CertificateFactory 

使用CertificateFactory导入存在的证书

## CertPath 

证书链

```java
CertificateFactory cf = CertificateFactory.getInstance("X.509");
FileInputStream fis = new FileInputStream("key_file");
CertPath crtPath = cf.generateCertPath(fis);
in.close();
```

## CRL 

验证证书是否已经被revoke 

```java
CertificateFactory cf = CertificateFactory.getInstance("X.509");
FileInputStream fis = new FileInputStream("key_file");
CRL crl = cf.generateCRL(fis);
System.out.printn(crl.isRevoked(cf.generateCertificate(fis)));
in.close();
```

