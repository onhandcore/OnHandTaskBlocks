# 第三方组件与运行时

本候选包不包含 CPython 解释器、Python 标准库、.NET Framework、Thoroughfare、ForkJoin、其他 OnHand 产品或 pip 第三方包。后端字节码仅使用 Python 标准库；Native 前端调用 Windows/.NET 的 WinForms、Drawing 和 Web.Extensions。web/index.html 未引入远程 CDN 或外部脚本库。公开薄入口、业务字节码和前端 EXE 均为本产品构建产物。

这些外部运行时须由用户或 Host 通过合法来源独立取得并遵守各自许可。本包没有复制其运行时二进制，因而没有把它们的许可当作本产品再分发授权。未来若改为捆绑运行时，必须重新盘点并随包履行其许可证/声明义务；本结论不可套用。

Python 官方许可资料：https://docs.python.org/3.12/license.html 。Python 自身含多个独立许可部分，取得和再分发 Python 时应保留其发行版完整许可。Microsoft .NET Framework 的许可随实际取得的 Windows/.NET 产品提供。本包不对第三方重新授权。

内部构建检查未找到本产品源文件中的第三方版权标记，但这不构成自有代码权利链证明。权利人已声明持有第一方版权并批准本包 LICENSE；OnHand Core 是创作者个人署名及品牌，不是公司。该声明不替代对每项来源的独立法律鉴证，亦不涉及第三方版权。当前不虚构第三方许可证，也不以其他 OnHand 产品的 MIT 许可替代本产品许可。
