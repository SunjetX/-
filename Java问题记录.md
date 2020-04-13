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

##### xxx is not a function：需要注意的是：id不能与函数名相同。

##### 扩大a标签的点击范围

```css
a {
    line-height: 50px;    
    display: inline-block;    
    width: 100%;
}
```

**JS中，重新加载页面而不是新打开一个页面：location.href。**



**HTML中，如果希望a标签内的文字垂直居中，那么style内可以设置行高line-height。**



**SQL中的case语句：**

```xml
<select id="findSetValuesByUpid" resultMap="BaseResultMap" parameterType="java.lang.Integer">
    SELECT
    a.*,
    CASE
    nameMark
    WHEN 0 THEN
    b.TrueName
    WHEN 1 THEN
    c.userName
    END AS trueName
    FROM
    data_product_set_values AS a
    LEFT JOIN data_user AS b ON a.sysuserid = b.id
    LEFT JOIN data_jy_systemUser AS c ON a.sysuserid = c.id
    <where>
        <if test="upid != null">
            a.upid = #{upid}
        </if>
    </where>
    ORDER BY
    a.id DESC
</select>
```


**SQL中设置变量：DECLARE @prefix VARCHAR(50);set @prefix = '10%';**



**Mybatis中也有类似switch的语句：choose-when-otherwise**



**通过JSON从后端穿前端的过程中被修改了属性名大小写怎么办：在实体的属性上添加@JsonProperty("xxx")**



**js日期格式化，去掉时分秒**

```
formatter: function (value, row, index) {
	return /\d{4}-\d{1,2}-\d{1,2}/g.exec(value);
}
```



**SQL中查询数据，如果为null则自定义返回的值，类似三元表达式**

```SQL
isnull(value1, value2)
value1为列名，value2为替换后的值。如：
isnull(name, '佚名')
意思是如果name为空的话，就返回佚名。
```



##### Cause: com.microsoft.sqlserver.jdbc.SQLServerException: 数据类型 varchar 和 varbinary 在 add 运算符中不兼容

'%' + searchName + '%'	通常是这里出了问题



##### SQL中有or的条件需要格外注意括号



##### RequiresPermissions多个权限只需满足其中一项写法：

```java
@RequiresPermissions(value = {"tuhao_main_isbz", "tuhao_sh_isbz"}, logical = Logical.OR)
```



**IDEA设置忽略文件的方法**

首先，未被纳入版本控制的文件，可以在.ignore文件中预先配置好忽略；

其次，如果已经被纳入版本控制，但是不希望修改之后被提交的，就创建一个changelist用来放这些文件。



