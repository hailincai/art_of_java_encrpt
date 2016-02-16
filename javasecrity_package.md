# java.secrity package

## Key class 
Key class是密钥接口的顶层接口，每个密钥有3个通用的属性  

* 算法，密钥的算法，如DES, DSA. ```getAlgorithm()```
* 外部编码形式，比如x509 / pcks #8. ```getEncoded()```
* 已编码密钥的格式的名称(?). ```getFormat()```

# SecurityKey, PublicKey and PrivateKey  

### SecurityKey (???)

SecurityKey是对称密钥顶层接口, 对称加密技术使用对称密钥。Mac算法也使用SecurityKey接口来提供秘密密钥，具体的实现类是```SecurityKeySpec```.

### PublicKey and PrivateKey

它们是非对称密钥的顶层接口。具体的非对称密钥实现类包含DH（in ```java.crypto.interfaces```), RSA, DSA和EC (in ```java.security.interfaces```)

## AlgorithmParameters

提供密码参数的不透明表示 

```java
AlgorithmParameters ap = AlgorithmParameters.getInstance("DES");
ap.init(new BigInteger("19050619766489163472369").toByteArray());
byte[] b = ap.getEncoded();
//will output 19050619766489163472369
System.out.println(new BigInteger(b).toString());
```

## AlgorithmParameterGenerator  

用来生成AlgorithmParameters对象  

```java
AlgorithmParameterGenerator apg = AlgorithmParameterGenerator.getInstance("DES");
apg.init(56);
AlgorithmParameters ap = apg.generateParameters();
byte[] b = ap.getEncoded();
System.out.println(new BigInteger(b).toString());
```

## KeyPair

非对称密钥的载体，内部包含PublicKey和PrivateKey


## KeyPairGenerator  

```public class KeyPairGenerator extends KeyPairGenratorSpi```

非对称密钥生成器

```java
KeyPairGenerator kpg = KeyPairGenerator.getInstance("DSA");
kpg.initialize(1024);
KeyPair keys = kpg.genKeyPair();
```

## KeyFactory 

```public class KeyFactory extends Object```

根据密钥规范 ( ```KeySpec``` )，还原密钥. 与之对应的是```SecretKeyFactory```，用来产生秘密密钥 (?)

```java
KeyPairGenerator kpg = KeyPairGenerator.getInstance("RSA");
kpg.initialize(1024);
KeyPair kp = kpg.generateKeyPair();

byte[] keyBytes = kp.getPrivate().getEncoded();
PKCS8EncodedKeySpec keySpec = new PKCS8EncodedKeySpec(keyBytes); //why is this spec
KeyFactory kf = KeyFactory.getInstance("RSA");
Key privateKey = kf.generatePrivateKey(keySpec);
```

## SecureRandom

```public class SecureRandom extends Random```

产生强随机数，各种Security类初始化都会用到。

## Signature 

```public abstract class Signature extends SignatureSpi```

用于生成和验证数字签名，支持的算法包括```NONEWithDSA```, ```SHA1withDSA```, ```MD2withRSA```, ```MD5withRSA```, ```SHA1withRSA```, ```SHA256withRSA```, ```SHA384withRSA```

使用3步骤

* 初始化
* 更新
* 签署或者验证签名

```java
//签名初始化
void initSign(PrivateKey private)

//验证初始化
void initVerify(PublicKey public)
void initVerify(Certificate certificate)
```

```java
byte[] data = "Hello World".getBytes();
KeyPairGenerator kpg = KeyPairGenerator.getInstance("RSA");
kpg.initialize(1024);
KeyPair kp = kpg.generateKeyPair();

//signature
Signature sign = Signature.getInstance(kpg.getAlgorithm());
sign.initSign(kp.getPrivateKey());
sign.update(data);
byte[] signResult = sign.sign();

//verify signature
sign.initVerify(kp.getPublicKey());
sign.update(data);
sign.verify(signResult);
```

## KeyStore

```public class KeyStore extends Object```

用户管理密钥和证书的存储，基本使用的就2中类型JKS和PKCS12. PKCS12只读

## 其他对象 ```SignObject```, ```Timestamp```, ```CodeSigner```