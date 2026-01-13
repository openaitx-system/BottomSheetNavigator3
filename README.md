
<div align="right">
  <details>
    <summary >🌐 Language</summary>
    <div>
      <div align="center">
        <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=en">English</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=zh-CN">简体中文</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=zh-TW">繁體中文</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=ja">日本語</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=ko">한국어</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=hi">हिन्दी</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=th">ไทย</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=fr">Français</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=de">Deutsch</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=es">Español</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=it">Italiano</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=ru">Русский</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=pt">Português</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=nl">Nederlands</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=pl">Polski</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=ar">العربية</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=fa">فارسی</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=tr">Türkçe</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=vi">Tiếng Việt</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=id">Bahasa Indonesia</a>
        | <a href="https://openaitx.github.io/view.html?user=stefanoq21&project=BottomSheetNavigator3&lang=as">অসমীয়া</
      </div>
    </div>
  </details>
</div>

# Material3 BottomSheet Navigation

This library provides a navigation solution for Compose projects using Material3 BottomSheets. It allows you to define your BottomSheet as navigation routes, eliminating the need for the `androidx.compose.material.navigation` and ` androidx.compose.material:material` !
libraries. This simplifies your app's dependencies and ensures a consistent Material3 experience.
This library also leverages the new functionality from `androidx.navigation:navigation-compose:2.8.0-beta0X` to allow you to define routes with serialized classes.

[![Maven Central](https://img.shields.io/maven-central/v/io.github.stefanoq21/material3-navigation)](https://central.sonatype.com/artifact/io.github.stefanoq21/material3-navigation)

![Static Badge](https://img.shields.io/badge/minSdk-21-blue?link=https%3A%2F%2Fgithub.com%2Fstefanoq21%2FBottomSheetNavigator3%2Fblob%2Fmain%2Fmaterial3-navigation%2Fbuild.gradle.kts%23L15)

## Implementation

You can follow the implementation approach used in the  [app](https://github.com/stefanoq21/BottomSheetNavigator3/tree/main/app "app") module. Alternatively, you can find a detailed explanation below.

### Dependencies
The library is now available on MavenCentral!!! 
Add the dependencies to your `libs.versions.toml`
```
[versions]
...
material3Navigation = "X.X.X" current release version

[libraries]
...
material3-navigation = { group = "io.github.stefanoq21", name = "material3-navigation", version.ref = "material3Navigation" }

```
In your `build.gradle.kts` implement your dependencies:
```
...
dependencies {
...
 implementation(libs.material3.navigation)
```
### Usage
Define your **BottomSheetNavigator**
```
...
   val bottomSheetNavigator =
                    rememberBottomSheetNavigator(skipPartiallyExpanded = true/false)
                val navController = rememberNavController(bottomSheetNavigator)
```
Add the **ModalBottomSheetLayout** on top of the **NavHost** component and pass the **bottomSheetNavigator** as parameter:
```
ModalBottomSheetLayout(
                        modifier = Modifier
                            .fillMaxSize(),
                        bottomSheetNavigator = bottomSheetNavigator
                    ) {
                        NavHost(
                            navController = navController,
                            startDestination = Screen.Home
                        ) {
...
```
Define your routes as strings or data class (depend on the compose navigation version you are using):
```
...
   bottomSheet<Screen.BottomSheetFullScreen> {
                                BSFullScreenLayout()
                            }
  bottomSheet("BottomSheetFullScreen") {
                                BSFullScreenLayout()
                            }
...
```
Everything is ready! Just navigate to your new destination as usual:
```
...
Button(onClick = { navController.navigate(Screen.BottomSheetFullScreen) }) {
                                        Text(text = "BottomSheetFullScreen")
                                    }
...
```

### Navigating Back from a Bottom Sheet

To implement a back or close button in your bottom sheet, I suggest to use `onBackPressedDispatcher.onBackPressed()`. This because if you use  `navController.popBackStack()` the animation will not appear. The animation was disabled, in this case, to avoid problems during the navigation that start from bottomshets.

### Customization

The library currently supports the same customization options of the standard `androidx.compose.material3.ModalBottomSheet`. You can customize the appearance of the all the bottomsheets used in your navigation graph by passing the parameters to the `ModalBottomSheetLayout`.

## Preview
![](https://github.com/stefanoq21/BottomSheetNavigator3/assets/22545898/c971f6cf-bb04-41c1-b3ea-7b72757e09af)


## Contributing

We welcome contributions to this library! If you have bug reports, feature requests, or code improvements, please feel free to create a pull request. I appreciate your help in making this library even better.

## License

   Copyright 2024 stefanoq21

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.

