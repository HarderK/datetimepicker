# API方法
- 一般的使用方法，在input元素上调用fdatepicker()方法
- onRender：控制日期的天数哪些为不可选状态，但是不能控制时间为不可选状态，不可选的日期`return disable;`即可,onRender()方法会在生成日历界面时不断调用，date参数表示的就是日历上的一天，如上例，date小于某个日期时，返回 disabled，那么小于这个日期的时间全部不可选

```
$('#endTime').fdatepicker({
    format: 'yyyy-mm-dd hh:ii',		// 日期显示的格式
    pickTime: true		// 使用选择时间，false则不选择时间
    onRender: function(date) {			// 可选
	    let time = new Date(checkin.date.getTime()).setHours(0,0,0);
	    return date.getTime() < time ? 'disabled' : '';
    }
})

```
---
- 最后的data('datepicker')返回的是一个封装的对象(这里表述为userDate)， 调用date()方法可以获取到选中状态的时间。
- on('changeData', func)：监听日期变动，日期变动则触发相应的时间，调用userDate的update()方法设置相应时间选择框的时间。

```
let checkin = $('#beginTime').fdatepicker({
    format: 'yyyy-mm-dd hh:ii',
    pickTime: true
}).on('changeDate', function(ev){

    let begin = new Date($('#beginTime').val());
    let end = new Date( $('#endTime').val());
    if(begin > end || $('#endTime').val() == '') {  
        checkout.update(begin);
    }
}).data('datepicker');

let checkout = $('#endTime').fdatepicker({
    format: 'yyyy-mm-dd hh:ii',
    pickTime: true,
    onRender: function(date) {
        let time = new Date(checkin.date.getTime()).setHours(0,0,0);
        return date.getTime() < time ? 'disabled' : '';
    }
}).data('datepicker')
```