# ApsaraDB for Memcache {#concept_fvw_vt4_ydb .concept}

CloudMonitor provides seven monitoring metrics for ApsaraDB for Memcache, including cache used and read hit rate, to help you monitor the status of the service instances. It also allows you to set alarm rules for these monitoring metrics. After you purchase the Memcache service, CloudMonitor automatically collects data for the previous monitoring metrics.

## Monitoring service {#section_kgs_yt4_ydb .section}

-   Descriptions of monitoring metrics

    |Monitoring metrics|Meaning|Dimension|Unit|Minimum monitoring granularity|
    |:-----------------|:------|:--------|:---|:-----------------------------|
    |Cache used|The amount of cache used|Instance|Bytes|1 minute|
    |Read hit rate|The probability of reading key-values \(KVs\) successfully|Instance|Percentage|1 minute|
    |QPS|Total times of reading KVs per second|Instance|Times|1 minute|
    |Number of records|Total number of KVs in the current measurement period|Instance|KVs|1 minute|
    |Cache inbound bandwidth|Traffic generated by accessing the cache|Instance|Bit/s|1 minute|
    |Cache outbound bandwidth|Traffic generated by reading the cache|Instance|Bit/s|1 minute|
    |Eviction|Number of KVs evicted per second|Instance|KVs per second|1 minute|

    **Note:** 

    -   Monitoring data is saved for up to 31 days.

    -   You can view metric data for up to 14 consecutive days.


-   View monitoring data
    1.  Log on to the [CloudMonitor console](https://cms-intl.console.aliyun.com).
    2.  From the **Cloud Service Monitoring** drop-down list, select **ApsaraDB for Memcache**.
    3.  Click an instance name or click **Monitoring Charts** in the **Actions** column to access the instance monitoring details page and view various metrics.
    4.  Click the **Time Range** quick selection button at the top of the page or use the specific selection function.
    5.  Click the **Zoom In** button in the upper-right corner of the monitoring chart to enlarge the chart.

## Alarm service {#section_ryv_g54_ydb .section}

CloudMonitor provides alarm services for all Memcache monitoring metrics. After setting an alarm rule for an important monitoring metric, you can receive an alarm notification once the monitoring data exceeds the set threshold value, so that you can handle the problem rapidly to avoid malfunction.

-   Parameter description
    -   Monitoring metrics: the monitoring metrics provided by ECS for Redis.
    -   Statistical cycle: the alarm system checks whether your monitoring data has exceeded the alarm threshold based on the cycle. For example, if the statistical cycle of the alarm rule for memory usage is set to one minute, the system checks whether the memory usage has exceeded the threshold value every other minute.
    -   Statistical method: refers to the method used to determine if the data exceeds the threshold. The average value, maximum value, minimum value, and sum value can be set to the statistical method.
        -   Average value: the average value of monitoring data within the statistical cycle. The statistic result is the average of all the monitoring data collected within 15 minutes. An average value over 80% is deemed to exceed the threshold.
        -   Maximum value: the maximum value of monitoring data within the statistical cycle. When the maximum value of the monitoring data collected within the statistical cycle is over 80%, it exceeds the threshold.
        -   Minimum value: the minimum value of monitoring data within the statistical cycle. When the minimum value of the monitoring data collected within the statistical cycle is over 80%, it exceeds the threshold.
        -   Sum value: the sum of monitoring data within the statistical cycle. When the sum of the monitoring data collected within the statistical cycle is over 80%, it exceeds the threshold. This method is required for traffic metrics.
    -   Consecutive times: an alarm is triggered when the value of the monitoring metrics continuously exceeds the threshold value for the set consecutive cycles.

        For example, you have set the alarm to go off when the CPU usage exceeds the threshold value of 80% for three consecutive 5-minute statistical cycles. That is to say, no alarm is triggered when the CPU usage is found to exceed 80% for the first time. No alarm is triggered either when the CPU usage exceeds 80% again in the second detection five minutes later. The alarm is triggered when the CPU usage exceeds 80% again in the third detection. Therefore, from the first time when the actual data exceeds the threshold to the time when the alarm rule is triggered, the minimum time consumed is: the statistical cycle x \(the number of consecutive detections - 1\), which is 5 x \(3 - 1\) = 10 minutes in this case.

-   Set an alarm rule
    1.  Log on to the [CloudMonitor console](https://cms-intl.console.aliyun.com).
    2.  From the **Cloud Service Monitoring** drop-down list, select **ApsaraDB for Memcache**.
    3.  Click an instance name or click **Monitoring Charts** in the **Actions** column to access the instance monitoring details page.
    4.  Click the bell icon in the upper-right corner of the monitoring chart to set an alarm rule for corresponding monitoring metrics of this instance.
-   Set batch alarm rules
    1.  Log on to the [CloudMonitor console](https://cms-intl.console.aliyun.com).
    2.  From the **Cloud Service Monitoring** drop-down list, select **ApsaraDB for Memcache**.
    3.  Select the appropriate instance on the instance list page. Click **Set Alarm Rules** at the bottom of the page to add alarm rules in batches.
