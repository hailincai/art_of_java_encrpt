# java.secrity package

## Key class 
Key class是密钥接口的顶层接口，每个密钥有3个通用的属性  

* 算法，密钥的算法，如DES, DSA. ```getAlgorithm()```
* 外部编码形式，比如x509 / pcks #8. ```getEncoded()```
* 已编码密钥的格式的名称(?). ```getFormat()```

# SecurityKey, PublicKey and PrivateKey  

### SecurityKey

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

非对称密钥生成器

```java
KeyPairGenerator kpg = KeyPairGenerator.getInstance("DSA");
kpg.initialize(1024);
KeyPair keys = kpg.genKeyPair();
```

## KeyFactory 

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