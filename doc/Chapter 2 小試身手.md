# Chapter 2 小試身手
## 2-1 開發環境安裝
###2-1-1 安裝JDK 7

JDK 7 下載點: [Java SE Development Kit 7 Downloads](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

根據自己的電腦的作業喜統版本，選擇對應 JDK 版本進行安裝

![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/master/img/ch2-01.jpg)

###2-1-2 安裝 Eclipse

Eclipse 下載點: [Eclipse IDE for Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/keplersr2)

![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/master/img/ch2-02.jpg)

根據自己的電腦的作業系統版本，選擇對應eclipse 版本進行安裝

###2-1-3 安裝 GAE 開發套件

1.開啟Eclipse

![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/master/img/ch2-03.jpg)

2.在Eclipse上方功能表列上**Help** -> **Instal New Software**

![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/master/img/ch2-04.jpg)

3.根據自己的Eclipse下載對應的GAE 開發套件

GAE 各版本開發套件下載路徑 <br>
Eclipse 4.4 (Luna)	Plugin for Eclipse 4.4 (Luna)	https://dl.google.com/eclipse/plugin/4.4 <br>
Eclipse 4.3 (Kepler)	Plugin for Eclipse 4.3 (Kepler)	https://dl.google.com/eclipse/plugin/4.3  <br>
Eclipse 3.8/4.2 (Juno)	Plugin for Eclipse 3.8/4.2 (Juno)	https://dl.google.com/eclipse/plugin/4.2 <br>

筆者Eclipse為Kepler，所以在輸入套件路徑如圖:

![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/master/img/ch2-05.jpg)
然後勾選:<br>
● Developer Tools <br>
● Google Plugin for Eclipse <br>
● SDKs<br> 
勾選這三項後，下一步，同意條款，進行套件安裝。

###2-1-4 修改 Eclipse 編碼

筆者建議將Eclipse 編碼改為UTF-8 ，支援轉換其他語系過程中，才不會變成亂碼。

1.**Windows -> Preferences**

![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/master/img/ch2-06.jpg)

2.**General -> Workspace -> UTF-8**

![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/9a17f501ce34854af2afd9a6f3f932adc19b3a64/img/ch2-07.jpg)


## 2-2 第一個 GAE 程式 (Hello, Google App Engin)，本機端
## 2-2 第一個 GAE 程式，如何發佈到雲端

* * *
### 參考資料
1.GAE 開發套件: [Using the Google Plugin for Eclipse](https://cloud.google.com/appengine/docs/java/tools/eclipse)
<br>
