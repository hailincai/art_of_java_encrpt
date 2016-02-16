# java.crypto package

为加密操作提供类和接口 

## Mac 

```public class Mac extends Object implements Cloneable```

和一般的摘要算法的不同在于，该算法需要一个双方共享的秘密密钥才能计算出摘要。Java支持```HmacMD5```, ```HmacSHA1```, ```HmacSHA256```, ```HmacSHA384```, ```HmacSHA512```.

```java
byte[] input = "hello world!".getBytes();
KeyGenerator kg = KeyGenerator.getInstance("HmacMD5");
SecretKey key = kp.generateKey();
Mac mac = Mac.getInstance(kp.getAlgorithm());
mac.init(key);
byte[] output = mac.doFinal(input);
```

## KeyGenerator

```public class KeyGenerator extends Object```

用来产生秘密密钥 SecretKey

## KeyAggrement ( skip for now, not need now )

```public class KeyAgreement extends Object```

密钥协定，在DH算法中将被使用


## SecretKeyFactory 

```java
KeyGenerator kg = KeyGenerator.getInstance("DES");
SecretKey key = kp.generateKey();
byte[] keyOutput = key.getEncoded();

DESKeySpec kspec = new DESKeySpec(keyOutput);
SecretKeyFactory kf = SecretKeyFactory.getInstance("DES");
SecretKey resotreKey = kf.generateSecret(kspec);
```

## Cipher 

```public class Cipher extends Object```

加解密核心类， 


```java
Cipher cipher = Cipher.getInstace("算法/工作模式/填充模式");
cipher.init(int opMode, Key)//opMode means加密还是解密
cipher.init(int opMode, Key, AlgorithmParameters)
cipher.init(int opMode, Key, AlgorithmParameterSpec)
//使用公钥初始化
cipher.init(int opMode, Certificate certificate);
```