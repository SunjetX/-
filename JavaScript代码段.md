##### 移除最后一个div（退格功能）

```
$("#xxx div:last-child").remove();
```



##### js里可以用c:foreach

需要注意的是：标签中的el表达式正常写，不需要加引号；[但是取值的时候必须要加上引号]()！！！否则显示的将是一个类似序号或者地址值的数字。



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
oninput="if(/[^0-9.]/g.test(value))value=value.replace(/[^0-9.]/g,'')"

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

```js
$('#dataGrid').datagrid('hideColumn', 'state');

```



**select2回显数据**

```js
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

```js
$(this).select2("data")[0].text;
```



**select2删除选中项**

```js
$(this).val(null).trigger("change");
```



**js对象转url参数**

```js
/**
     * param 将要转为URL参数字符串的对象
     * key URL参数字符串的前缀
     * encode true/false 是否进行URL编码,默认为true
     *
     * return URL参数字符串
     */
    var urlEncode = function (param, key, encode) {
        if (param == null) return '';
        var paramStr = '';
        var t = typeof (param);
        if (t == 'string' || t == 'number' || t == 'boolean') {
            paramStr += '&' + key + '=' + ((encode == null || encode) ? encodeURIComponent(param) : param);
        } else {
            for (var i in param) {
                var k = key == null ? i : key + (param instanceof Array ? '[' + i + ']' : '.' + i);
                paramStr += urlEncode(param[i], k, encode);
            }
        }
        return paramStr;
    };

