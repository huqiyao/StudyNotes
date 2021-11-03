# 安装

```shell
# /Users/qiyao/Documents/Programs/Arcanist
git clone https://github.com/phacility/libphutil.git
git clone https://github.com/phacility/arcanist.git
```



# 添加环境变量

```shell
# 启动编辑
vim ~/.zshrc

# 内容:
export PATH=$PATH:/Users/qiyao/Documents/Programs/Arcanist/arcanist/bin

# 使其生效
source ~/.zshrc

# 更新arcanist
arc upgrade
```



# 配置 lint engine

```shell
# 任意目录Dir_X，我放在 Programs/Arcanist下
git clone ssh://vcs-user@codes.growingio.com/source/arc-support.git

arc set-config load '["Dir_X/arc-support/src/"]'
```



# 使用

```shell
git add .
git commit -m ''

# arc diff
arc diff master (--only / --preview)
```

⬇️

 Exception 
fopen(/Users/qiyao/Documents/Projects/gio-platform-marketing/junit.xml): failed to open stream: No such file or directory

**解决：**

引入 ```junit.xml``` 文件，以躲过diff过程中的测试

```xml
<?xml version="1.0" encoding="UTF-8"?>
<testsuites name="jest tests" tests="656" failures="0" time="36.605">
  <testsuite name="#addComponentToDashboard" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="7.6" tests="14">
    <testcase classname="dashboardHelper.spec.js" name="#addComponentToDashboard dashboard should has added the normal Component" time="0.022">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#addComponentToDashboard dashboard should be noChange when component is null" time="0.004">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#addComponentToDashboard return null when dashboard is null or underfined" time="0">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#addComponentToSuperContainer Container should has added the normal Component" time="0.002">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#addComponentToSuperContainer Container should be noChange when component is null" time="0">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#addComponentToSuperContainer return null when Container is null or underfined" time="0.001">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#ensureDashboardHasLayout dashboard should noChange when dashboard has layout" time="0.001">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#ensureDashboardHasLayout return dashboard has layout" time="0.004">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#ensureDashboardHasLayout dashboard should be null when it is null " time="0.001">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#upgradeDashboardVersion dashboard must has 2 components" time="0.005">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="#upgradeDashboardVersion dashboard must noChange when it has components" time="0">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="test function getPreviewChart return null when component has null or unKnown type" time="0.001">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="test function getPreviewChart return find Chart when component type is chartId" time="0.018">
    </testcase>
    <testcase classname="dashboardHelper.spec.js" name="test function getPreviewChart return chart  when component type is chart" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="global filter" errors="0" failures="0" skipped="3" timestamp="2020-02-25T02:31:08" time="8.512" tests="118">
    <testcase classname="generateChartParams.spec.js" name="global filter uses the default filter if there is no global filter" time="0.081">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="global filter uses the global filter if there is global filter" time="0.008">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="global time range when there is no global time range if it has the timeRange sets the timeRange" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="global time range when there is no global time range if it has the timeRange returns the today timeRange with one hour interval" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="global time range when there is no global time range if it has the timeRange uses the laset 7 days default time range if it has no timeRange" time="0.004">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="global time range when there is no global time range when there is set the global time range uses the global time range if there is global filter" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="global user segmentation sets the chart&apos;s userTag" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#parseChartSelfTimeRange sets the default timeRange when there is not timeRange" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#parseChartSelfTimeRange does nothing if there is timeRange already" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#listValidInterval return proper interval for line chart for in today, only oneHour" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#listValidInterval return proper interval for line chart from 7 days to below , oneHour or oneDay" time="0.029">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#listValidInterval return proper interval for line chart from 7 days to above , oneHour or oneDay" time="0.018">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#listValidInterval return proper interval for comparison chart for in today, only oneHour" time="0.033">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#listValidInterval return proper interval for comparison chart from yesterday to below , oneHour or oneDay" time="0.009">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#listValidInterval return proper interval for comparison chart from yesterday to above , oneHour or oneDay" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#chartParamsInterval return proper interval for line chart for start in today, only oneHour" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#chartParamsInterval return proper interval for line chart for start in yesterday to 7 days, oneHour or oneDay or oneWeek or oneMonth" time="0.016">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#chartParamsInterval return proper interval for line chart for start after 7 days, oneDay oneWeek oneMonth" time="0.008">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#chartParamsInterval return proper interval for comparison chart for start in today, only oneHour" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#chartParamsInterval return proper interval for comparison chart for start in yesterday, oneHour or oneDay or oneWeek" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#chartParamsInterval return proper interval for comparison chart for start in the days after yesterday, oneDay oneWeek" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#convertChartSeriesNames sets the dimensionNames and metricNames" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#convertChartSeriesNames does not convert the metricNames when the chart does not contain any metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#convertChartSeriesNames does not convert the dimensionNames when the chart does not contain any dimensions" time="0.004">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody bar is not valid when it does not have any metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody bar is valid when it has some metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody vbar is not valid when it does not have any metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody vbar is valid when it has some metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody line is not valid when it does not have any metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody line is valid when it has some metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody bubble is not valid when it does not have any metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody bubble is valid when it does not have x and y" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody bubble is valid when it has x and y" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody bubble is not valid when it does not have any dimensions" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody table is not valid when it does not have any metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody table is not valid when it does not have any dimensions" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody table is valid when it has some metrics and dimensions" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody abar is not valid when it does not have any metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody abar is not valid when it does not have any dimensions" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody abar is valid when it has some metrics and dimensions" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody singleNumber is not valid when it does not have any metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody singleNumber is valid when it has some metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody funnel is not valid when it does not have any metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody funnel is valid when it has some metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody comparison is not valid when it does not have any metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody comparison is valid when it has some metrics" time="0.017">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody tbar is not valid when it does not have any metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody tbar is valid when it has some metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody dimensionLine is not valid when it does not have any metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody dimensionLine is not valid when it does not have any dimensions" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody dimensionLine is valid when it has some metrics and dimensions" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody dimensionVbar is not valid when it does not have any metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody dimensionVbar is not valid when it does not have any dimensions" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#validChartRequestBody dimensionVbar is valid when it has some metrics and dimensions" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#correctChartParams top attribute related removes orders attribute if it is not in metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#correctChartParams top attribute related removes orders attribute if it is not in dimensions" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#correctChartParams top attribute related does nothing" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#correctChartParams does nothing if it is not a bubble chart" time="0">
      <skipped/>
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#correctChartParams removes the null metrics" time="0">
      <skipped/>
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#correctChartParams sets the default metricType if it has not metricType" time="0">
      <skipped/>
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#convertBubbleMetrics returns the indexed metrics when its type is &quot;none&quot;" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#convertBubbleMetrics returns the indexed metrics when its type is &quot;radius&quot;" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#convertBubbleMetrics returns the indexed metrics when its type is &quot;color&quot;" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#convertBubbleMetrics returns the indexed metrics when its type is &quot;all&quot;" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#appendFilter append filter appends filter if the original filter is null" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#appendFilter append filter appends filter if the original filter is {}" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#appendFilter append filter if the original filter is valid combines two single level filters" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#appendFilter append filter if the original filter is valid combines two mutilple levels filters" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#appendFilter append filter if the original filter is valid combines mutiple levels filter to single level filter" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#appendFilter append filter if the original filter is valid combines single level filter to mutiple levels filter" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#appendFilter clear appended filter clears the appended filter if the append filter is null" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#appendFilter clear appended filter clears the appended filter if the append filter is {}" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType any returns orders null" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType bar returns 1 metric" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType bar returns 1 dimension" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType vbar returns 20 metrics" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType vbar returns 0 dimensions" time="0.005">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType line returns 20 metrics" time="0.005">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType line returns 0 dimensions" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType bubble returns 4 metrics" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType bubble returns 1 dimensions" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType table returns 20 metrics" time="0.052">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType table returns 5 dimensions" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType table to table returns 11 metrics" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType table to table returns 6 dimensions" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType abar returns 1 metrics" time="0.004">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType abar returns 1 dimension" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType abar sets the default aggregateType" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType singleNumber returns 1 metrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType singleNumber returns 1 dimension" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType singleNumber sets the aggregateType to sum if there is no dimensions" time="0.012">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType singleNumber sets the aggregateType to avg if there is one dimensions" time="0.022">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType switchs from bubble chart returns filtered the null metrics" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType dimensionLine returns 1 metrics" time="0.004">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType dimensionLine returns 0 dimensions" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType dimensionVbar returns 1 metrics" time="0.018">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartType dimensionVbar returns 0 dimensions" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams params is null do nothing" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams metrics editing #deleteMetric" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams metrics editing #addMetric" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams metrics editing #updateMetric" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams metrics editing #newMetrics" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams dimensions editing #deleteDimension" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams dimensions editing #addDimension" time="0.01">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams dimensions editing #setDimensions" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams setting timeRange sets the default timeRange" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams #subChartType" time="0.013">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams #comment" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams #interval" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams #name" time="0.003">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams #period" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams #period" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams #period" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#setChartParams #chartType" time="0.002">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#cleanUselessOrders when orders is null, do nothing" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#cleanUselessOrders clean orders when invalid" time="0.001">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#cleanUselessOrders do not clean orders when has valid dimension" time="0">
    </testcase>
    <testcase classname="generateChartParams.spec.js" name="#cleanUselessOrders do not clean orders when has valid metric" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="test realtime 自动命名" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="10.06" tests="3">
    <testcase classname="epic.test.js" name="test realtime 自动命名 test 自动设置图表类型" time="0.026">
    </testcase>
    <testcase classname="epic.test.js" name="test realtime 自动命名 test 自动命名" time="0.008">
    </testcase>
    <testcase classname="epic.test.js" name="test realtime 自动命名 test 指标的后置条件" time="0.029">
    </testcase>
  </testsuite>
  <testsuite name="TagsReducer" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:17" time="1.888" tests="17">
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #setSelectedTag returns the default selectedTags attributes" time="0.002">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #setSelectedTag sets the selectedTags if the tag is not selected" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #setSelectedTag removes the the if the tag is selected" time="0.006">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #setSelectedTag does not change the selectedTags attributes if there is no action tagId" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #clearSelectedTags clears selectedTags attributes if it is empty" time="0">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #clearSelectedTags clears selectedTags attributes if it is not empty" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #addTag adds the tag to tags attributes" time="0">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #openTag open the specific tag if the action.id is not undefined" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #openTag close the specific tag if the action.id is undefined" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #removeTag remove the tag" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #removeTag do nothing if tag id does not exist" time="0">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer #removeTag do nothing if tag id is undefined" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer EDITING_TAG returns the default editing attr" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer RESET_TAGS_UI_STATE sets the tags params" time="0">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer TAG_SEARCH sets the search attributes" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer TAG_SEARCH resets the search attributes if the keywords is empty string" time="0.001">
    </testcase>
    <testcase classname="TagsReducer.spec.js" name="TagsReducer TAG_SEARCH resets the search attributes if the keywords is null" time="0">
    </testcase>
  </testsuite>
  <testsuite name="GraphContentPicker unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="12.705" tests="1">
    <testcase classname="index.test.js" name="GraphContentPicker unit test GraphContentPicker snapshot" time="0.176">
    </testcase>
  </testsuite>
  <testsuite name="Testing LargeNumberText" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="12.933" tests="4">
    <testcase classname="index.test.js" name="Testing LargeNumberText Snapshot" time="0.023">
    </testcase>
    <testcase classname="index.test.js" name="Testing LargeNumberText should be able to render component" time="0.016">
    </testcase>
    <testcase classname="index.test.js" name="Testing LargeNumberText render rate" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="Testing LargeNumberText render isFuture" time="0.002">
    </testcase>
  </testsuite>
  <testsuite name="AuthEditor" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="12.995" tests="2">
    <testcase classname="index.test.js" name="AuthEditor renders correctly" time="0.101">
    </testcase>
    <testcase classname="index.test.js" name="AuthEditor renders some user correctly" time="0.023">
    </testcase>
  </testsuite>
  <testsuite name="Ads Attribution Edit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="13.751" tests="1">
    <testcase classname="index.test.js" name="Ads Attribution Edit test should snapshot Editor" time="0.043">
    </testcase>
  </testsuite>
  <testsuite name="test component DimensionFilter" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="14.096" tests="1">
    <testcase classname="index.test.js" name="test component DimensionFilter do snapshot" time="0.036">
    </testcase>
  </testsuite>
  <testsuite name="RealTimeNumber unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:17" time="6.54" tests="1">
    <testcase classname="index.test.js" name="RealTimeNumber unit test RealTimeNumber snapshot" time="0.008">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component TargetUser" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="15.338" tests="1">
    <testcase classname="index.test.js" name="Testing the component TargetUser it will render the 全部访问用户 when value equals uv" time="0.135">
    </testcase>
  </testsuite>
  <testsuite name="Testing component List" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:22" time="2.462" tests="2">
    <testcase classname="index.test.js" name="Testing component List do snapshot" time="0.042">
    </testcase>
    <testcase classname="index.test.js" name="Testing component List will render correctly with isFull equals true" time="0.005">
    </testcase>
  </testsuite>
  <testsuite name="SiderbarMenu" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:19" time="6.13" tests="1">
    <testcase classname="index.test.js" name="SiderbarMenu renders correctly" time="0.146">
    </testcase>
  </testsuite>
  <testsuite name="Component will render correctly" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:23" time="2.856" tests="1">
    <testcase classname="index.test.js" name="Component will render correctly renders correctly" time="0.103">
    </testcase>
  </testsuite>
  <testsuite name="Testing LargeNumberText" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:20" time="5.883" tests="4">
    <testcase classname="index.test.js" name="Testing LargeNumberText Snapshot" time="0.044">
    </testcase>
    <testcase classname="index.test.js" name="Testing LargeNumberText should be able to render component" time="0.034">
    </testcase>
    <testcase classname="index.test.js" name="Testing LargeNumberText render rate" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="Testing LargeNumberText render isFuture" time="0.002">
    </testcase>
  </testsuite>
  <testsuite name="test component RenderSelect" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:22" time="4.514" tests="2">
    <testcase classname="index.test.js" name="test component RenderSelect will render correctly with correct Options" time="0">
    </testcase>
    <testcase classname="index.test.js" name="test component RenderSelect do snapshot" time="0.013">
    </testcase>
  </testsuite>
  <testsuite name="test ads dashboard main thread" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="18.23" tests="9">
    <testcase classname="sagas.test.js" name="test ads dashboard main thread test main" time="0.012">
    </testcase>
    <testcase classname="sagas.test.js" name="test ads dashboard main thread test switchToSomeProductType web" time="0.004">
    </testcase>
    <testcase classname="sagas.test.js" name="test ads dashboard main thread test switchToSomeProductType mobile" time="0.001">
    </testcase>
    <testcase classname="sagas.test.js" name="test ads dashboard main thread test switchToSomeProductType minp" time="0">
    </testcase>
    <testcase classname="sagas.test.js" name="test ads dashboard main thread test initWeb" time="0">
    </testcase>
    <testcase classname="sagas.test.js" name="test ads dashboard main thread test setActivityEffectActivies" time="0.001">
    </testcase>
    <testcase classname="sagas.test.js" name="test ads dashboard main thread test setConversionMetric" time="0">
    </testcase>
    <testcase classname="sagas.test.js" name="test ads dashboard main thread test setMobileConversionMetric" time="0">
    </testcase>
    <testcase classname="sagas.test.js" name="test ads dashboard main thread test watchDataReportConfigsFetched" time="0">
    </testcase>
  </testsuite>
  <testsuite name="HistoricalTrendChart" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:22" time="4.441" tests="2">
    <testcase classname="index.test.js" name="HistoricalTrendChart HistoricalTrendChart snapshot EmptyChart, ErrorChart, LoadingChart, should match a snapshot" time="0.132">
    </testcase>
    <testcase classname="index.test.js" name="HistoricalTrendChart HistoricalTrendChart render HistoricalTrendChart render UserNumber" time="0.019">
    </testcase>
  </testsuite>
  <testsuite name="store/data/dashboards/selectors" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:21" time="5.554" tests="7">
    <testcase classname="dashboardsSelector.spec.js" name="store/data/dashboards/selectors filter - isVisible" time="0.003">
    </testcase>
    <testcase classname="dashboardsSelector.spec.js" name="store/data/dashboards/selectors filter - isSubscribed dashboard with subscribed === true return true" time="0.03">
    </testcase>
    <testcase classname="dashboardsSelector.spec.js" name="store/data/dashboards/selectors filter - isSubscribed dashboard with subscribed === false return false" time="0.001">
    </testcase>
    <testcase classname="dashboardsSelector.spec.js" name="store/data/dashboards/selectors selectors - dashboardsSelector" time="0">
    </testcase>
    <testcase classname="dashboardsSelector.spec.js" name="store/data/dashboards/selectors selectors - visibleDashboardsSelector" time="0.002">
    </testcase>
    <testcase classname="dashboardsSelector.spec.js" name="store/data/dashboards/selectors selectors - subscribedDashboardsSelector" time="0">
    </testcase>
    <testcase classname="dashboardsSelector.spec.js" name="store/data/dashboards/selectors selectors - subscribedVisibleDashboardsSelector" time="0.002">
    </testcase>
  </testsuite>
  <testsuite name="ConfirmModal unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:26" time="2.196" tests="1">
    <testcase classname="index.test.js" name="ConfirmModal unit test snapshot" time="0.033">
    </testcase>
  </testsuite>
  <testsuite name="Ads Attribution List test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:24" time="3.982" tests="1">
    <testcase classname="index.test.js" name="Ads Attribution List test should snapshot List" time="0.272">
    </testcase>
  </testsuite>
  <testsuite name="ChartTooltip unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:27" time="1.478" tests="1">
    <testcase classname="index.test.js" name="ChartTooltip unit test snapshot" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="Testing the 👉CopiableText👈 component " errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:27" time="1.973" tests="2">
    <testcase classname="index.test.js" name="Testing the 👉CopiableText👈 component  will render correctly with props" time="0.546">
    </testcase>
    <testcase classname="index.test.js" name="Testing the 👉CopiableText👈 component  do the CopiableText component snapshot" time="0.037">
    </testcase>
  </testsuite>
  <testsuite name="test component FieldSelect" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:26" time="2.741" tests="2">
    <testcase classname="index.test.js" name="test component FieldSelect it will render correctly" time="0.01">
    </testcase>
    <testcase classname="index.test.js" name="test component FieldSelect do snapshot" time="0.03">
    </testcase>
  </testsuite>
  <testsuite name="Picker unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:26" time="2.674" tests="1">
    <testcase classname="index.test.js" name="Picker unit test Picker snapshot  renders correctly" time="0.019">
    </testcase>
  </testsuite>
  <testsuite name="Testing DatePicker" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:26" time="3.198" tests="2">
    <testcase classname="index.test.js" name="Testing DatePicker should be able to render component" time="0.154">
    </testcase>
    <testcase classname="index.test.js" name="Testing DatePicker should be able to render range component" time="0.802">
    </testcase>
  </testsuite>
  <testsuite name="Testing Greeting" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:29" time="0.576" tests="3">
    <testcase classname="index.test.js" name="Testing Greeting should be able to render component" time="0.051">
    </testcase>
    <testcase classname="index.test.js" name="Testing Greeting should be able to render text currently " time="0.014">
    </testcase>
    <testcase classname="index.test.js" name="Testing Greeting should be able to destroy" time="0.026">
    </testcase>
  </testsuite>
  <testsuite name="SelectCoreTab unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:27" time="2.744" tests="1">
    <testcase classname="index.test.js" name="SelectCoreTab unit test SelectCoreTab snapshot  renders correctly" time="0.041">
    </testcase>
  </testsuite>
  <testsuite name="conditionsGroups" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:29" time="0.52" tests="14">
    <testcase classname="index.test.js" name="conditionsGroups initial state should match a snapshot" time="0.004">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups addGroup addGroup should success" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups toggleGroupOp toggleGroupOp should be OR" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups addConditionToGroup addConditionToGroup should be success" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups handleConditionsUserScopeChange handleConditionsUserScopeChange should be success" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups handleConditionUserActionChange handleConditionUserActionChange should be success" time="0.009">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups handleConditionEventChange handleConditionEventChange should be success" time="0.007">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups handleConditionDimensionChange handleConditionDimensionChange should be success" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups handleConditionOpChange handleConditionEventChange should be success" time="0.007">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups handleConditionEventCountChange handleConditionEventCountChange should be success" time="0.006">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups handleConditionBetweenInputChange handleConditionBetweenInputChange should be success" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups handleConditionDimensionValuesChange handleConditionDimensionValuesChange should be success" time="0.011">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups handleConditionRangeChange handleConditionRangeChange should be success" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="conditionsGroups addConditionToGroup and removeCondition addConditionToGroup and removeCondition should be success" time="0.003">
    </testcase>
  </testsuite>
  <testsuite name="Popfilter" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:28" time="1.978" tests="1">
    <testcase classname="Popfilter.test.tsx" name="Popfilter render with default props" time="0.435">
    </testcase>
  </testsuite>
  <testsuite name="Testing LargeNumberText" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:29" time="1.024" tests="4">
    <testcase classname="index.test.js" name="Testing LargeNumberText Snapshot" time="0.012">
    </testcase>
    <testcase classname="index.test.js" name="Testing LargeNumberText should be able to render component" time="0.03">
    </testcase>
    <testcase classname="index.test.js" name="Testing LargeNumberText render rate" time="0.004">
    </testcase>
    <testcase classname="index.test.js" name="Testing LargeNumberText render isFuture" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="Testing Attribution" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:24" time="5.597" tests="2">
    <testcase classname="index.test.js" name="Testing Attribution should be able to render component 👉ExactDocking 👈 when isExactDocking is true" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="Testing Attribution would not be able to render component 👉ExactDocking 👈 when isExactDocking is false" time="0.002">
    </testcase>
  </testsuite>
  <testsuite name="Tab unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:29" time="0.522" tests="1">
    <testcase classname="index.test.js" name="Tab unit test Tab snapshot" time="0.013">
    </testcase>
  </testsuite>
  <testsuite name="DeleteConfirmModal unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:29" time="1.749" tests="1">
    <testcase classname="index.test.js" name="DeleteConfirmModal unit test DeleteConfirmModal snapshot" time="0.01">
    </testcase>
  </testsuite>
  <testsuite name="DataOverViewGrid unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:29" time="1.19" tests="1">
    <testcase classname="index.test.js" name="DataOverViewGrid unit test snapshot" time="0.009">
    </testcase>
  </testsuite>
  <testsuite name="Testing component ProductPicker" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:30" time="1.177" tests="4">
    <testcase classname="index.test.js" name="Testing component ProductPicker will render correctly with onInit be called" time="0.092">
    </testcase>
    <testcase classname="index.test.js" name="Testing component ProductPicker will render correctly with correct counts Option component" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="Testing component ProductPicker do snapshot" time="0.008">
    </testcase>
    <testcase classname="index.test.js" name="test function mapToWebProduct will return web product" time="0">
    </testcase>
  </testsuite>
  <testsuite name="#setSelectedTag" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:30" time="0.946" tests="6">
    <testcase classname="tagsActions.spec.js" name="#setSelectedTag returns the setSelectedTag action" time="0.004">
    </testcase>
    <testcase classname="tagsActions.spec.js" name="#clearSelectedTags returns the clearSelectedTags action" time="0.001">
    </testcase>
    <testcase classname="tagsActions.spec.js" name="#addTag returns the mergeTags action" time="0.001">
    </testcase>
    <testcase classname="tagsActions.spec.js" name="#removeTag returns the removeTag action" time="0.001">
    </testcase>
    <testcase classname="tagsActions.spec.js" name="#resetTagsUIState returns the resetTagsUIState action" time="0">
    </testcase>
    <testcase classname="tagsActions.spec.js" name="#search tags returns search tags action" time="0">
    </testcase>
  </testsuite>
  <testsuite name="BetweenInputs" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:29" time="1.829" tests="4">
    <testcase classname="index.test.js" name="BetweenInputs BetweenInputs snapshot should match a snapshot" time="0.046">
    </testcase>
    <testcase classname="index.test.js" name="BetweenInputs BetweenInputs funciton focus is true" time="0.012">
    </testcase>
    <testcase classname="index.test.js" name="BetweenInputs BetweenInputs funciton has two inputs" time="0.01">
    </testcase>
    <testcase classname="index.test.js" name="BetweenInputs BetweenInputs funciton setState focus &amp; blur" time="0.019">
    </testcase>
  </testsuite>
  <testsuite name="test component ChannelSelector" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:30" time="1.54" tests="1">
    <testcase classname="index.test.js" name="test component ChannelSelector will render correctly with props" time="0.014">
    </testcase>
  </testsuite>
  <testsuite name="test component FormPanel" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:30" time="0.795" tests="1">
    <testcase classname="index.test.js" name="test component FormPanel do snapshot" time="0.01">
    </testcase>
  </testsuite>
  <testsuite name="projectsAction" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:30" time="0.961" tests="9">
    <testcase classname="projectsActions.spec.js" name="projectsAction #cacheProjectData returns a ccheProjectAction" time="0.001">
    </testcase>
    <testcase classname="projectsActions.spec.js" name="projectsAction #addApp returns an addAppAction" time="0.001">
    </testcase>
    <testcase classname="projectsActions.spec.js" name="projectsAction #updateProducts return an updateProductsAction" time="0.001">
    </testcase>
    <testcase classname="projectsActions.spec.js" name="projectsAction #removeProduct returns a removeProductAction" time="0.001">
    </testcase>
    <testcase classname="projectsActions.spec.js" name="projectsAction #addProject return an addProject" time="0">
    </testcase>
    <testcase classname="projectsActions.spec.js" name="projectsAction #updateProjectList returns an updateProjectListAction" time="0.001">
    </testcase>
    <testcase classname="projectsActions.spec.js" name="projectsAction #toggleProjectStatus #returns an toggleProjectStatusAction" time="0.001">
    </testcase>
    <testcase classname="projectsActions.spec.js" name="projectsAction #setEdittingProduct returns the setEdittingProduct action" time="0">
    </testcase>
    <testcase classname="projectsActions.spec.js" name="projectsAction #updateEdittingProduct returns the actions.updateEdittingProduct" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="test component CampaignSelector" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:30" time="1.282" tests="2">
    <testcase classname="index.test.js" name="test component CampaignSelector will render correctly with 40 campaigns" time="0.014">
    </testcase>
    <testcase classname="index.test.js" name="test component CampaignSelector do snapshot" time="0.01">
    </testcase>
  </testsuite>
  <testsuite name="RenderDateRange unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:31" time="0.606" tests="1">
    <testcase classname="index.test.js" name="RenderDateRange unit test RenderDateRange snapshot" time="0.013">
    </testcase>
  </testsuite>
  <testsuite name="ConfirmPopover" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:30" time="1.268" tests="3">
    <testcase classname="index.test.js" name="ConfirmPopover ConfirmPannal snapshot should match a snapshot" time="0.383">
    </testcase>
    <testcase classname="index.test.js" name="ConfirmPopover ConfirmPannal props should render props" time="0.159">
    </testcase>
    <testcase classname="index.test.js" name="ConfirmPopover ConfirmPopover html should render 3 div" time="0.144">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component 👉DomainUpgrade👈" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:32" time="0.746" tests="2">
    <testcase classname="index.test.js" name="Testing the component 👉DomainUpgrade👈 it will render correctly with props" time="0.027">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component 👉DomainUpgrade👈 do the DomainUpgrade component snapshot" time="0.012">
    </testcase>
  </testsuite>
  <testsuite name="Testing Card" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:31" time="1.257" tests="1">
    <testcase classname="index.test.js" name="Testing Card Snapshot" time="0.009">
    </testcase>
  </testsuite>
  <testsuite name="usersAction" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:32" time="0.936" tests="8">
    <testcase classname="usersActions.spec.js" name="usersAction #editUser returns an usersAction" time="0.003">
    </testcase>
    <testcase classname="usersActions.spec.js" name="usersAction #editPassword returns an editPasswordAction" time="0.001">
    </testcase>
    <testcase classname="usersActions.spec.js" name="usersAction #inviteUser returns an inviteUserAction" time="0">
    </testcase>
    <testcase classname="usersActions.spec.js" name="usersAction #showUsersToInviteDetail returns a showUsersToInviteDetailAction" time="0.001">
    </testcase>
    <testcase classname="usersActions.spec.js" name="usersAction #updateUserStatus returns an updateUserStatusActioin" time="0">
    </testcase>
    <testcase classname="usersActions.spec.js" name="usersAction #editUsersToInviteDetail returns an editUsersToInviteDetail" time="0">
    </testcase>
    <testcase classname="usersActions.spec.js" name="usersAction #removeInvitation returns an removeInvitationAction" time="0.001">
    </testcase>
    <testcase classname="usersActions.spec.js" name="usersAction #updateInvitations returns an updateInvitationAction" time="0">
    </testcase>
  </testsuite>
  <testsuite name="circleActions" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:32" time="0.98" tests="11">
    <testcase classname="circleAction.spec.js" name="circleActions #setBrowseMode" time="0.005">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #setCircleUrl" time="0.001">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #setCircleable" time="0.001">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #setIframeUrl" time="0.001">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #setCirclingPage" time="0.001">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #setLimitPanel" time="0.001">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #toggleHighlight" time="0.001">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #pageTagSaved" time="0.001">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #switchBrowseMode" time="0.002">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #pageTagSaved" time="0.023">
    </testcase>
    <testcase classname="circleAction.spec.js" name="circleActions #setLoadingState" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="pageEventHelper" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:32" time="0.963" tests="3">
    <testcase classname="pageEventHelper.test.js" name="pageEventHelper filter protocol" time="0.001">
    </testcase>
    <testcase classname="pageEventHelper.test.js" name="pageEventHelper normalize url" time="0.001">
    </testcase>
    <testcase classname="pageEventHelper.test.js" name="pageEventHelper add http protocol" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="App TencentLink Preview test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:32" time="0.882" tests="1">
    <testcase classname="index.test.js" name="App TencentLink Preview test should snapshot" time="0.06">
    </testcase>
  </testsuite>
  <testsuite name="Ads AttributionAnalysis MultiModel test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:08" time="24.986" tests="2">
    <testcase classname="index.test.js" name="Ads AttributionAnalysis MultiModel test should snapshot table with single data" time="0.328">
    </testcase>
    <testcase classname="index.test.js" name="Ads AttributionAnalysis MultiModel test should snapshot table with compare data" time="0.078">
    </testcase>
  </testsuite>
  <testsuite name="Component will render correctly" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:32" time="1.254" tests="1">
    <testcase classname="index.test.js" name="Component will render correctly renders correctly" time="0.133">
    </testcase>
  </testsuite>
  <testsuite name="Test the component ConversionWindow" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:32" time="0.812" tests="1">
    <testcase classname="index.test.js" name="Test the component ConversionWindow will render 30 Options component cuz our max-conversionWindow is 30days" time="0.007">
    </testcase>
  </testsuite>
  <testsuite name="undefined" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:32" time="1.02" tests="1">
    <testcase classname="index.test.js" name=" EditModal snapshot" time="0.006">
    </testcase>
  </testsuite>
  <testsuite name="CustomColumns" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:32" time="1.111" tests="1">
    <testcase classname="CustomColumns.test.tsx" name="CustomColumns renders with default vaule" time="0.447">
    </testcase>
  </testsuite>
  <testsuite name="Product snapshot" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:33" time="0.702" tests="4">
    <testcase classname="index.test.js" name="Product snapshot should snapshoot" time="0.081">
    </testcase>
    <testcase classname="index.test.js" name="Product Status Tag test should AppLinks &amp; TencentLinks actived" time="0.035">
    </testcase>
    <testcase classname="index.test.js" name="Product Status Tag test shouldn`t AppLinks and TencentLinks actived" time="0.022">
    </testcase>
    <testcase classname="index.test.js" name="Product Status Tag test should ulink actived" time="0.01">
    </testcase>
  </testsuite>
  <testsuite name="SubscriptionBox" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:33" time="0.797" tests="4">
    <testcase classname="SubscriptionBox.test.tsx" name="SubscriptionBox render with subscribed" time="0.006">
    </testcase>
    <testcase classname="SubscriptionBox.test.tsx" name="SubscriptionBox render with unsubscribed" time="0.003">
    </testcase>
    <testcase classname="SubscriptionBox.test.tsx" name="SubscriptionBox render with subscribed and confirmed" time="0.264">
    </testcase>
    <testcase classname="SubscriptionBox.test.tsx" name="SubscriptionBox can subscribe and unsubscribe" time="0.042">
    </testcase>
  </testsuite>
  <testsuite name="test component FieldInput" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:33" time="1.027" tests="1">
    <testcase classname="index.test.js" name="test component FieldInput will render correctly with props" time="0.009">
    </testcase>
  </testsuite>
  <testsuite name="ContentWrapper" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:33" time="0.6" tests="4">
    <testcase classname="index.test.js" name="ContentWrapper ContentWrapper snapshot should match a snapshot" time="0.095">
    </testcase>
    <testcase classname="index.test.js" name="ContentWrapper ContentWrapper render header render" time="0.01">
    </testcase>
    <testcase classname="index.test.js" name="ContentWrapper ContentWrapper render title render" time="0.005">
    </testcase>
    <testcase classname="index.test.js" name="ContentWrapper ContentWrapper render headerRightComponent render" time="0.008">
    </testcase>
  </testsuite>
  <testsuite name="App Detail Preview test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:33" time="0.716" tests="1">
    <testcase classname="index.test.js" name="App Detail Preview test should snapshot" time="0.088">
    </testcase>
  </testsuite>
  <testsuite name="Test the component Trigger" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:33" time="0.995" tests="2">
    <testcase classname="index.test.js" name="Test the component Trigger will render PlaceHolder component when value is empty string" time="0.11">
    </testcase>
    <testcase classname="index.test.js" name="Test the component Trigger just do the snapshot" time="0.054">
    </testcase>
  </testsuite>
  <testsuite name="App UniversalLink Preview test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:33" time="0.676" tests="1">
    <testcase classname="index.test.js" name="App UniversalLink Preview test should snapshot" time="0.036">
    </testcase>
  </testsuite>
  <testsuite name="Testing IfTooltip" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:33" time="0.93" tests="3">
    <testcase classname="index.test.js" name="Testing IfTooltip Snapshot: render a disabled children with tooltip." time="0.009">
    </testcase>
    <testcase classname="index.test.js" name="Testing IfTooltip Snapshot: render a children without tooltip." time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="Testing IfTooltip Hover test" time="0.055">
    </testcase>
  </testsuite>
  <testsuite name="Footer unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:33" time="0.849" tests="1">
    <testcase classname="index.test.js" name="Footer unit test Footer snapshot" time="0.007">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component 👉EmptyTrackerList👈" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:34" time="0.78" tests="5">
    <testcase classname="index.test.js" name="Testing the component 👉EmptyTrackerList👈 will render correctly with deeplink props" time="0.065">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component 👉EmptyTrackerList👈 will render correctly with onelink props" time="0.008">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component 👉EmptyTrackerList👈 will render correctly with minplink props" time="0.009">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component 👉EmptyTrackerList👈 will render correctly with no linkType props" time="0.005">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component 👉EmptyTrackerList👈 do the component EmptyTrackerList snapshot" time="0.009">
    </testcase>
  </testsuite>
  <testsuite name="URLInput unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:34" time="0.986" tests="1">
    <testcase classname="index.test.js" name="URLInput unit test URLInput snapshot" time="0.02">
    </testcase>
  </testsuite>
  <testsuite name="test component ProductSelect" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:34" time="0.648" tests="1">
    <testcase classname="index.test.js" name="test component ProductSelect will render correctly" time="0.012">
    </testcase>
  </testsuite>
  <testsuite name="createChart" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:34" time="0.602" tests="5">
    <testcase classname="index.test.ts" name="createChart getMeasureQuery should return query separated by unit separator if given a measure" time="0.003">
    </testcase>
    <testcase classname="index.test.ts" name="createChart getMeasureQuery should return query separated by record separator if given more than 1 measure" time="0.001">
    </testcase>
    <testcase classname="index.test.ts" name="createChart getQueryFromObejct should ignore invalid value like empty string, null" time="0">
    </testcase>
    <testcase classname="index.test.ts" name="createChart getMeasureFromQuery should return measure object from query string" time="0.009">
    </testcase>
    <testcase classname="index.test.ts" name="createChart getMeasureFromQuery should return empty array if given an empty string" time="0">
    </testcase>
  </testsuite>
  <testsuite name="LargeNumberProvider test unit" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:34" time="0.678" tests="3">
    <testcase classname="index.test.js" name="LargeNumberProvider test unit LargeNumberProvider snapshot" time="0.021">
    </testcase>
    <testcase classname="index.test.js" name="LargeNumberProvider test unit LargeNumberProvider render" time="0.005">
    </testcase>
    <testcase classname="index.test.js" name="LargeNumberProvider test unit LargeNumberProvider render state" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="Testing TimeUnit" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:34" time="0.596" tests="11">
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit pass start time that last 7 days before and get time range" time="0.009">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit pass start time that last 7 days before and pass end time that 7 days after, then get time range" time="0.002">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit pass start time that last 7 days before and pass end time that 3 days before, then get time range" time="0.002">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit The range time is future" time="0">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit The range of the time is in a day" time="0.002">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit Get start by range of time" time="0">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit Get end by range of time" time="0.001">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit Get status" time="0.001">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit formate time" time="0.003">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit More than 30 days" time="0.002">
    </testcase>
    <testcase classname="timeUtil.test.js" name="Testing TimeUnit Get time range" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="undefined" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:34" time="0.786" tests="1">
    <testcase classname="index.test.js" name=" ExactDocking snapshot" time="0.009">
    </testcase>
  </testsuite>
  <testsuite name="#strip" errors="0" failures="0" skipped="1" timestamp="2020-02-25T02:31:35" time="0.641" tests="36">
    <testcase classname="GrUtils.spec.js" name="#strip strips the html tag" time="0.008">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#getCnDayOfWeek returns an empty string if given undefined" time="0">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#getCnDayOfWeek returns an empty string if given 0" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#getCnDayOfWeek returns the day of week in chinese if given a date" time="0">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#getCnDayOfWeek returns the day of week in chinese if given a timestamp" time="0.008">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#getCnDayOfWeek returns the a single number in chinese if given a false as the second param " time="0">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="generateKeyFromObject returns the string with object keys separated by -" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="generateKeyFromObject returns the string coresponding the sequence of sorted object keys" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="generateKeyFromObject returns empty string if the given parameter was not an Object" time="0.004">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="normalizeWeekTimeRange returns the startTime in fisrt Monday and endTime in last Sunday if the range was more than 1 week" time="0.004">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="normalizeWeekTimeRange returns the current week if the range was in 1 week" time="0.002">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="normalizeWeekTimeRange returns the last week if Sunday of endTime was in future" time="0">
      <skipped/>
    </testcase>
    <testcase classname="GrUtils.spec.js" name="getPercent returns the percent in string if given two valid parameters" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="getPercent returns the percent with two decimal places" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="getPercent returns the percent with given number of decimal places" time="0.003">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="getPercent returns 0% if given invalid parameters" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="getPercent returns the percent without % sign if given a false value as parameter for sign" time="0.002">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="getPercent returns the percent if just given an decimal" time="0">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="autoCompleteUrl completes the url if the url does not start with http or https" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="autoCompleteUrl returns the url if the url starts with http" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="autoCompleteUrl returns the url if the url starts with https" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="hasTargetRoute return false when no candidates" time="0.002">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="hasTargetRoute return false when no target" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="hasTargetRoute returns false when no candidate match" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="hasTargetRoute returns true when has candidate" time="0.003">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="validate email empty str should be invalid email" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="validate email no @ should be invalid email" time="0">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="validate email no user info should be invalid email" time="0.002">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="validate email no domain should be invalid email" time="0">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="validate email xyz@gio.com should be a valid email" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#compareVersion Do not compare when any ver is empty" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#compareVersion 0.9.40 should greater than 0.9.39" time="0.002">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#compareVersion 0.9.40_sjflagi should greater than 0.9.39_fjlsaie" time="0.002">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#compareVersion 0.9.39_sjflagi should less than 0.9.40_fjlsaie" time="0">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#compareVersion 0.9.40_sjflagi should equal than 0.9.40_fjlsaie" time="0.001">
    </testcase>
    <testcase classname="GrUtils.spec.js" name="#compareVersion 1.0_fskefgt should greater than 0.9.40_fjlsaie" time="0">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component SearchTable" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:35" time="0.658" tests="1">
    <testcase classname="index.test.js" name="Testing the component SearchTable do snapshot" time="0.015">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component NoLinkPlaceholder" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:35" time="0.562" tests="2">
    <testcase classname="index.test.js" name="Testing the component NoLinkPlaceholder will render correctly" time="0.009">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component NoLinkPlaceholder do snapshot" time="0.072">
    </testcase>
  </testsuite>
  <testsuite name="Test install sdk actions" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:35" time="1.007" tests="8">
    <testcase classname="installSdkActions.spec.js" name="Test install sdk actions return nextStep action" time="0.002">
    </testcase>
    <testcase classname="installSdkActions.spec.js" name="Test install sdk actions return previousStep action" time="0.001">
    </testcase>
    <testcase classname="installSdkActions.spec.js" name="Test install sdk actions return toggleSaveProductFormLoading action" time="0">
    </testcase>
    <testcase classname="installSdkActions.spec.js" name="Test install sdk actions return updateTempProductForm action" time="0.001">
    </testcase>
    <testcase classname="installSdkActions.spec.js" name="Test install sdk actions return resetState action" time="0.001">
    </testcase>
    <testcase classname="installSdkActions.spec.js" name="Test install sdk actions return enableFormValidation" time="0">
    </testcase>
    <testcase classname="installSdkActions.spec.js" name="Test install sdk actions return updateState action" time="0.001">
    </testcase>
    <testcase classname="installSdkActions.spec.js" name="invitingEngineer actions #updateInvitingEngineer returns an invitingEngineer action" time="0.006">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component Gap" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:35" time="0.841" tests="14">
    <testcase classname="index.test.js" name="Testing the component Gap Gap will render correctly with mock props" time="0.023">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component Gap do Gap component snapshot" time="0.005">
    </testcase>
    <testcase classname="index.test.js" name="Testing the function getProductTypeByPlatform will return web when platform equals js" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="Testing the function getProductTypeByPlatform will return mobile when platform equals ios/android" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="Testing the function getProductTypeByPlatform will return minp when platform equals minp" time="0">
    </testcase>
    <testcase classname="index.test.js" name="Testing the function getProductTypeByPlatform will return minp when platform equals minp" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="Testing the function dayToSecond will return 86400 when input 1" time="0">
    </testcase>
    <testcase classname="index.test.js" name="Testing the function secondToDay will return 1 when input 86400" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="Testing the function processChartDataByTop will return the correct chartdata by top" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component Star will return null when props.disabled equals true" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component Star will return null when props.disabled equals false" time="0.005">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component Star do the component Star snapshot" time="0.004">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component NoPermissionNotice will render correctly with text" time="0.015">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component NoPermissionNotice do snapshot" time="0.005">
    </testcase>
  </testsuite>
  <testsuite name="test component RenderSelect" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:35" time="0.617" tests="2">
    <testcase classname="index.test.js" name="test component RenderSelect will render correctly with correct Options" time="0.009">
    </testcase>
    <testcase classname="index.test.js" name="test component RenderSelect do snapshot" time="0.008">
    </testcase>
  </testsuite>
  <testsuite name="Testing HowTo component" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.529" tests="3">
    <testcase classname="index.test.js" name="Testing HowTo component will render correctly with negative recordLength" time="0.045">
    </testcase>
    <testcase classname="index.test.js" name="Testing HowTo component props.showPanel will be called when button is clicked" time="0.043">
    </testcase>
    <testcase classname="index.test.js" name="Testing HowTo component do snapshot" time="0.007">
    </testcase>
  </testsuite>
  <testsuite name="undefined" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.513" tests="1">
    <testcase classname="shortcutRange.spec.js" name=" queryRangesHandle getAllRangeValues testing" time="0.018">
    </testcase>
  </testsuite>
  <testsuite name="SelectList" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.643" tests="5">
    <testcase classname="index.test.js" name="SelectList renderItem should render one option when given one string option" time="0.04">
    </testcase>
    <testcase classname="index.test.js" name="SelectList renderItem should render two options when given two object options" time="0.004">
    </testcase>
    <testcase classname="index.test.js" name="SelectList renderItem should render options with selected one when given correspoding value" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="SelectList labelRenderer should render label by labelRenderer if given labelRenderer prop" time="0.014">
    </testcase>
    <testcase classname="index.test.js" name="SelectList labelRenderer should pass isGroup to labelRender if option&apos;s type was groupName" time="0.017">
    </testcase>
  </testsuite>
  <testsuite name="ChartWrapper" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.42" tests="3">
    <testcase classname="index.test.js" name="ChartWrapper ChartWrapper snapshot should match a snapshot" time="0.052">
    </testcase>
    <testcase classname="index.test.js" name="ChartWrapper ChartWrapper render header render" time="0.01">
    </testcase>
    <testcase classname="index.test.js" name="ChartWrapper ChartWrapper render title render" time="0.006">
    </testcase>
  </testsuite>
  <testsuite name="App Links Preview test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.672" tests="1">
    <testcase classname="index.test.js" name="App Links Preview test should snapshot" time="0.049">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component Announcement" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.636" tests="1">
    <testcase classname="index.test.js" name="Testing the component Announcement do snapshot" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="#Test CircleSelector" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.525" tests="4">
    <testcase classname="CircleSelector.spec.js" name="#Test CircleSelector filter tags by pageTag" time="0.005">
    </testcase>
    <testcase classname="CircleSelector.spec.js" name="#Test CircleSelector sort page tags by path" time="0.001">
    </testcase>
    <testcase classname="CircleSelector.spec.js" name="#Test CircleSelector calculatePageTags" time="0">
    </testcase>
    <testcase classname="CircleSelector.spec.js" name="#Test CircleSelector calculate Elem tags" time="0.012">
    </testcase>
  </testsuite>
  <testsuite name="#findUser" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.427" tests="16">
    <testcase classname="dataConvertor.spec.js" name="#findUser returns the correct user." time="0.007">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#findUser returns the user with name &apos;System&apos; if there is no user." time="0.001">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#readableFilter return the readableFilter format for 1 level logic" time="0.001">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#readableFilter return the readableFilter format for 2 level logic" time="0">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#readableFilter returns the nested readable filters" time="0">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#serverFormatMetricExpression, #clientFormatMetricExpression: convert full expression #clientFormatMetricExpression, convert full expression" time="0.002">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#serverFormatMetricExpression, #clientFormatMetricExpression: convert full expression #serverFormatMetricExpression, convert full expression" time="0.002">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#serverFormatMetricExpression, #clientFormatMetricExpression: convert part expression #serverFormatMetricExpression, covert part expression" time="0.001">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#serverFormatMetricExpression, #clientFormatMetricExpression: convert part expression #clientFormatMetricExpression, covert part expression" time="0.001">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#getChartFilterKeys when the filter is empty returns the empty key when filter is empty" time="0">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#getChartFilterKeys when the filter is empty returns the empty key when filter exprs is empty" time="0.002">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#getChartFilterKeys when the filter is single level filter returns the keys when the filter is single level" time="0.001">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#getChartFilterKeys when the filter is single level filter returns the keys when the filter is single level filter but in exprs" time="0">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#getChartFilterKeys when the filter is mutiple levels filter when the filter is combined with two single level filter returns the keys" time="0">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#getChartFilterKeys when the filter is mutiple levels filter when the filter is combined with two mutiple levels filters returns the keys" time="0.001">
    </testcase>
    <testcase classname="dataConvertor.spec.js" name="#getChartFilterKeys when the filter is mutiple levels filter when the filter is combined with one single filter and one mutiple levels filter returns the keys" time="0">
    </testcase>
  </testsuite>
  <testsuite name="InputInfo unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.54" tests="1">
    <testcase classname="index.test.js" name="InputInfo unit test InputInfo snapshot" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component 👉Delete👈" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.436" tests="1">
    <testcase classname="index.test.js" name="Testing the component 👉Delete👈 do the Delete component snapshot" time="0.045">
    </testcase>
  </testsuite>
  <testsuite name="testing the component widthField" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.498" tests="2">
    <testcase classname="index.test.js" name="testing the component widthField render correctly" time="0.019">
    </testcase>
    <testcase classname="index.test.js" name="testing the function getDisplayName will return the correct component-name" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="BroadDocking test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.301" tests="1">
    <testcase classname="index.test.js" name="BroadDocking test should snapshot" time="0.012">
    </testcase>
  </testsuite>
  <testsuite name="converChartData with empty data" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:36" time="0.392" tests="13">
    <testcase classname="index.test.js" name="converChartData with empty data chartType is line, and it should match chart source" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with one metric and dims is time chartType is line, and it should match chart source" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with multi metrics and dims is time chartType is line, and it should match chart source" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with one metric and dims are time and rt chartType is line, and it should match chart source" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with one metric and dim is time chartType is comparison, and it should match chart source" time="0.005">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with one targetUser and no dimension chartType is vbar, and it should match chart source" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with one targetUser, no dimension subcharttype is total chartType is vbar, and it should match chart source" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with one dimension or two segmentations chartType is vbar, and it should match chart source" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with one dimension or two segmentations and subcharttye is total chartType is vbar, and it should match chart source" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with one dimension or two segmentations, charttype is bar chartType is bar, and it should match chart source" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="converChartData charttype is table chartType is table, and it should match chart source" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="converChartData with chartype is singleNumber chartType is singleNumber, and it should match chart source" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="converChartData charttype is bubble chartType is bubble, and it should match chart source" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component ButtonGroup" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.444" tests="3">
    <testcase classname="index.test.js" name="Testing the component ButtonGroup will render OK-Button when isAnalysisButtonClicked is false" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component ButtonGroup will render OK-Button when isAnalysisButtonClicked is true &amp;&amp; isQueryConditionChange is true" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component ButtonGroup will render Cancel-Text only when isAnalysisButtonClicked is true &amp;&amp; isQueryConditionChange is true" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="test component SearchFilter" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.453" tests="1">
    <testcase classname="index.test.js" name="test component SearchFilter will render correctly with props" time="0.011">
    </testcase>
  </testsuite>
  <testsuite name="ExceptionChart" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.39" tests="4">
    <testcase classname="index.test.js" name="ExceptionChart ExceptionChart snapshot EmptyChart, ErrorChart, LoadingChart, should match a snapshot" time="0.05">
    </testcase>
    <testcase classname="index.test.js" name="ExceptionChart ExceptionChart render EmptyChart render" time="0.009">
    </testcase>
    <testcase classname="index.test.js" name="ExceptionChart ExceptionChart render ErrorChart render" time="0.004">
    </testcase>
    <testcase classname="index.test.js" name="ExceptionChart ExceptionChart render LoadingChart render" time="0.009">
    </testcase>
  </testsuite>
  <testsuite name="Input" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.342" tests="3">
    <testcase classname="index.test.js" name="Input renders correctly" time="0.029">
    </testcase>
    <testcase classname="index.test.js" name="Input renders with props correctly" time="0.008">
    </testcase>
    <testcase classname="index.test.js" name="Input renders with suffix correctly" time="0.005">
    </testcase>
  </testsuite>
  <testsuite name="Testing Table" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.418" tests="1">
    <testcase classname="index.test.js" name="Testing Table should be able to render component" time="0.047">
    </testcase>
  </testsuite>
  <testsuite name="SelectGroup unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.496" tests="1">
    <testcase classname="index.test.js" name="SelectGroup unit test renders correctly" time="0.011">
    </testcase>
  </testsuite>
  <testsuite name="searchFilter#search" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.385" tests="14">
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is string returns the exactly matched item" time="0.004">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is string returns the mostly matched item" time="0.001">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is string returns all item if removed keywords" time="0">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is string returns all of the item searched by null" time="0.001">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is string returns all of the item if it does not specify column" time="0">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is string returns the item searched by Chinese" time="0.002">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is string returns the item searched by pinyin" time="0.002">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is array keywords in name" time="0.004">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is array keywords in name with many items" time="0.001">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is array returns all item if removed keywords" time="0.001">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is array returns all of the item searched by null" time="0.001">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is array keywords in creatorName" time="0.001">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is array keywords with 汉字 in creatorName" time="0">
    </testcase>
    <testcase classname="searchFilter.spec.js" name="searchFilter#search when column is array keywords with 汉字 in creatorName bu search with pinyin" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="test component DownloadExportPanel" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.409" tests="1">
    <testcase classname="index.test.js" name="test component DownloadExportPanel do snapshot" time="0.015">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component NoProduct" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.317" tests="2">
    <testcase classname="index.test.js" name="Testing the component NoProduct will render correctly with props" time="0.042">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component NoProduct do component NoProduct snapshot" time="0.009">
    </testcase>
  </testsuite>
  <testsuite name="message" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.377" tests="1">
    <testcase classname="index.test.js" name="message should display correctly" time="0.034">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component Tip" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.363" tests="1">
    <testcase classname="index.test.js" name="Testing the component Tip do Tip component snapshot" time="0.03">
    </testcase>
  </testsuite>
  <testsuite name="TableActions" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.431" tests="2">
    <testcase classname="TableActions.test.tsx" name="TableActions render actions" time="0.026">
    </testcase>
    <testcase classname="TableActions.test.tsx" name="TableActions can clear selected" time="0.006">
    </testcase>
  </testsuite>
  <testsuite name="webCircleReducers" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:37" time="0.366" tests="15">
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #setBrowseMode set browse mode with &quot;circle&quot;" time="0.006">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #setBrowseMode set browse mode with &quot;heatMap&quot;" time="0.001">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #setBrowseMode set heatMap dashboard to visible when set mode to heatMap" time="0.014">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #setBrowseMode resets the isLoading state when switch to the browseMode which is not heatMap" time="0.001">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #updateURL update url" time="0.001">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #updateIframeUrl update iframe url" time="0.001">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #updateTitle update title" time="0.001">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #updateTitle update title and check the initialPageTitle" time="0.001">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #setCircleAble set circleable" time="0">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #setPageTag set page tag" time="0.001">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #circlingPage circling pgae with false" time="0.001">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #switchBrowseMode switch browse mode with true" time="0">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #toggleHighlighting toggleHighlighting with true" time="0.001">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #pageTagSaved page tag saved" time="0">
    </testcase>
    <testcase classname="circleReducers.spec.js" name="webCircleReducers #setLoadingState sets the loading state" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="test component FieldInput" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.355" tests="2">
    <testcase classname="index.test.js" name="test component FieldInput it will render correctly without error" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="test component FieldInput it will render correctly with error" time="0.002">
    </testcase>
  </testsuite>
  <testsuite name="Ads Permission Model&apos;s unit test: reducer" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.356" tests="1">
    <testcase classname="reducers.test.js" name="Ads Permission Model&apos;s unit test: reducer permissionReducer init" time="0.005">
    </testcase>
  </testsuite>
  <testsuite name="#generateId" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.356" tests="10">
    <testcase classname="chartDataCacheFormatter.spec.js" name="#generateId handles the empty filter" time="0.006">
    </testcase>
    <testcase classname="chartDataCacheFormatter.spec.js" name="#generateId generates the same id with same key attributes" time="0.006">
    </testcase>
    <testcase classname="chartDataCacheFormatter.spec.js" name="#generateId generates the different ids with different key attribtues" time="0.003">
    </testcase>
    <testcase classname="chartDataCacheFormatter.spec.js" name="#generateId generates the different ids with different ids" time="0.002">
    </testcase>
    <testcase classname="chartDataCacheFormatter.spec.js" name="#generateId generates the different ids with different chartTypes" time="0.006">
    </testcase>
    <testcase classname="chartDataCacheFormatter.spec.js" name="#generateId generates the different ids with different intervals" time="0.002">
    </testcase>
    <testcase classname="chartDataCacheFormatter.spec.js" name="#generateId returns the matched data with timeRange and different order of filter" time="0.002">
    </testcase>
    <testcase classname="chartDataCacheFormatter.spec.js" name="#compareRequestChartParams returns true when the request params is equal" time="0.001">
    </testcase>
    <testcase classname="chartDataCacheFormatter.spec.js" name="#compareRequestChartParams returns true when the request params is equal but the unnessary request params is not same" time="0.001">
    </testcase>
    <testcase classname="chartDataCacheFormatter.spec.js" name="#compareRequestChartParams returns false when the request params is not equal" time="0.003">
    </testcase>
  </testsuite>
  <testsuite name="selectors/models/tagsSelector" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.362" tests="20">
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isVisible" time="0.002">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isActivated status 等于 activated 的 tag 应该返回 true" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isActivated status 不等于 activated 的 tag 应该返回 false" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isPageEventType eventType === page 的应该返回 true" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isPageEventType eventType !== page 的应该返回 false" time="0">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isMrgdEventType eventType === mrgd 的应该返回 true" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isMrgdEventType eventType !== mrgd 的应该返回 false" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isElemEventType eventType === elem 的应该返回 true" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isElemEventType eventType !== elem 的应该返回 false" time="0">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isClckAction actions 中含有 clck 的应该返回 true" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isClckAction actions 中不含有 clck 的应该返回 false" time="0">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isImpAction actions 中含有 imp 的应该返回 true" time="0">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isImpAction actions 中不含有 imp 的应该返回 false" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isChngAction actions 中含有 chng 的应该返回 true" time="0">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isChngAction actions 中不含有 chng 的应该返回 false" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isPageAction actions 中含有 page 的应该返回 true" time="0">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector filter - isPageAction actions 中不含有 page 的应该返回 false" time="0.001">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector selector - tagsSelector" time="0">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector selector - visibleTagsSelector" time="0.002">
    </testcase>
    <testcase classname="tagsSelector.spec.js" name="selectors/models/tagsSelector selector - activatedVisibleTagsSelector" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="Button" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.4" tests="3">
    <testcase classname="index.test.js" name="Button renders correctly" time="0.016">
    </testcase>
    <testcase classname="index.test.js" name="Button renders with tip correctly" time="0.005">
    </testcase>
    <testcase classname="index.test.js" name="Button renders withoutBg correctly" time="0.006">
    </testcase>
  </testsuite>
  <testsuite name="test component FieldCheckbox" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.444" tests="1">
    <testcase classname="index.test.js" name="test component FieldCheckbox do snapshot" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="DataFilter" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.422" tests="7">
    <testcase classname="index.test.tsx" name="DataFilter render children should render children component with parent data" time="0.004">
    </testcase>
    <testcase classname="index.test.tsx" name="DataFilter filter data should ignore if filter value and match were undefined" time="0.01">
    </testcase>
    <testcase classname="index.test.tsx" name="DataFilter filter data should filter data with default equal filter" time="0.002">
    </testcase>
    <testcase classname="index.test.tsx" name="DataFilter filter data should filter data with given filter" time="0.003">
    </testcase>
    <testcase classname="index.test.tsx" name="DataFilter filter data should filter data by predicate if provided" time="0.001">
    </testcase>
    <testcase classname="index.test.tsx" name="DataFilter filter data should update state if value changed" time="0.004">
    </testcase>
    <testcase classname="index.test.tsx" name="DataFilter filter data should add filter to state if not exist" time="0.015">
    </testcase>
  </testsuite>
  <testsuite name="AuthEditor" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.349" tests="1">
    <testcase classname="index.test.js" name="AuthEditor renders correctly" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="test component DebounceButton" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.454" tests="3">
    <testcase classname="index.test.js" name="test component DebounceButton will render correctly with Button" time="0.004">
    </testcase>
    <testcase classname="index.test.js" name="test component DebounceButton onClick will be called when Button is be clicked" time="0.015">
    </testcase>
    <testcase classname="index.test.js" name="test component DebounceButton do snapshot" time="0.005">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component Empty" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.334" tests="2">
    <testcase classname="index.test.js" name="Testing the component Empty will render correctly" time="0.005">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component Empty do snapshot" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="projectsReducer" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.402" tests="8">
    <testcase classname="projectsReducers.spec.js" name="projectsReducer #appApp returns the new app with the given attribute" time="0.009">
    </testcase>
    <testcase classname="projectsReducers.spec.js" name="projectsReducer #appApp returns the new app with projectKeyId" time="0.007">
    </testcase>
    <testcase classname="projectsReducers.spec.js" name="projectsReducer #updateProducts returns the products widht new product" time="0.002">
    </testcase>
    <testcase classname="projectsReducers.spec.js" name="projectsReducer #updateProduct update product normally" time="0.002">
    </testcase>
    <testcase classname="projectsReducers.spec.js" name="projectsReducer #cacheProjectData returns the new project" time="0.003">
    </testcase>
    <testcase classname="projectsReducers.spec.js" name="projectsReducer #setEdittingProduct returns the state with given edittingProduct" time="0.001">
    </testcase>
    <testcase classname="projectsReducers.spec.js" name="projectsReducer #setDeletingProduct returns the state with given deletingProduct" time="0.001">
    </testcase>
    <testcase classname="projectsReducers.spec.js" name="projectsReducer #updateEdittingProduct returns the edittingProduct with new attr" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="editSegmentationHelper" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.363" tests="1">
    <testcase classname="editSegmentationHelper.test.js" name="editSegmentationHelper editSegmentationHelper transformPayloadToState" time="0.005">
    </testcase>
  </testsuite>
  <testsuite name="cache latest" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.381" tests="2">
    <testcase classname="cacheLatest.test.js" name="cache latest cache correctly" time="0.035">
    </testcase>
    <testcase classname="cacheLatest.test.js" name="cache latest cache array args correctly" time="0.021">
    </testcase>
  </testsuite>
  <testsuite name="test component FieldTextArea" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.412" tests="2">
    <testcase classname="index.test.js" name="test component FieldTextArea it will render correctly without error" time="0.015">
    </testcase>
    <testcase classname="index.test.js" name="test component FieldTextArea it will render correctly with error" time="0.003">
    </testcase>
  </testsuite>
  <testsuite name="installSdkReducers" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.412" tests="7">
    <testcase classname="installSdkReducers.spec.js" name="installSdkReducers nextStep" time="0.003">
    </testcase>
    <testcase classname="installSdkReducers.spec.js" name="installSdkReducers previousStep" time="0.001">
    </testcase>
    <testcase classname="installSdkReducers.spec.js" name="installSdkReducers updateTempProductForm" time="0.001">
    </testcase>
    <testcase classname="installSdkReducers.spec.js" name="installSdkReducers resetState" time="0.001">
    </testcase>
    <testcase classname="installSdkReducers.spec.js" name="installSdkReducers enableFormValidation" time="0.002">
    </testcase>
    <testcase classname="installSdkReducers.spec.js" name="installSdkReducers updateState" time="0">
    </testcase>
    <testcase classname="installSdkReducers.spec.js" name="#updateInvitingEngineer returns the invitingEngineer with given attrs" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="testing reducer" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:38" time="0.407" tests="9">
    <testcase classname="index.test.js" name="testing reducer test action ON_ANTI_FRAUD_SEARCH_VALUE_CHANGE" time="0.015">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_ANTI_FRAUD_PRODUCT_VISIBLE_CHANGE" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_ALL_ANTI_FRAUD_SETTINGS_FETCH_START" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_ALL_ANTI_FRAUD_SETTINGS_FETCHED" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_ANTI_FRAUD_SETTING_PANEL_SHOW" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_ALL_ANTI_FRAUD_SETTINGS_FETCH_FAIL" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_ANTI_FRAUD_SETTING_FETCHED" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_ANTI_FRAUD_SETTING_CHANGE" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_ANTI_FRAUD_SETTING_PANEL_HIDE" time="0.009">
    </testcase>
  </testsuite>
  <testsuite name="Event platform" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.49" tests="6">
    <testcase classname="index.test.ts" name="Event platform getEventsCommonPlatforms should return empty array if given events has no platform in common" time="0.005">
    </testcase>
    <testcase classname="index.test.ts" name="Event platform getEventsCommonPlatforms should return corresponding platforms if given a single event" time="0.001">
    </testcase>
    <testcase classname="index.test.ts" name="Event platform getEventsCommonPlatforms should return event platforms in common" time="0.001">
    </testcase>
    <testcase classname="index.test.ts" name="Event platform getEventsCommonPlatforms should return result with ALL_PLATFORM if any event&apos;s platform was &apos;all&apos;" time="0.001">
    </testcase>
    <testcase classname="index.test.ts" name="Event platform getEventsCommonPlatforms should return result with ALL_PLATFORM if any event&apos;s platform was empty" time="0.001">
    </testcase>
    <testcase classname="index.test.ts" name="Event platform getEventsCommonPlatforms should return only one ALL_PLATFORM" time="0">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component InitialEmpty" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.309" tests="2">
    <testcase classname="index.test.js" name="Testing the component InitialEmpty will render correctly" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="Testing the component InitialEmpty do snapshot" time="0.006">
    </testcase>
  </testsuite>
  <testsuite name="pinyinFilter" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.419" tests="3">
    <testcase classname="pinyinFilter.spec.js" name="pinyinFilter isContain returns true if given a heteronym and simple selling" time="0.003">
    </testcase>
    <testcase classname="pinyinFilter.spec.js" name="pinyinFilter isContain returns false if given the simple selling that don&apos;t match the target" time="0.001">
    </testcase>
    <testcase classname="pinyinFilter.spec.js" name="pinyinFilter getAllPinYins returns all possible matching simple spelling array if given a heteronym" time="0.002">
    </testcase>
  </testsuite>
  <testsuite name="validationRules" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.32" tests="11">
    <testcase classname="validationRules.spec.js" name="validationRules none: if params is none return true" time="0.001">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules required: if params is none return false" time="0.001">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules required: if params not none return true" time="0.001">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules arrayNotEmpty: if params is none return false" time="0.001">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules arrayNotEmpty: if params is none return false" time="0">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules arrayNotEmpty: if params array not none return true" time="0">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules ascArray: if params is not array return false" time="0">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules ascArray: if params is nul return false" time="0.001">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules ascArray: if params is asc array return true" time="0">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules ascArray: if params is asc array return true" time="0.001">
    </testcase>
    <testcase classname="validationRules.spec.js" name="validationRules ascArray: if params is dasc array return true" time="0">
    </testcase>
  </testsuite>
  <testsuite name="Testing the 👉Error👈 component" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.265" tests="2">
    <testcase classname="index.test.js" name="Testing the 👉Error👈 component Error will render correctly with mock props" time="0.004">
    </testcase>
    <testcase classname="index.test.js" name="Testing the 👉Error👈 component do Error snapshot" time="0.003">
    </testcase>
  </testsuite>
  <testsuite name="Ads Permission Model&apos;s unit test: actionCreator" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.306" tests="10">
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: onSelectedUserForPermission" time="0.004">
    </testcase>
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: onSelectedRoleForPermission" time="0.001">
    </testcase>
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: onClearForPermission" time="0.001">
    </testcase>
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: onPostPermission" time="0.002">
    </testcase>
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: onDeletePermission" time="0.011">
    </testcase>
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: onFetchedUserPermission" time="0.001">
    </testcase>
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: onChangeOneAclForPermission" time="0">
    </testcase>
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: onChangeOneProductAclForPermission" time="0.001">
    </testcase>
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: onChangeAllAclForPermission" time="0.001">
    </testcase>
    <testcase classname="actions.test.js" name="Ads Permission Model&apos;s unit test: actionCreator actionCreator: setAuthoritySearch" time="0">
    </testcase>
  </testsuite>
  <testsuite name="#transformFilterValueToOld" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.309" tests="7">
    <testcase classname="dimensionFilter.spec.js" name="#transformFilterValueToOld single value" time="0.002">
    </testcase>
    <testcase classname="dimensionFilter.spec.js" name="#transformFilterValueToNew single value" time="0.001">
    </testcase>
    <testcase classname="dimensionFilter.spec.js" name="#transformDimensionFilterToNew empty case" time="0.001">
    </testcase>
    <testcase classname="dimensionFilter.spec.js" name="#transformDimensionFilterToNew one filter case" time="0.001">
    </testcase>
    <testcase classname="dimensionFilter.spec.js" name="#transformDimensionFilterToNew multiple filter cases, and there is invalid cases" time="0.001">
    </testcase>
    <testcase classname="dimensionFilter.spec.js" name="#transformDimensionFilterToOld empty case" time="0">
    </testcase>
    <testcase classname="dimensionFilter.spec.js" name="#transformDimensionFilterToOld multiple filter cases, and there is invalid cases" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="ActivityItem" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.361" tests="2">
    <testcase classname="index.test.js" name="ActivityItem ActivityItem Snapshot" time="0.047">
    </testcase>
    <testcase classname="index.test.js" name="ActivityItem ActivityItem render children" time="0.003">
    </testcase>
  </testsuite>
  <testsuite name="ActivityIsNotStart unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.295" tests="1">
    <testcase classname="ActivityIsNotStart.test.js" name="ActivityIsNotStart unit test ActivityIsNotStart snapshot" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="#stringifyObjValues" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.315" tests="1">
    <testcase classname="routingActions.spec.js" name="#stringifyObjValues stringify should only stringify obj values" time="0.002">
    </testcase>
  </testsuite>
  <testsuite name="Testing the 👉IconCircle👈 component" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.326" tests="1">
    <testcase classname="index.test.js" name="Testing the 👉IconCircle👈 component do IconCircle component snapshot" time="0.033">
    </testcase>
  </testsuite>
  <testsuite name="SelectInfo unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.309" tests="1">
    <testcase classname="index.test.js" name="SelectInfo unit test SelectInfo snapshot" time="0.004">
    </testcase>
  </testsuite>
  <testsuite name="testing reducer" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.337" tests="9">
    <testcase classname="index.test.js" name="testing reducer test action ON_CREATE_START" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_HIDE_EDIT_PANEL" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_CREATE_COMPLETE" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_EDIT_COMPLETE" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_DELETE_COMPLETE" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_SHOW_EDIT_PANEL" time="0.005">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_CREATE_FAIL" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_EDIT_FAIL" time="0">
    </testcase>
    <testcase classname="index.test.js" name="testing reducer test action ON_DELETE_FAIL" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="OnboardingCard unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.366" tests="1">
    <testcase classname="index.test.js" name="OnboardingCard unit test OnboardingCard snapshot" time="0.008">
    </testcase>
  </testsuite>
  <testsuite name="Testing the component 👉NoPermission👈" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:39" time="0.304" tests="1">
    <testcase classname="index.test.js" name="Testing the component 👉NoPermission👈 do the NoPermission component snapshot" time="0.025">
    </testcase>
  </testsuite>
  <testsuite name="test function ruleRunner" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:40" time="0.171" tests="2">
    <testcase classname="index.test.js" name="test function ruleRunner when type equals regexp" time="0.002">
    </testcase>
    <testcase classname="index.test.js" name="test function ruleRunner when type equals regexp is empty string" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="Testing 👉Either👈 component" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:40" time="0.203" tests="3">
    <testcase classname="index.test.js" name="Testing 👉Either👈 component Either will render children-component if has right" time="0.003">
    </testcase>
    <testcase classname="index.test.js" name="Testing 👉Either👈 component Either would not render children-component if has no right" time="0.001">
    </testcase>
    <testcase classname="index.test.js" name="Testing 👉Either👈 component do Either component snapshot" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="helper" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:40" time="0.185" tests="4">
    <testcase classname="helper.test.js" name="helper getObjectAttr should return undefind if obj or key was not given" time="0.007">
    </testcase>
    <testcase classname="helper.test.js" name="helper getObjectAttr should return value when given single word key" time="0.001">
    </testcase>
    <testcase classname="helper.test.js" name="helper getObjectAttr should return value when given camel case key " time="0">
    </testcase>
    <testcase classname="helper.test.js" name="helper getObjectAttr should return correspoding snake case value when given camel case key " time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="Testing the 👉HyperLink👈 component" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:40" time="0.235" tests="2">
    <testcase classname="index.test.js" name="Testing the 👉HyperLink👈 component HyperLink will render correctly with props" time="0.018">
    </testcase>
    <testcase classname="index.test.js" name="Testing the 👉HyperLink👈 component do HyperLink component snapshot" time="0.016">
    </testcase>
  </testsuite>
  <testsuite name="conditionHelper" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:40" time="0.202" tests="2">
    <testcase classname="conditionHelper.test.js" name="conditionHelper conditionHelper convertToObject" time="0.003">
    </testcase>
    <testcase classname="conditionHelper.test.js" name="conditionHelper conditionHelper convertToObject" time="0.002">
    </testcase>
  </testsuite>
  <testsuite name="h5Details unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:40" time="0.202" tests="1">
    <testcase classname="index.test.js" name="h5Details unit test h5Details snapshot" time="0.001">
    </testcase>
  </testsuite>
  <testsuite name="RealTimeChart unit test" errors="0" failures="0" skipped="0" timestamp="2020-02-25T02:31:40" time="0.21" tests="1">
    <testcase classname="index.test.jsx" name="RealTimeChart unit test RealTimeChart snapshot" time="0.001">
    </testcase>
  </testsuite>
</testsuites>
```



