---
sidebar_position: 3
---

## 1 题目

编写一个函数来验证输入的字符串是否是有效的 IPv4 或 IPv6 地址。

如果是有效的 IPv4 地址，返回 "IPv4" ；
如果是有效的 IPv6 地址，返回 "IPv6" ；
如果不是上述类型的 IP 地址，返回 "Neither" 。
IPv4 地址由十进制数和点来表示，每个地址包含 4 个十进制数，其范围为 0 - 255， 用(".")分割。比如，172.16.254.1；

同时，IPv4 地址内的数不会以 0 开头。比如，地址 172.16.254.01 是不合法的。

IPv6 地址由 8 组 16 进制的数字来表示，每组表示 16 比特。这些组数字通过 (":")分割。比如,  2001:0db8:85a3:0000:0000:8a2e:0370:7334 是一个有效的地址。而且，我们可以加入一些以 0 开头的数字，字母可以使用大写，也可以是小写。所以， 2001:db8:85a3:0:0:8A2E:0370:7334 也是一个有效的 IPv6 address 地址 (即，忽略 0 开头，忽略大小写)。

然而，我们不能因为某个组的值为 0，而使用一个空的组，以至于出现 (::) 的情况。 比如， 2001:0db8:85a3::8A2E:0370:7334 是无效的 IPv6 地址。

同时，在 IPv6 地址中，多余的 0 也是不被允许的。比如， 02001:0db8:85a3:0000:0000:8a2e:0370:7334 是无效的。

**示例 1：**

```txt
输入：IP = "172.16.254.1"
输出："IPv4"
解释：有效的 IPv4 地址，返回 "IPv4"
```

**示例 2：**

```txt
输入：IP = "2001:0db8:85a3:0:0:8A2E:0370:7334"
输出："IPv6"
解释：有效的 IPv6 地址，返回 "IPv6"
```

**示例 3：**

```txt
输入：IP = "256.256.256.256"
输出："Neither"
解释：既不是 IPv4 地址，又不是 IPv6 地址
```

**示例 4：**

```txt
输入：IP = "2001:0db8:85a3:0:0:8A2E:0370:7334:"
输出："Neither"
```

**示例 5：**

```txt
输入：IP = "1e1.4.5.6"
输出："Neither"
```

**提示：**

* IP 仅由英文字母，数字，字符 '.' 和 ':' 组成。

## 2 问题分析

1. **IPv4 判断标准**：
   1. **通过 `.` 分割后的长度必须为 4**。
   2. **每一段的长度必须在 1 到 3 之间**。
   3. **每一段的长度大于 1 时，不能包含前导 0**。
   4. **每一段都必须是数字**。
2. **IPv6 判断标准**：
   1. **通过 `:` 分割后的长度必须为 8**。
   2. **每一段的长度必须在 1 到 4 之间**。
   3. **每一段的字符都必须在 `0123456789abcdefABCDEF` 里面**。
3. 需要注意的是：
   1. `public String[] split(String regex, int limit)`：
      1. 该方法主要**根据匹配给定的正则表达式来拆分此字符串**。
      2. 该方法**返回的数组包含此字符串的子字符串**，**每个字符串都由另一个匹配给定表达式的子字符串终止**，**或者由此字符串末尾终止**，**数组中的子字符串按他们在此字符串中出现的顺序排列**，**如果表达式不匹配输入的任何部分**，**那么所得数组只具有一个元素**，**即此字符串**。
      3. `limit`参数**控制模式应用的次数**，因而**影响所得数组的长度**：
         1. **如果$limit \gt 0$**，则**模式最多被应用$limit - 1$次**，**数组的长度将不会大于$limit$**，而且**数组的最后一项将包含所有超出最后匹配的定界符的输入**。
         2. **如果$limit \lt 0$**，那么**模式将被应用尽可能多的次数**，而且**数组可以是任何长度**。
         3. **如果$limit = 0$**，那么**模式将被应用尽可能多的次数**，而且**数组可以是任何长度**，并且**结尾空字符串将被丢弃**。
      4. 具体实例如下：
         1. 假如有一个字符串`boo:and:foo`，使用这些参数可以生成以下结果：![](https://notebook.grayson.top/media/202111/2021-11-14_221925_952904.png)

## 3 参考代码

```java
/**
 * 468. 验证 IP 地址
 * @param queryIP   输入的字符串
 * @return  验证输入的字符串是否是有效的 IPv4 或 IPv6 地址
 */
public String validIPAddress(String queryIP) {
    if (queryIP.contains(".")) {return validateIPv4(queryIP);}
    else if (queryIP.contains(":")) {return validateIPv6(queryIP);}
    return "Neither";
}

/**
 * 验证输入的字符串是否是有效的 IPv4 地址
 * @param queryIP   输入的字符串
 * @return  验证输入的字符串是否是有效的 IPv4 地址
 */
public String validateIPv4(String queryIP) {
    String[] split = queryIP.split("\\.", -1);
    if (split.length != 4) {return "Neither";}
    for (String str: split) {
        if (str.length() == 0 || str.length() > 3) {return "Neither";}
        if (str.charAt(0) == '0' && str.length() != 1) {return "Neither";}
        for (char c: str.toCharArray()) {
            if (!Character.isDigit(c)) {return "Neither";}
        }
        if (Integer.parseInt(str) > 255) {return "Neither";}
    }
    return "IPv4";
}

/**
 * 验证输入的字符串是否是有效的 IPv6 地址
 * @param queryIP   输入的字符串
 * @return  验证输入的字符串是否是有效的 IPv6 地址
 */
public String validateIPv6(String queryIP) {
    String[] split = queryIP.split(":", -1);
    String hexdigits = "0123456789abcdefABCDEF";
    if (split.length != 8) {return "Neither";}
    for (String str: split) {
        if (str.length() == 0 || str.length() > 4) {return "Neither";}
        for (char c: str.toCharArray()) {
            if (hexdigits.indexOf(c) == -1) {return "Neither";}
        }
    }
    return "IPv6";
}
```

## 参考文献

1. [468. 验证 IP 地址](https://leetcode-cn.com/problems/validate-ip-address)。
2. [验证 IP 地址](https://leetcode-cn.com/problems/validate-ip-address/solution/yan-zheng-ip-di-zhi-by-leetcode)。
