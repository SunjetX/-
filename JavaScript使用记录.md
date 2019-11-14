##### 移除最后一个div（退格功能）

```
$("#xxx div:last-child").remove();
```

##### js里可以用c:foreach，惊了

##### 在js里最好只用单引号进行html的拼接

##### 取消radio的选择状态

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