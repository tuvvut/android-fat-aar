
因為透過 Android Gradle Plugin 打包的 AAR，不會包含透過 Maven 依賴的 AAR&JAR 或是 Local 的 AAR，所以如果發佈了一個自己的 Library，其他使用此 Library 的開發者必須自行 Dependencies 相關的檔案。

為了方便開發者使用，我們可以透過以下作法來產生一個包含所有 AAR&JAR 的 AAR。

1. 在 Library 專案裡的 build.gradle 加一行
`apply from: 'https://raw.githubusercontent.com/tuvvut/android-fat-aar/master/fat-aar.gradle'`

2. 對於 dependencies 裡 compile AAR 的指令改成 embedded AAR.
例如：

`compile 'xxx.xxx.xxx:library:1.0.0-SNAPSHOT@aar'`

改成

`embedded 'xxx.xxx.xxx:library:1.0.0-SNAPSHOT@aar'`

或是

`compile(name: 'library-1.0.0-SNAPSHOT', ext: 'aar')`

改成

`embedded(name: 'library-1.0.0-SNAPSHOT', ext: 'aar')`

3. 將產生的 AAR 檔給其他開發者用就行了

路徑範例：../yourLibrary/build/outputs/aar/yourLibrary-release.aar

結束！

註：目前只針對 release 的 AAR 有用

參考資料：
1. 將 JAR 包進 AAR https://gist.github.com/qrtt1/25a44fa29e46a5ec7f5b
	
2. 將 AAR 包進 AAR https://github.com/adwiv/android-fat-aar
	
3.更詳細的說明請參考：https://github.com/adwiv/android-fat-aar
