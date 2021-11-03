# String

- String用于表示文本数据

- 有最大长度 2^53-1（并不是指字符数，指utf16编码单位，即16位2字节）

   ```javascript
    '😄'.length // 16*2位 / 16 = 2
   ```

- 字符串的charAt、charCodeAt、length方法都是针对utf16编码的

- BMP(基本字符区域 : Unicode中**0-2^16(U+0000~U+FFFF)**的码点)，

  一个字符就是1个utf16编码单位；超出，则2个utf16编码单位

- 字符串一经确定即不能更改，有值类型的特征

  



# Number

- Number类型所有数值都以 IEEE-754 标准的64位双精度浮点数进行存储

- 精度丢失问题

  > ```javascript
  > 0.1 + 0.2 === 0.3 // false
  > ```
  >
  > 
  >
  > 改正：
  >
  > ```javascript
  > Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON // true
  > ```
  >
  > **检查等式左右两边差的绝对值是否小于最小精度，才是正确的比较浮点数的方法**

- 有 2^64-2^53+3 个值

- 额外的三个值是NaN、-Infinity、Infinity （为了在除以-0、0时不出错）