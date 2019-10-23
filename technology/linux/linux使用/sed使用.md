# sed 使用

``` bash
# 某一行后添加一行（第四行后）
sed -i '4 a\要添加的内容' t.txt
# 某一行前添加一行（第四行前）
sed -i '4 i\要添加的内容' t.txt
# 替换某一行内容（不是要替换的内容，是指替换后的内容）（第二行）
sed -i '2 c\替换后的内容' t.txt
# 最后一行添加内容（如果有环境变量的话不用用\转义符，不然会当做普通字符处理的）
sed -i "\$a ${tmp}" t.txt
# 查找某一行内容（12行）
sed -n '12p' zoo.cfg
# 匹配内容前添加一行
 sed -i '/allow linux.com/i\allow linux.cn' the.conf.file
```