# note
#1、如果要使用ipv4连接优先也不禁用ipv6，需要修改gai.conf配置文件使其生效。

编辑 /etc/gai.conf 文件，查找 precedence ::ffff:0:0/96 100 将前面的注释 # 去掉并保存，如果前面没有 # 号表示已经更改过设置了。如果没有查找到该行直接在文件末尾添加上
precedence ::ffff:0:0/96 100

CentOS默认没有 /etc/gai.conf 该文件，可以执行命令
cp -p /usr/share/doc/glibc-common-2.17/gai.conf /etc/

拷贝该文件后修改。

修改完成保存生效。这样设置后有IPv4的话优先使用IPv4，也不影响IPv6的使用。

注：::ffff:0:0/96 为IPv4/IPv6转换地址 (IPv4-mapped IPv6 address)。

#2、如果确实不需要IPv6，我们可以禁用IPv6

执行命令：echo "1" > /proc/sys/net/ipv6/conf/all/disable_ipv6
这样就掉了禁用ipv6，如需恢复的话删除掉 /proc/sys/net/ipv6/conf/all/disable_ipv6 这个文件就可以。
