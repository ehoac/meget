# keytool
keytool -genkeypair -alias ehoac -keyalg RSA -keypass ehoacsec -keystore ehoac.jks -storepass ehoacsec

### 迁移到行业标准格式 PKCS12
keytool -importkeystore -srckeystore ehoac.jks -destkeystore ehoac.jks -deststoretype pkcs12

### 查看keystore内容
keytool -list -rfc --keystore ehoac.jks | openssl x509 -inform pem -pubkey