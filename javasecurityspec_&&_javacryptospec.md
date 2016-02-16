# java.security.spec && java.crypto.spec

## KeySpec ( java.security.spec ) 

        KeySpec
        |
        |----------------|
        SecretKeySpec   EncodedKeySpec ( abstract )
                         |
            |-------------------------------|
        X509EncodedKeySpec ( public key )   PKCS8EncodedKeySpec ( private key )

* SecretKeySpec 通用秘密密钥KeySpec，对于具体的对称密钥有相对应的类，for example, DESKeySepc

## AlgorithmParameterSpec ( java.security.spec )

