---
title: XOR加密
date: 2019-07-17 15:59:50
tags: js
---

## XOR
XOR 运算有一个很奇妙的特点：如果对一个值连续做两次 XOR，会返回这个值本身。XOR 的这个特点，使得它可以用于信息的加密。
```js
/**
 * xor 加密程序 唯一区别添加了xor和hex默认值
 * @param {Strng} str 待加密字符串
 * @param {Number} xor 异或值
 * @param {Number} hex 加密后的进制数
 * @return {Strng} 加密后的字符串
 */
function encrypto( str, xor, hex ) {
    // 设置默认值
    xor = xor || 1;
    hex = hex || 16;

    if ( typeof str !== 'string' || typeof xor !== 'number' || typeof hex !== 'number') {
        return;
    }
    var resultList = [];
    hex = hex <= 25 ? hex : hex % 25;

    for ( var i=0; i<str.length; i++ ) {
        // 提取字符串每个字符的ascll码
        var charCode = str.charCodeAt(i);
        // 进行异或加密
        charCode = (charCode * 1) ^ xor;
        // 异或加密后的字符转成 hex 位数的字符串
        charCode = charCode.toString(hex);
        resultList.push(charCode);
    }

    var splitStr = String.fromCharCode(hex + 97);
    var resultStr = resultList.join( splitStr );
    return resultStr;
}

/**
 * xor 解密程序 唯一区别添加了xor和hex默认值
 * @param {Strng} str 待加密字符串
 * @param {Number} xor 异或值
 * @param {Number} hex 加密后的进制数
 * @return {Strng} 加密后的字符串
 */
function decrypto( str, xor, hex ) {
    // 设置默认值
    xor = xor || 1;
    hex = hex || 16;

    if ( typeof str !== 'string' || typeof xor !== 'number' || typeof hex !== 'number') {
        return;
    }
    var strCharList = [];
    var resultList = [];
    hex = hex <= 25 ? hex : hex % 25;
    // 解析出分割字符
    var splitStr = String.fromCharCode(hex + 97);
    // 分割出加密字符串的加密后的每个字符
    strCharList = str.split(splitStr);

    for ( var i=0; i<strCharList.length; i++ ) {
        // 将加密后的每个字符转成加密后的ascll码
        var charCode = parseInt(strCharList[i], hex);
        // 异或解密出原字符的ascll码
        charCode = (charCode * 1) ^ xor;
        var strChar = String.fromCharCode(charCode);
        resultList.push(strChar);
    }
    var resultStr = resultList.join('');
    return resultStr;
}

// 测试
const text = 'aaaaaa';
const testText = encrypto(text); // "60q60q60"
decrypto(testText); // "aaa"
```

```js
var ck = 150954;
var gz = 22000;
var mb = 1000000;
function test(ck, gz, mb) {
    var HL = 7.3;
    var GZ = gz + 25000 / HL + 13000 / HL + 5000 / HL;
    var HX = (3000 + 20000 + 5000) / HL + 1000;
    var SY = GZ - HX;
    
    var SUM = ck;
    
    var nowDate = new Date();
    var nowMonth = nowDate.getMonth();
    var nowDay = nowDate.getDate();
    
    var monthSum;
    
    for (var i=nowMonth; i<1000; i++) {
        SUM += SY;
        if (i % 12 === 0) {
            SUM += SY;
            
            SUM -= 30000;
            SUM -= 10000;
        }
        SUM *= 1.01;

        if (SUM >= mb) {
            monthSum = i - 5;
            
            if (nowDay > 10) {
                monthSum ++;
            }
            var nowDateCopy = new Date();
            nowDateCopy.setMonth(monthSum + nowMonth);
            nowDateCopy.setDate(10);
            var day = (nowDateCopy - nowDate) / (1000 * 60 * 60 * 24);
            console.log(day, nowDateCopy.toLocaleString(), monthSum);
            return nowDateCopy;
        }
    }
}
var mbDate = test(ck, gz, mb);

function test2(addCk, addGz) {
    if (addCk) {
        var sumMonth =  (mbDate - new Date()) / (1000 * 60 * 60 * 24) / (365/12);       
    }
}


```

## 参考资料
[js加密解密的方法](https://github.com/chenshenhai/blog/issues/21)
