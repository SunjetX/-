##### 移除最后一个div（退格功能）

```
$("#xxx div:last-child").remove();
```



##### js里可以用c:foreach

需要注意的是：标签中的el表达式正常写，不需要加引号；但是取值的时候必须要加上引号！！！否则显示的将是一个类似序号或者地址值的数字。



##### 在js里最好只用单引号进行html的拼接，不然会出现莫名其妙的错误。



##### 取消radio的选中状态

```js
$("input[name='xxx']").removeAttr("checked");
```



##### 点击按钮改变颜色

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



##### Ajax传递数组

```javascript
data: {ids: ids},
traditional: true
```

dataType:"json"  不写。



##### Select2取（多个）选中项的值

这里的val对应后端设置的id，

返回值是一个list集合。

```js
var valList = $("#xxx").select2('val');
```



##### Select取多个选中的title

```javascript
var select = document.getElementById("chooseTuhaoSelect2");
var pros = [];
for (i = 0; i < select.length; i++) {
    if (select.options[i].selected) {
        pros.push(select[i].title);
    }
}
```



##### 具有 true 和 false 两个属性的属性，如 checked, selected 或者 disabled 使用prop()，其他的使用 attr()

```javascript
$('input:checkbox[name="xxx"]').each(function (i) {   		       $(this).prop("checked","checked");                 $(this).prop("checked","checked");
})
```



##### 遍历input中class包含"pnameList"的值，并添加到数组

```javascript
$('input[class*="pnameList"]').each(function (i) {
	if ($(this).is(":checked")) {
		lnames.push($(this).val());
		pros.push($(this).val());
	}
});
```



##### forEach遍历数组，把input中class包含"pnameList"的相同的值勾选（checkbox）

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



##### Select2在回显的时候，由于select框中没有值，需要先在页面中取值（数据来源后端）。



##### 在html事件中（如onclick）调用js方法时，如果参数使用el表达式取值，那么这个参数需要加上单引号''，否则会出现错误：Uncaught SyntaxError: Invalid or unexpected token。



##### js报错：xxx is not a function  	这时候试着换一个方法命名，今天方法名用了downImg报错，但是改掉就好了。



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



##### 存在即更新，不存在则插入

```
if not exists (select * from current_stock where cinv_code = #{cinvCode} and c_wh_code = #{cWhCode} and del_flag = 0)      
		insert into current_stock(cinv_code, i_quantity, c_wh_code, create_by, create_date, update_by, update_date) values(#{cinvCode}, #{iQuantity}, #{cWhCode}, #{updateBy}, #{updateDate}, #{updateBy}, #{updateDate})   
else
		update current_stock set i_quantity = i_quantity + #{iQuantity}, update_by = #{updateBy}, update_date = #{updateDate} where cinv_code = #{cinvCode} and c_wh_code = #{cWhCode} and del_flag = 0
```



##### Mybatis插入后返回id

标签中添加属性，keyProperty="id" useGeneratedKeys="true"，插入后直接返回给传进来的对象



##### ajax避免重复提交

```javascript
beforeSend: function () {
	$("#submitButton").attr("disabled", true);
},
complete: function () {
	$("#submitButton").removeAttr("disabled");
}
```



##### easyUI清除勾选状态

```
onLoadSuccess:function(data){
	$('#dataGrid').datagrid('clearChecked');
}
```



##### 如果遇到JSON字段丢失的问题

在属性上加@JsonProperty("")



##### @Transactional(rollbackFor = Exception.class)

可以扩大事务控制的范围（Exception包括了RuntimeException和非运行时异常如：SQL、IOExeption等），如果不在括号里指定，默认是RuntimeException。



##### Select2既可以查询又可以输入

tags: true



**layer.open首次打开不居中的问题**

通过css解决的方案：

```javascript
layer.style(index, {
	left: '50%', 
	position: 'absolute', 
	top: '50%', 
	transform: 'translate(-50%, -50%)'
});
```



**js加锁防止重复提交**

```
var lock = false;
if (!lock) {
    lock = true;
    执行代码...
}
```



**javaScript只允许输入数字和小数点**

