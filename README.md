<h1 align="center">Jellyfin Android TV</h1>
<h3 align="center">Part of the <a href="https://jellyfin.org">Jellyfin Project</a></h3>

---

<p align="center">
<img alt="Logo banner" src="https://raw.githubusercontent.com/jellyfin/jellyfin-ux/master/branding/SVG/banner-logo-solid.svg?sanitize=true"/>
<br/><br/>
<a href="https://github.com/jellyfin/jellyfin-androidtv">
<img alt="GPL 2.0 License" src="https://img.shields.io/github/license/jellyfin/jellyfin-androidtv.svg"/>
</a>
<a href="https://github.com/jellyfin/jellyfin-androidtv/releases">
<img alt="Current Release" src="https://img.shields.io/github/release/jellyfin/jellyfin-androidtv.svg"/>
</a>
<a href="https://translate.jellyfin.org/projects/jellyfin-android/jellyfin-androidtv/">
<img alt="Translation Status" src="https://translate.jellyfin.org/widgets/jellyfin-android/-/jellyfin-androidtv/svg-badge.svg"/>
</a>
<br/>
<a href="https://opencollective.com/jellyfin">
<img alt="Donate" src="https://img.shields.io/opencollective/all/jellyfin.svg?label=backers"/>
</a>
<a href="https://features.jellyfin.org">
<img alt="Feature Requests" src="https://img.shields.io/badge/fider-vote%20on%20features-success.svg"/>
</a>
<a href="https://matrix.to/#/+jellyfin:matrix.org">
<img alt="Chat on Matrix" src="https://img.shields.io/matrix/jellyfin:matrix.org.svg?logo=matrix"/>
</a>
<br/>
<a href="https://play.google.com/store/apps/details?id=org.jellyfin.androidtv">
<img width="153" alt="Jellyfin on Google Play" src="https://jellyfin.org/images/store-icons/google-play.png"/>
</a>
<a href="https://www.amazon.com/gp/aw/d/B07TX7Z725">
<img width="153" alt="Jellyfin on Amazon Appstore" src="https://jellyfin.org/images/store-icons/amazon.png"/>
</a>
<a href="https://f-droid.org/en/packages/org.jellyfin.androidtv/">
<img width="153" alt="Jellyfin on F-Droid" src="https://jellyfin.org/images/store-icons/fdroid.png"/>
</a>
<br/>
<a href="https://repo.jellyfin.org/releases/client/androidtv/">Download archive</a>
</p>

Jellyfin Android TV is a Jellyfin client for Android TV, Nvidia Shield, and Amazon Fire TV devices. We welcome all contributions and pull
requests! If you have a larger feature in mind please open an issue so we can discuss the implementation before you start. 

## Building

The app uses Gradle and requires the Android SDK. We recommend using Android Studio, which includes all required dependencies, for
development and building. For manual building without Android Studio make sure a compatible JDK and Android SDK are installed and in your
PATH, then use the Gradle wrapper (`./gradlew`) to build the project with the `assembleDebug` Gradle task to generate an apk file:

```shell
./gradlew assembleDebug
```

The task will create an APK file in the `/app/build/outputs/apk/debug` directory. This APK file uses a different app-id from our stable
builds and can be manually installed to your device.

To build an optimized release APK for sideloading, run:

```shell
./gradlew assembleRelease
```

The task will create a signed APK file in the `/app/build/outputs/apk/release` directory. If no release keystore is configured, Gradle signs
the release APK with your local debug keystore so Android TV devices can install it. Builds signed this way are still release builds, but
Android only allows an installed APK to be updated by another APK signed with the same keystore/signing key. That means a build signed with
your local debug keystore, a different local release keystore, or any other non-matching key cannot update the official Jellyfin app or any
other installation signed with a different key; uninstall the existing app first, or configure and consistently use your own release keystore
with the `KEYSTORE_FILE`, `KEYSTORE_PASSWORD`, `SIGNING_KEY_ALIAS`, and `SIGNING_KEY_PASSWORD` environment variables.

For CI builds that should support in-place updates between artifacts, configure a dedicated non-production keystore in repository secrets so
the same key is used on every run. You can create one without Android Studio using the JDK `keytool` command:

```shell
keytool -genkeypair -v \
  -keystore ci-release-signing.jks \
  -alias ci-release \
  -keyalg RSA -keysize 2048 -validity 10000
base64 < ci-release-signing.jks | tr -d "\n"
```

Store the base64 output and passwords in `CI_RELEASE_KEYSTORE_BASE64`, `CI_RELEASE_KEYSTORE_PASSWORD`, `CI_RELEASE_KEY_ALIAS`, and
`CI_RELEASE_KEY_PASSWORD` repository secrets. The `App / Build` workflow uses these values automatically when present.

## Branching

The `master` branch is the primary development branch and the target for all pull requests. It is **unstable** and may contain breaking
changes or unresolved bugs. For production deployments and forks, always use the latest `release-x.y.z` branch. Do not base production work
or long-lived forks on `master`.

Release branches are created at the start of a beta cycle and are kept up to date with each published release. Maintainers will cherry-pick
selected changes into release branches as needed for backports. These branches are reused for subsequent patch releases.

## Translating

Translations can be improved very easily from our [Weblate](https://translate.jellyfin.org/projects/jellyfin-android/jellyfin-androidtv)
instance. Look through the following graphic to see if your native language could use some work! We cannot accept changes to translation
files via pull requests.

<p align="center">
<a href="https://translate.jellyfin.org/engage/jellyfin-android/">
<img alt="Detailed Translation Status" src="https://translate.jellyfin.org/widgets/jellyfin-android/-/jellyfin-androidtv/multi-auto.svg"/>
</a>
</p>
