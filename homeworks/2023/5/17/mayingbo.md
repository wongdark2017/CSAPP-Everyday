### 5.17

___

1. 计算机和编译器支持多种数据格式，用于编码整数和浮点数，以及不同的数据长度。例如，许多计算机具有操作单个字节的指令，同时也支持以2、4和8字节表示的整数。它们还支持以4和8字节表示的浮点数。
2. C语言支持多种整数和浮点数据的数据格式。图2.3展示了不同C数据类型通常分配的字节数（我们将在第2.2节讨论C标准所保证的内容与通常情况下的差异）。一些数据类型的确切字节数取决于程序的编译方式。我们展示了典型的32位和64位程序的大小。整数数据可以是有符号的，能够表示负数、零和正数值，也可以是无符号的，只允许非负值。char数据类型表示一个字节。尽管char名称源自于它被用于存储文本字符串中的单个字符，但它也可以用于存储整数值。short、int和long数据类型旨在提供一系列可用于表示整数值的范围。