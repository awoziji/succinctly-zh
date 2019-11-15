## 计数器列

HBase 的字节输入，字节输出方法与单元格值有一个例外：计数器列。计数器列以与其他列相同的方式存在于表中的列族中，但它们的更新方式不同 - HBase 提供了以原子方式递增计数器值而无需先读取它的操作。

对于 HBase Shell， incr 命令递增计数器单元格值，或者如果它不存在则创建计数器列。您可以选择指定要增加的金额;如果你不这样做，那么 HBase 将增加 1。代码清单 19 显示了两个命令，它们将计数器单元添加到行 rk1 - 第一个添加一个新单元格， c：1 ，默认增量为 1，第二个添加单元格 c：2 ，增量为 100：

代码清单 19：增加计数器列

```
hbase(main):006:0> incr 'counters', 'rk1', 'c:1'
COUNTER VALUE = 1
0 row(s) in 0.0130 seconds

hbase(main):007:0> incr 'counters', 'rk1', 'c:2', 100
COUNTER VALUE = 100
0 row(s) in 0.0090 seconds

```

Shell 的响应在更新后显示计数器的值。计数器是一个非常有用的功能，特别是对于高容量，高并发系统。在 access-logs 表中，我可以使用计数器列来记录用户在系统上花费的时间。

系统审计组件需要将当前使用情况添加到该期间已记录的任何内容，如果用户打开了多个会话，我们可以同时更新同一个单元。如果审计组件的不同实例手动读取现有值，添加到它并同时放置更新，那么我们将遇到竞争条件并且更新将丢失。

使用计数器列，审计组件的每个实例都发出一个递增命令，而不必读取现有值，HBase 负责正确更新数据，防止任何竞争条件。

计数器列的读取方式与其他单元格值的读取方式相同，但在 HBase Shell 中，它们显示为原始字节数组的十六进制表示形式，如代码清单 20 所示，它读取上一个命令中设置的值。请注意，HBase Shell 使用不常见的 ASCII /二进制编码显示数据，因此 x01 是 c 中的值 1：， x00d 是值 c 中的 100：：

代码清单 20：计数器列值

```
hbase(main):008:0> get 'counters', 'rk1'
COLUMN                          CELL                                                                                   
 c:1                            timestamp=1446726973017, value=\x00\x00\x00\x00\x00\x00\x00\x01                        
 c:2                            timestamp=1446726979178, value=\x00\x00\x00\x00\x00\x00\x00d                           
2 row(s) in 0.0140 seconds

```

![](img/00011.jpeg) 注意：您应该始终使用客户端的 increment 命令创建计数器列。如果您将其创建为具有自定义值的普通列，然后尝试递增它，您将收到以下错误：“尝试增加不是 64 位宽的字段。”这是 HBase 说你不能增加一个不在计数器列中的值。