```
onpropertychange="if(/[^0-9.]/g.test(value))value=value.replace(/[^0-9.]/g,'')"
```



**javaScript只允许输入数字**

```
onkeyup="if(this.value.length==1){this.value=this.value.replace(/[^0-9.]/g,'')}else{this.value=this.value.replace(/\D/g,'')}"
onafterpaste="if(this.value.length==1){this.value=this.value.replace(/[^0-9.]/g,'')}else{this.value=this.value.replace(/\D/g,'')}"
```



**限制输入**

```
// 判断只能输入纯数字或者小数点，及负整数
        function clearNoNum(event, obj) {
            //响应鼠标事件，允许左右方向键移动
            event = window.event || event;
            if (event.keyCode == 37 | event.keyCode == 39) {
                return;
            }
            var t = obj.value.charAt(0);
            //先把非数字的都替换掉，除了数字和.
            obj.value = obj.value.replace(/[^\d.]/g, "");
            //必须保证第一个为数字而不是.
            obj.value = obj.value.replace(/^\./g, "");
            //保证只有出现一个.而没有多个.
            obj.value = obj.value.replace(/\.{2,}/g, ".");
            //保证.只出现一次，而不能出现两次以上
            obj.value = obj.value.replace(".", "$#$").replace(/\./g, "").replace("$#$", ".");
            //如果第一位是负号，则允许添加   如果不允许添加负号 可以把这块注释掉
             if (t == '-') {
                 obj.value = '-' + obj.value;
             }
        }
        
 // 限制数字位数
        function numSizeLimit(th) {
            var regStrs = [
                ['^(\\d+\\.\\d{1}).+', '$2'] //禁止录入小数点后2位以上
            ];
            for (var i = 0; i < regStrs.length; i++) {
                var reg = new RegExp(regStrs[i][0]);
                th.value = th.value.replace(reg, regStrs[i][1]);
            }
        }
```



**日期格式转换**

```
	/**
     * 日期格式转换
     */
    function dateFormater(value) {
        var str = '';
        if (value != undefined && value != null) {
            var dt = new Date();
            dt.setTime(value);
            var year = dt.getFullYear();//查询年份
            var month = dt.getMonth() + 1;//查询月份
            if (Number(month) < 10) {
                month = '0' + month;
            }
            var date = dt.getDate();//查询当月日期
            if (Number(date) < 10) {
                date = '0' + date;
            }
            str = year + "-" + month + "-" + date;
        }
        return str;
    }
```



**格式化日期（去掉时分秒）**

```
/\d{4}-\d{1,2}-\d{1,2}/g.exec(date);
```



**格式化数字**

```
// 格式化数字 千分位
    function fmoney(s, n) {
        n = n > 0 && n <= 20 ? n : 2;
        s = parseFloat((s + "").replace(/[^\d\.-]/g, "")).toFixed(n) + "";
        var l = s.split(".")[0].split("").reverse(),
            r = s.split(".")[1];
        var t = "";
        for (var i = 0; i < l.length; i++) {
            t += l[i] + ((i + 1) % 3 == 0 && (i + 1) != l.length ? "," : "");
        }
        return t.split("").reverse().join("") + "." + r;
    }
```



**生成从minNum到maxNum的随机数**

```
function randomNum(minNum, maxNum) {
        switch (arguments.length) {
            case 1:
                return parseInt(Math.random() * minNum + 1, 10);
            case 2:
                return parseInt(Math.random() * (maxNum - minNum + 1) + minNum, 10);
            default:
                return 0;
        }
    }
```



**EasyUI隐藏列**

```
$('#dataGrid').datagrid('hideColumn', 'state');
```



**select2回显数据**

```
 // 回显数据
    function echoSelect2(dom, value) {
        $.each(value, function (index, value) {
            $(dom).append(new Option(value.text, value.id, false, true));
        });
        $(dom).trigger("change");
    }
    
// value 格式 及 调用方法
	var select2Val = [{id: ccuscode, text: ccuscode + " [" + ccusname + "]"}];
	echoSelect2($("#select2"), select2Val);
```



**select2获取选中text**

```
$(this).select2("data")[0].text;
```