```



**js遍历时判断两个元素是否是同一个**

```js
$(dom).is($(this)
```



**radio选中**

```js
$("input:radio[name='isfg']").change(function () {
                if ($("#isfg1").is(":checked")) {
                    $("td[data-fgtuhao]").show();
                }
                if ($("#isfg0").is(":checked")) {
                    $("td[data-fgtuhao]").hide();
                }
            });
```



**清空select2**

```js
$("#tuhaos").val('').trigger("change");
```



**取消选中radio**

```js
$("input:radio[name='isfg']").prop("checked", false);
```



**获取选中radio**

```js
$("input:radio[name='isfg']:checked").val();
```



**批量insert**

insert into xxx (xx,xx)

select xx,xx from xxx



**限制输入0-100**

```js
oninput="if(value>100){value=100}else{value=value.replace(/[^\d]/g,'')}if(value.indexOf(0)==0){value=0}"
```



**ajax传递list对象**

```js
data["yfMarkList[" + i + "].id"] = id;
ajax中data: data
```



**sqlserver获取年月**

```CONVERT(varchar(30), GETDATE(), 120)```



**checkbox是否被选中**

```$("#abc").is(':checked');   ```



**sqlserver日期忽略时分秒**

convert(date, created_date, 23)



**layui年月范围选择**

```js
//年月范围选择
        laydate.render({
            elem: '#rangeTime'
            , trigger: 'click'
            , range: '~' //或 range: '~' 来自定义分割字符
            , done: function (value, date, endDate) {
                let times = value.split('~');
                $("#beginTime").val(times[0].trim());
                $("#endTime").val(times[1].trim());
            }
        });
```



**Object转BigDecimal**

```java
private static BigDecimal getBigDecimal(Object value) {
        BigDecimal ret = null;
        if (value != null) {
            if (value instanceof BigDecimal) {
                ret = (BigDecimal) value;
            } else if (value instanceof String) {
                ret = new BigDecimal((String) value);
            } else if (value instanceof BigInteger) {
                ret = new BigDecimal((BigInteger) value);
            } else if (value instanceof Number) {
                ret = new BigDecimal(((Number) value).doubleValue());
            } else {
                throw new ClassCastException("Not possible to coerce [" + value + "] from class " + value.getClass() + " into a BigDecimal.");
            }
        }
        return ret;
    }
```



**使用tooltip提示框**

```js
 html：
 	data-toggle="tooltip"
 js：
     $('[data-toggle="tooltip"]').tooltip({
        trigger: 'hover',
        placement: 'left'
     });
 css：(底色改为白色，字体改为黑色)
	 .tooltip-inner {
            max-width: 200px;
            padding: 3px 8px;
            color: #000;
            text-align: center;
            background-color: #fff;
            border-radius: 4px;
        }
```



**使用css控制td的高度和宽度，不能控制td，应该在td中再嵌套一个div，通过控制这个div间接控制td的大小**

```css
.hideContent {
    text-overflow: ellipsis;
    overflow: hidden;
    width: 200px;
    height: 40px;
}
```



**给div增加滚动条**(css)

```
overflow:auto
```



**laydate选择年月**

```js
laydate.render({
            elem: '#jhfkDate'
            , type: 'month'
            , trigger: 'click'
            , btns: ['clear', 'confirm']
            , min: getyyMM(1)
            , change: function (value, date) {
                $("#jhskDate").val(value);
            }
            , ready: function (date) {
                $(".layui-laydate").off('click').on('click', '.layui-laydate-list li', function () {
                    $(".layui-laydate").remove();
                });
            }
        });
        
  function getyyMM(range) {
        //创建日期对象
        var date = new Date();

        //获取年份
        var yy = date.getFullYear();

        //获取月份
        // 默认选中的
        var mm = "";
        if (range == 1) {
            mm = date.getMonth() + 1;
        }
        if (range == 2) {
            mm = date.getMonth() + 2;
        }
        // 允许选中的最大值
        if (range == 3) {
            mm = date.getMonth() + 4;
        }
        // 如果月份小于10 前面加0
        mm = (mm < 10 ? "0" + mm : mm);
        // 如果月份大于12 年+1; 月份-12
        yy = mm > 12 ? yy + 1 : yy;
        mm = mm > 12 ? mm - 12 : mm;

        //返回日期
        var time = '';
        if (range == 1) {
            time = yy.toString() + "-" + mm.toString();
        }
        if (range == 2 || range == 3) {
            time = yy.toString() + "-" + mm.toString() + "-" + "01";
        }
        return time;
    }
```



**日期格式转换**

```js
// 日期格式转换
    function dateFormat(fmt, date) {
        let ret;
        const opt = {
            "Y+": date.getFullYear().toString(),        // 年
            "m+": (date.getMonth() + 1).toString(),     // 月
            "d+": date.getDate().toString(),            // 日
            "H+": date.getHours().toString(),           // 时
            "M+": date.getMinutes().toString(),         // 分
            "S+": date.getSeconds().toString()          // 秒
            // 有其他格式化字符需求可以继续添加，必须转化成字符串
        };
        for (let k in opt) {
            ret = new RegExp("(" + k + ")").exec(fmt);
            if (ret) {
                fmt = fmt.replace(ret[1], (ret[1].length == 1) ? (opt[k]) : (opt[k].padStart(ret[1].length, "0")))
            };
        };
        return fmt;
    }
```



**获取当前页面排序**

```js
$("datagrid").datagrid("options").sortName;
$("datagrid").datagrid("options").sortOrder;
```



**监听window.open关闭**

```js
var winObj = window.open('http://www.google.com','google','width=800,height=600,status=0,toolbar=0');
var loop = setInterval(function() {   
    if(winObj.closed) {  
        clearInterval(loop);  
        alert('closed');  
    }  
}, 1000);
```



**layer.confirm**

```
function shAll() {
        layer.confirm("确认通过审核？",{
            btn: ['确定', '取消'],
            shadeClose: true
        }, function (index) {
            $.ajax({
                url: '${ctx}/tuhao/tuhao/productNo/shAll.html',
                type: 'post',
                dataType: 'json',
                data: {},
                success: function (data) {
                    var result = data.result;
                    var message = data.msg;
                    if (result) {
                        layer.msg(message, {
                            icon: 1, //图标
                            time: 1500   //1.5秒关闭(如果不配置,默认是3秒)
                        }, function () {
                            window.$('#datagrid').datagrid('reload');
                            // 关闭窗口
                            x_admin_close();
                        });
                    } else {
                        layer.msg(message, {icon: 2});
                    }
                }
            });
        });
    }
```



**fmt:formatNumber去除千分位**

```jstl
增加属性：ingUsed="false"
```
