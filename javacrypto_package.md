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