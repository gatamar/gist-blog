`uniqueCount` not stable: https://discuss.newrelic.com/t/confusing-results-count-and-uniquecount-timestamp/58849
```
SELECT count(*)/uniqueCount(session) AS 'Pageviews per Session' FROM PageView
```
