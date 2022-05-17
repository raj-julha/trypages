# Anything That can be handy

## log4net

See https://logging.apache.org/log4net/release/manual/configuration.html

https://logging.apache.org/log4net/log4net-1.2.13/release/sdk/log4net.ILog.IsDebugEnabled.html

```xml
<log4net>
    <appender name="DatedDebugFileAppender" type="log4net.Appender.RollingFileAppender">
        <file value="D:\Logs\${COMPUTERNAME}-appname"/>
        <staticLogFileName value="false"/>
        <appendToFile value="true"/>
        <datePattern value="yyyyMMdd"/>
        <lockingModel type="log4net.Appender.FileAppender+MinimalLock"/>
        <rollingStyle value="Date"/>
        <datePattern value=".yyyyMMdd&quot;.debug&quot;"/>
        <filter type="log4net.Filter.LevelRangeFilter">
            <acceptOnMatch value="true"/>
            <levelMin value="DEBUG"/>
            <levelMax value="DEBUG"/>
        </filter>
        <layout type="log4net.Layout.PatternLayout">
            <conversionPattern value="[%date{yyyy-MM-dd HH:mm:ss.fff}] [%t] %-5p %c [%method] - %message%newline"/>
        </layout>
    </appender>   
    
    <root>
        <!-- set value attribute of level to ALL to include debug logs and INFO to exclude logs 
             when value is ALL the log.IsDebugEnabled flag is true
             when value is INFO the log.IsDebugEnabled flag is false
        -->
        <level value="ALL"/>
        <!-- <level value="INFO"/> -->
        <appender-ref ref="DatedLogFileAppender"/>
        <appender-ref ref="DatedErrorFileAppender"/>
        <appender-ref ref="DatedDebugFileAppender"/>
    </root>
</log4net>
```

```csharp
/// <summary>
/// </summary>
public class SomeClass
{
    #region  Logging

    private static readonly ILog log = LogManager.GetLogger(MethodBase.GetCurrentMethod().DeclaringType);
    private static readonly bool isDebugEnabled = log.IsDebugEnabled;
    #endregion


    private void DoSomething() 
    {
        if(isDebugEnabled)
        {
            log.Debug("Show Debug details");
        }
    
    }
}
```
