##### 移除最后一个div（退格功能）。

```
$("#xxx div:last-child").remove();
```



##### js里可以用c:foreach，惊了。



##### 在js里最好只用单引号进行html的拼接，不然会出现莫名其妙的错误。



##### 取消radio的选中状态。

```js
$("input[name='xxx']").removeAttr("checked");
```



##### 点击按钮改变颜色。

```javascript
var lsNum = 1;
//条件查询
function clean(num) {
    if (num != null && num !== '') {
        // 返回原颜色
        if (lsNum !== num) {
            $("#searchName").val("");
            document.getElementById("num" + lsNum).style.background = "#009688";
        }
        lsNum = num;
        // 修改颜色
        document.getElementById("num" + num).style.background = "#5FB878";
    } else {
        if (lsNum !== 0) {
            num = lsNum;
        }
    }
    var searchName = $("#searchName").val().trim();
    var tuhaoProductNoFF = {
        "num": num,
        "searchName": searchName
    };
    $("#tuhaoDataGrid").datagrid('reload', tuhaoProductNoFF);
    $("#cls").click();
}
```

还是用原生的js方法好用，jq感觉很多方法不灵的。



##### Ajax传递数组。

```javascript
data: {ids: ids},
traditional: true
```

dataType:"json"  不写。



##### Select2取（多个）选中项的值。2019.11.19

这里的val对应后端设置的id，

返回值是一个list集合。

```js
var valList = $("#xxx").select2('val');
```



##### Select取多个选中的title。2019.11.19

```javascript
var select = document.getElementById("chooseTuhaoSelect2");
var pros = [];
for (i = 0; i < select.length; i++) {
    if (select.options[i].selected) {
        pros.push(select[i].title);
    }
}
```



##### 具有 true 和 false 两个属性的属性，如 checked, selected 或者 disabled 使用prop()，其他的使用 attr()。2019.11.19

```javascript
$('input:checkbox[name="xxx"]').each(function (i) {   		       $(this).prop("checked","checked");                 $(this).prop("checked","checked");
})
```



##### 遍历input中class包含"pnameList"的值，并添加到数组。2019.11.20

```javascript
$('input[class*="pnameList"]').each(function (i) {
	if ($(this).is(":checked")) {
		lnames.push($(this).val());
		pros.push($(this).val());
	}
});
```



##### forEach遍历数组，把input中class包含"pnameList"的相同的值勾选（checkbox）。2019.11.20

```javascript
var lname = '${tuhaoProductGGD.lname}';
if (lname != null && lname != '' && lname != undefined) {
	var lnames = lname.split(",");
	lnames.forEach(function (i) {
        $("input[class*='pnameList']").each(function (j) {
            if ($(this).val() == i.trim().toString()) {
                $(this).prop("checked", "checked");
            }        
        })
	})
}
```



##### Select2在回显的时候，由于select框中没有值，需要先在页面中取值（数据来源后端）。2019.11.20

##### 在html事件中（如onclick）调用js方法时，如果参数使用el表达式取值，那么这个参数需要加上单引号''，否则会出现错误：Uncaught SyntaxError: Invalid or unexpected token。2019.11.20

##### js报错：xxx is not a function  	这时候试着换一个方法命名，今天方法名用了downImg报错，但是改掉就好了。2019.11.20

##### <c:set var="indexNum" value="${out.index}${inner.index}"/>在el表达式内无法做数据类型转换，可以用c:set。

##### 元素拖拽排序

```js
//sortable拖拽排序
$(function () {
    $("#sortable").sortable({
        stop: function (event, ui) {
            checkGs();
        }
    });
    $("#sortable").disableSelection();
});
```

##### EasyUI的queryParams属性只在进入页面的时候生效一次，如果在同一页面进行了其它操作，使页面重新加载了一次（如搜索），那么这个属性会失效。

