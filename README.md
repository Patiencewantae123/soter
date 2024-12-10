
# Hello TENCENT SOTER

[![License](http://img.shields.io/badge/license-BSD3-brightgreen.svg?style=flat)](https://github.com/Tencent/soter/blob/master/LICENSE)
[![Version](https://jitpack.io/v/Tencent/soter.svg)](https://jitpack.io/#Tencent/soter)
[![WeChat Approved](https://img.shields.io/badge/WeChat_Approved-2.0.0-red.svg)](https://github.com/Tencent/soter/wiki)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/Tencent/soter/pulls)

## Latest Release: 2.1.8
- Fixed known issues.

## Version 2.0.7 Update
- Released `aar` to Jitpack. For new dependency method, check [here](https://github.com/Tencent/soter#%E6%B7%BB%E5%8A%A0gradle%E4%BE%9D%E8%B5%96).

## Key Features in Version 2.0
- Added support for Huawei devices.
- Added support for Android 9.0 (Pie).
- Introduced facial recognition.
- Updated backend ASK parsing, details [here](https://github.com/Tencent/soter/wiki/%E5%AE%89%E5%85%A8%E6%8E%A5%E5%85%A5%E2%80%94%E2%80%94%E5%90%8E%E5%8F%B0).
- Changes to the `is_support` parameter, see [here](https://github.com/Tencent/soter/wiki/%E5%90%8E%E5%8F%B0%E6%8E%A5%E5%8F%A3%E6%96%87%E6%A1%A3).

## Overview of TENCENT SOTER

**TENCENT SOTER** is Tencent's biometric authentication platform and standard established in 2015. It is now supported on over 100 models and hundreds of millions of Android devices and continues to grow.

TENCENT SOTER is already implemented in use cases like WeChat fingerprint payment and fingerprint authentication in Official Accounts and Mini Programs.

With TENCENT SOTER, you can integrate **secure fingerprint authentication** without accessing users' fingerprint data, providing a seamless experience akin to WeChat’s fingerprint payment.

![Soter Framework](https://github.com/WeMobileDev/article/blob/master/assets/soter/SoterFramework.png)

## Quick Start Guide

Experience the power of TENCENT SOTER in just a few lines of code. Before you start, ensure your testing device is listed in the [supported models](http://mp.weixin.qq.com/s/IRI-RCGsVB2WiPwUCGcytA).

### Add Gradle Dependency

Add TENCENT SOTER to your `build.gradle`:

```groovy
repositories {
    ...
    maven {
        url "https://jitpack.io"
    }
    ...
}

dependencies {
    ...
    implementation 'com.github.Tencent.soter:soter-wrapper:2.0.7'
    ...
}
```

### Declare Permissions

Include the following in `AndroidManifest.xml`:

```xml
<queries>
    <package android:name="com.tencent.soter.soterserver" />
</queries>

<uses-permission android:name="android.permission.USE_FINGERPRINT" />
<uses-permission android:name="android.permission.USE_BIOMETRIC" />
```

### Initialization

Initialize TENCENT SOTER once in your app's lifecycle (e.g., `Application` class or before usage):

```java
InitializeParam param = new InitializeParam.InitializeParamBuilder()
    .setScenes(0) // Scene constant for key generation or fingerprint authentication
    .build();
SoterWrapperApi.init(context, new SoterProcessCallback<SoterProcessNoExtResult>() { ... }, param);
```

### Prepare Keys

Generate keys needed for fingerprint authentication:

```java
SoterWrapperApi.prepareAuthKey(new SoterProcessCallback<SoterProcessKeyPreparationResult>() { ... }, false, true, 0, null, null);
```

### Perform Fingerprint/Face Authentication

Authenticate users using the following code:

```java
AuthenticationParam param = new AuthenticationParam.AuthenticationParamBuilder()
    .setScene(0)
    .setContext(MainActivity.this)
    .setBiometricType(ConstantsSoter.FINGERPRINT_AUTH) // Use FINGERPRINT or FACEID
    .setSoterBiometricCanceller(mSoterBiometricCanceller)
    .setPrefilledChallenge("test challenge")
    .setSoterBiometricStateCallback(new SoterBiometricStateCallback() { ... })
    .build();
SoterWrapperApi.requestAuthorizeAndSign(new SoterProcessCallback<SoterProcessAuthenticationResult>() { ... }, param);
```

### Release Resources

Release TENCENT SOTER when not needed:

```java
SoterWrapperApi.release();
```

## Documentation and More

- [SOTER SDK Overview](https://github.com/Tencent/soter/wiki)
- For higher security needs (e.g., login, payment), see [here](https://github.com/Tencent/soter/wiki).

## Contact and Support

For issues, visit [GitHub Issues](https://github.com/Tencent/soter/issues) or join our QQ group for technical discussions:

![QQ Group QR Code](https://github.com/WeMobileDev/article/blob/master/assets/soter/SOTER%E4%BA%A4%E6%B5%81%E7%BE%A4%E7%BE%A4%E4%BA%8C%E7%BB%B4%E7%A0%81.png)

## Contributing

Check our [CONTRIBUTING guide](./CONTRIBUTING.md) for information on contributing.

## License

TENCENT SOTER is distributed under the [BSD License](./LICENSE).

## Compliance

Refer to the [Compliance Usage Guide](https://github.com/Tencent/soter/wiki/SOTER-Client-SDK%E5%90%88%E8%A7%84%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97).

## Information

- **SDK Name**: SOTER Client SDK
- **Version**: 2.1.8
- **Developer**: Shenzhen Tencent Computer Systems Company Limited
- **Main Function**: A complete, secure fingerprint authentication solution.
- [Usage Instruction](https://github.com/Tencent/soter/wiki)
- [Privacy Policy](https://github.com/Tencent/soter/wiki/SOTER-Client-SDK%E4%B8%AA%E4%BA%BA%E4%BF%A1%E6%81%AF%E4%BF%9D%E6%8A%A4%E8%A7%84%E5%88%99?from_wecom=1)

## Contribution Encouragement

Join the [Tencent Open Source Contribution Plan](https://opensource.tencent.com/contribution) and become a part of the growing TENCENT SOTER community!

---

Let me know if you'd like any adjustments or additional details!
