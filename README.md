jqCron for Quartz Framework
============================

Forked and modified original jqCron to support cron expression based for Quartz Framework.

Changes done to the original jqCron.js

```javascript
this.getCron = function(){
	var period = _selectorPeriod.getValue();
	
	// Add 0 as the first item in the array and increment the array index by 1 when setting the value in the below code
	// Added ? where ever applicable in the cron expression to support quartz scheduler
	
	var items = ['0','*', '*', '*', '*', '*'];
	if(period == 'hour') {
		items[1] = _selectorMins.getCronValue();
		items[5] = '?';  // To support Quartz
	}
	if(period == 'day' || period == 'week' || period == 'month' || period == 'year') {
		items[1] = _selectorTimeM.getCronValue();
		items[2] = _selectorTimeH.getCronValue();
		items[5] = '?';  // To support Quartz
	}
	if(period == 'month' || period == 'year') {
		items[3] = _selectorDom.getCronValue();
		items[5] = '?';  // To support Quartz
	}
	if(period == 'year') {
		items[4] = _selectorMonth.getCronValue();
		items[5] = '?';  // To support Quartz
	}
	if(period == 'week') {
		items[3] = '?';  // To support Quartz
		items[5] = _selectorDow.getCronValue();
	}
	return items.join(' ');
};
```

To pre populate selected cron expression back in jqCron, set default_value by removing the first two characters in the cron expression and replacing all ? by *
```javascript
default_value: '0 10 * * *'.substr(2).replace(/\?/g,"*")
```

Madan Narra

For original jQuery plugin goto [this link](https://github.com/arnapou/jqCron)
