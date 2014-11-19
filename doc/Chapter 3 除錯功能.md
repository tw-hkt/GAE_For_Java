# Chapter 3 除錯功能

## 3-1 Log 日誌訊息
### 3-1-1 打印日誌範例:
Log_DemoServlet.java
```java
public class Log_DemoServlet extends HttpServlet {

	private static final Logger log = Logger.getLogger(Log_DemoServlet.class
			.getName());

	public void doGet(HttpServletRequest req, HttpServletResponse resp)
			throws IOException {
		log.finest("finest message.");
		log.finer("finer message.");
		log.fine("fine message.");
		log.config("config message.");
		log.info("informational message.");
		log.warning("warning message.");
		log.severe("error message.");

	} // end doGet
}// end class
```
在WEB-INF/logging.properties 設定印出Log 的等級，低於此等級則不會被印出來
```java
.level = INFO
```
以此 **INFO** 等級為例，所以 **finest、finer、fine、config** 等log訊息，將不會被印出來。
<br>
(設定 **INFO**，為 **INFO** 等級的會被印出來。)

可以到**雲端專案控制台** -> **監控** -> **紀錄** 看到日誌訊息。
![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/master/img/ch3-01.png)
<br>
<br>
<br>
### 3-1-2 回撈日誌範例:
日誌分兩種: **請求**(request)和**應用程式**(application)。

獲取日誌的一般過程如下：

1.使用**LogQuery**指定哪些記錄返回。
<br>
2.使用**LogServiceFactory.getLogService()**來創建**LogService**
<br>
3.調用**LogServiceFactory.getLogService()**。fetch()方法返回一個迭代器請求日誌。
<br>
4.在每次迭代中，對於每個**RequestLogs**，根據需要處理該請求的屬性。
<br>
5.或者，使用**RequestLogs.getAppLogLines()**來獲得應用程序日誌（**AppLogLine**與此請求相關聯）。
<br>
6.獲取應用程序日誌，可以根據每個**AppLogLine**的屬性數據來獲取。

Log_DemoServlet.java
```java
public class Log_DemoServlet extends HttpServlet {

	private static final Logger log = Logger.getLogger(Log_DemoServlet.class
			.getName());

	public void doGet(HttpServletRequest req, HttpServletResponse resp)
			throws IOException {
	 resp.setContentType("text/html");
    PrintWriter writer = resp.getWriter();
    // We use this to break out of our iteration loop, limiting record
    // display to 5 request logs at a time. (設定顯示最近五筆)
    int limit = 5;

    // This retrieves the offset from the Next link upon user click.
    String offset = req.getParameter("offset");

    // We want the App logs for each request log
    LogQuery query = LogQuery.Builder.withDefaults();
    query.includeAppLogs(true);

    // Set the offset value retrieved from the Next link click.
    if (offset != null) {
      query.offset(offset);
    }

    // This gets filled from the last request log in the iteration
    String lastOffset = null;
    int i = 0;

    // Display a few properties of each request log.
    for (RequestLogs record : LogServiceFactory.getLogService().fetch(query)) {
      writer.println("<br />REQUEST LOG <br />");
      Calendar cal = Calendar.getInstance();
      cal.setTimeInMillis(record.getStartTimeUsec() / 1000);

      writer.println("IP: " + record.getIp()+"<br />");
      writer.println("Method: " + record.getMethod()+"<br />");
      writer.println("Resource " + record.getResource()+"<br />");
      writer.println(String.format("<br />Date: %s", cal.getTime().toString()));

      lastOffset = record.getOffset();

      // Display all the app logs for each request log.
      for (AppLogLine appLog : record.getAppLogLines()) {
        writer.println("<br />"+ "APPLICATION LOG" +"<br />");
        Calendar appCal = Calendar.getInstance();
        appCal.setTimeInMillis(appLog.getTimeUsec() / 1000);
        writer.println(String.format("<br />Date: %s",
                            appCal.getTime().toString()));
        writer.println("<br />Level: "+appLog.getLogLevel()+"<br />");
        writer.println("Message: "+ appLog.getLogMessage()+"<br /> <br />");
      } //for each log line

      if (++i >= limit) {
        break;
      }
    } // for each record

    // When the user clicks this link, the offset is processed in the
    // GET handler and used to cycle through to the next 5 request logs.
    //(根據offset位置，再來獲取五筆)
    writer.println(String.format("<br><a href=\"/?offset=%s\">Next</a>",
                             lastOffset));

	} // end doGet
}// end class
```
<br>
<br>
<br>

### 3-1-3 下載日誌範例:
Windows 命令方式，存到mylogs.txt記事本中，
```java
./appengine-java-sdk/bin/appcfg.cmd request_logs myapp/war mylogs.txt
```
預設下載 log 的等級為INFO，濾掉debug等級(finest、finer、fine、config)的訊息。
<br>
<br>
<br>
## 3-2 中斷除錯
在本地端，可以在程式碼中，設立中斷點，執行逐行除錯模式

![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/b194025967374c3ab609e2c879e78a42c93c48ed/img/ch3-02.png)

<br>
可以加入想要監看的變數來進行邏輯驗證運算判斷

![](https://raw.githubusercontent.com/tw-hkt/GAE_For_Java/master/img/ch3-03.png)

<br>
<br>
<br>
## 3-3 傻瓜除錯

### 3-3-1 HTML 輔助
將變數或邏輯結果直接印在前端網頁上
```java
<p></p>
```

### 3-3-2 JavaScript 輔助
彈出對話視窗
```java
alert();
```

* * *
### 參考資料
1.GAE官方說明文件: [Logs Java API Overview](https://cloud.google.com/appengine/docs/java/logs/)
<br>
2.GAE官方說明文件: [Javadoc Reference](https://cloud.google.com/appengine/docs/java/javadoc/com/google/appengine/api/log/package-summary)
<br>
3.GAE官方說明文件: [Using Cloud Logging in App Engine Apps](https://cloud.google.com/appengine/articles/logging)
<br>
4.GAE官方說明文件: [logs-related quotas](https://cloud.google.com/appengine/docs/quotas#Logs)
<br>
5.GAE官方說明文件: [Downloading logs from App Engine](https://cloud.google.com/appengine/docs/java/tools/uploadinganapp#Downloading_Logs)
<br>
6.GAE官方說明文件: [log level](https://cloud.google.com/appengine/docs/java/tools/uploadinganapp#command_line_arguments_appcfg_severity)
