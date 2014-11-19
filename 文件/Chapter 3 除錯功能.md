# Chapter 3 除錯功能

## 3-1 Log 日誌訊息
#### 範例:
Log_DemoServlet.java
```java
public class Log_DemoServlet extends HttpServlet {

	private static final Logger log = Logger.getLogger(Log_DemoServlet.class
			.getName());

	public void doGet(HttpServletRequest req, HttpServletResponse resp)
			throws IOException {
		log.finest("An finest message.");
		log.finer("An finer message.");
		log.fine("An fine message.");
		log.config("An config message.");
		log.info("An informational message.");
		log.warning("A warning message.");
		log.severe("An error message.");

	} // end doGet
}// end class
```
#### WEB-INF/logging.properties
設定印出Log 的等級，低於此等級則不會被印出來
```java
.level = INFO
```
以此 **INFO** 等級為例，所以 **finest、finer、fine、config** 等log訊息，將不會被印出來。
<br>
(設定 **INFO**，為 **INFO** 等級的會被印出來。)

## 3-2 中斷除錯

* * *
參考資料:
<br>
1.GAE官方說明文件: [Logs Java API Overview](https://cloud.google.com/appengine/docs/java/logs/)
<br>
2.GAE官方說明文件: [Javadoc Reference](https://cloud.google.com/appengine/docs/java/javadoc/com/google/appengine/api/log/package-summary)
<br>
3.GAE官方說明文件: [Using Cloud Logging in App Engine Apps](https://cloud.google.com/appengine/articles/logging)
