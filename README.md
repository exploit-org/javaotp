# JavaOTP
Lightweight yet powerful library to generate TOTP 2FA codes.

# Installation
Please note, that you should first add exploit.org's repository.

### Maven:
```xml
<repositories>
    <repository>
        <id>exploit</id>
        <name>Exploit Repository</name>
        <url>https://maven.exploit.org</url>
    </repository>
</repositories>
```
```xml
<dependency>
    <groupId>org.exploit</groupId>
    <artifactId>java-otp</artifactId>
    <version>1.0</version>
</dependency>
```

### Gradle:
```groovy
repositories {
    mavenCentral()

    maven {
        url("https://maven.exploit.org")
    }
}
```
```groovy
implementation 'org.exploit:java-otp:1.0'
```

# Usage
First you need to create instance of `TOTPGenerator` and pass there your `TOTPConfig`.
```java
public static void main(String[] args) {
    var hashAlgorithm = HashAlgorithm.SHA1;
    var otpLength = 6;
    var secretLength = 20;
    var timeStepSeconds = 30;

    // Please note, parameters above are used in default constructor new TOTPConfig()
    var config = new TOTPConfig(hashAlgorithm, otpLength, secretLength, timeStepSeconds);

    var generator = new TOTPGenerator(config);

    var secretKey = generator.generateSecret();
    var otpCode = generator.generate(secretKey);
}
```

`hashAlgorithm` - Hash algorithm used. Most common supported: SHA1, SHA256, SHA512.

`otpLength` - Length of temporary code produced.

`secretLength` - Length of secret key used for creating OTP keys.

`timeStepSeconds` - Time after which temporary code expires.

## Backup Codes
You can also generate short secure backup codes for users:
```java
public static void main(String[] args) {
    var count = 10;
    var length = 10;

    // Please note, parameters above are used in default constructor new BackupConfig()
    var config = new BackupConfig(count, length);
    var generator = new BackupCodeGenerator();

    var codes = generator.generateCodes();
    // Or just generate 1 code
    var code = generator.generateCode();
}
```

## License
JavaOTP is licensed under the BSD License. See [BSD](LICENSE) for more information.