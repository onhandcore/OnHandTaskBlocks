# OnHandTaskBlocks

[English](README.md) | 简体中文

正式 **2.0.0** [Release](https://github.com/onhandcore/OnHandTaskBlocks/releases/tag/v2.0.0) · [下载 ZIP](https://github.com/onhandcore/OnHandTaskBlocks/releases/download/v2.0.0/OnHandTaskBlocks-2.0.0-windows-x64-rc8.zip) · [SHA256 文件](https://github.com/onhandcore/OnHandTaskBlocks/releases/download/v2.0.0/OnHandTaskBlocks-2.0.0-windows-x64-rc8.zip.sha256)。实际公开时间：2026-10-24T17:33:03Z（UTC）。

OnHandTaskBlocks 是面向 AI Host 的可视化任务炮台：把任务整理成可编辑的积木、确认计划，再控制投送、查看进度、选择结果和恢复工单，让多步骤工作有清楚的操作入口。

## 从任务到可追踪的结果

输入任务后，由 Host 理解需求并提交步骤与依赖，用户确认计划后再 Fire。任务面板展示投送、执行与结果状态，支持工单恢复以及结果材料选择。

- **可视化组织**：编辑任务、确认计划，按依赖组织步骤，查看进度与结果。
- **明确外置矩阵技能偏好**：在设置中启用“优先使用 OnHand 矩阵执行任务”（默认关闭），可要求 Host 优先考虑当前已接入、适用且获得授权的 OnHand 外置矩阵 Skill。对于通常倾向原生能力的 Host，这能把用户的外置技能调用偏好明确传达给它，帮助提高相关 Skill 被主动考虑和采用的机会。
- **手动与自动发射**：手动 Fire 或启用自动投送。默认顺序提交；显式启用齐射时，容量可设为 2–20。设置本身不会 Fire，实际并发仍受 Host 和 ForkJoin 的合法接纳约束。
- **停止与恢复**：STOP 提交停止请求；暂停自动发射与停止 Child 是不同操作。恢复明确选择的工单时自动模式暂停，保留选择；恢复数据不会转移旧 Host 的管理权。
- **胶囊投送与同步**：按发射顺序投送完整任务胶囊，主窗口探针提供机械通知与协调，展示经 Host 校验并同步的结果。已投送、已读或已复制均不代表执行成功。

Windows Native 炮台是当前已验证的首发界面。包内也含 `web/index.html` 和回环 HTTP 服务，提供浏览器任务界面相关能力；这不代表已验证跨平台 Web 产品，也不是公网托管服务。Windows 默认启动使用 Native 监督链；不要把随包 Web 文件单独打开当作完整安装。

矩阵设置传递的是用户偏好和调用优先建议，不修改模型内部权重，也不保证 Host 每次都选择外置 Skill。每次 Fire 会冻结当时的偏好；Host 合同要求随任务传给 Child、跨窗口交接并在恢复时沿用原快照，之后修改设置不会改写已发射任务。Host 仍保留语义判断、权限与最终执行决定；该设置不会自动安装、批准或激活任何 Skill，不代替 OnHandBestFit 的候选选择职责、OnHandThoroughfare 的连接与机械路由职责，或 OnHandForkJoin 的真实并发执行职责。设置中另有默认开启的“默认调用 OnHandDrudge”和“默认检索 RecallLedger”独立选项，分别表达适用时的编排偏好和相关知识边界的检索偏好；它们同样受各自正式合同及授权约束，不意味着每项任务都必须调用或自动写入知识。

## TaskBlocks、Host 与 ForkJoin

TaskBlocks 负责可视化组织、用户操作、Fire／STOP 请求、胶囊投送、主窗口探针协调和结果展示。Host 负责任务语义、实际接纳、权限决策，以及通过合法机制执行相应操作。真实独立 Child 由 Host 使用自己的合法任务创建机制创建。

OnHandForkJoin 是独立产品，负责其正式合同覆盖的 Child 并发协调、协作式 STOP、正式 RESULT、Join 与相关执行控制。TaskBlocks 不自带 ForkJoin 执行引擎；主窗口投送探针不代替 ForkJoin 的 Group Probe，也不代替 Parent 执行 Join。点击 STOP 不等于 Child 已停止，Fire 回执不等于已创建 Child，界面计数不等于正式成功。

两款产品按联合介绍、独立定位、同步发布、互不冒领的方式协作；同步发布不等于捆绑安装或彼此依赖。ForkJoin 可独立使用，不依赖 TaskBlocks，其 standalone 使用不强制要求 Thoroughfare。两款产品已获准同批公开发行；[OnHandForkJoin 官方仓库](https://github.com/onhandcore/OnHandForkJoin)提供其独立构件及合同。

## 安装与启动

完整解压官方 Windows x64 ZIP 到用户可写的独立目录，保留所有文件和目录结构，不覆盖运行中的旧版本。可用 `FILES.sha256` 核验逐文件摘要。

需要 Windows x64、.NET Framework 4.x WinForms，以及完整 **CPython 3.12 x64** 和标准库（包括 ctypes 等扩展模块）。这些运行时不随包提供；后端无需额外 pip 包。其他 Python 次版本不能加载本包字节码。请通过合法来源取得运行时，Python 可从 python.org 取得。

在解压目录运行，例如 PowerShell 中：

```powershell
$env:TASKBLOCKS_PYTHON = 'C:\Path\To\Python312\python.exe'
& '.\Start-TaskBlocks.cmd' --check-python
& '.\Start-TaskBlocks.cmd'
```

请替换示例路径。`TASKBLOCKS_PYTHON` 只填写真实解释器 EXE 的完整路径，不附加参数；未设置时使用 PATH 中的 `python.exe`。目录、Office 启动器和商店占位别名不受支持。预检检查实现、版本、位数、标准库及解释器文件，失败不会启动实例；预检通过本身不证明完整任务执行成功。

也可双击 `Start-TaskBlocks.cmd`。无需管理员权限或 PowerShell Bypass；CMD 直接调用 Python。可选 PS1 入口仍受组织执行策略管理。`native/OnHandTaskBlocks.exe` 也可启动，使用同一解释器选择规则。启动脚本在安装目录调用 `python -B -m taskblocks.launch`，只打开编辑／恢复入口，不自动创建 Child。

默认用户数据目录是安装目录下的 `state`；可在启动前用 `TASKBLOCKS_STATE_DIR` 指定其他可写目录。相关 Host、后端与前端必须使用相同数据目录。`TASKBLOCKS_PORT` 默认 8765；不同实例不要复用端口或数据目录。

## 连接 Host 与调用

编辑界面可单独启动；完整任务执行需要兼容且已获授权的 Host、OnHandThoroughfare 和 OnHandForkJoin，均须另行取得和接入，本包不包含它们。其他 Skill 仅在适用、已接入且获授权时使用。设置中的能力偏好不授予权限，也不安装或自动执行其他产品。

Host 应按 [公开 Host 合同](HOST_CONTRACT.md) 完成接线审查和正式安装生命周期，使用本安装的实际根目录、当前会话及 Binding 事实。正式路径为 Thoroughfare 的 ON_DEMAND / DIRECT_HOST_RETURN；接口为 `taskblocks.invoke.invoke(surface, payload)`，`PublicHostSurface(root, task_run_id=None)`。Host 导入也要求 CPython 3.12 x64。启动 payload 使用合同规定的 `contract_version` 和 `operation=launch`；有 prompt 时须提供稳定 delivery_id。不要凭示例猜测版本值或重用其他会话凭据。

Host 必须处理返回的合法 GUI 交接及同轮有界等待，持续接收输入、计划确认、Fire 与结果边界，直到业务正式收口或 Native 会话退出。连接成功不代表 Host 会主动选择执行，也没有自动唤醒已结束 Host 回合的调度器。本包不会自注册、修改 Host 配置、Binding 或安装依赖。

## 退出、断开与卸载

先由 Host 按正式协议处理仍在运行或结果未知的任务，完成必要的 STOP、Join 与行政收口。关闭窗口不会停止独立 Child。通过 Native 窗口关闭按钮退出，等待该实例监督进程与回环 HTTP 服务退出。业务完成保留窗口供查看结果；窗口退出后不会在后台重启。

仅解压且未正式注册的安装，退出后删除解压目录即可移除程序，无注册表项、服务、计划任务或全局快捷方式。已正式接入的安装，先通过合法生命周期核实静止并断开，再删除程序目录；不要手改中央状态。

`state` 保存工单、历史和运行回执，不是可统一删除的缓存。需要时先备份，或使用外部 `TASKBLOCKS_STATE_DIR`；删除程序不会清理外部数据。数据目录内的临时 `ui-runtime` 回执与 bootstrap 副本，在实例已退出且不再需要诊断后由用户决定清理，不要删除其他安装的数据。

## 验证范围与已知限制

Windows x64 Native 是当前已验证范围；本候选复用覆盖相同运行字节的既有 Windows 业务和安装验收。Linux、macOS 真机运行、跨平台浏览器完整流程、其他 Host 及新版 Host 的等价行为未得到全面验证；最新 WorkBuddy 独立回归未提供。不同 Host 的工具、独立任务创建及自动化程度不同，接入前须核实其正式合同和可用能力。

自动发射依赖原 Host 持续处理事件；它不是无人值守后台服务。失败会暂停自动模式，恢复或打开工单也会暂停。恢复只使用明确选择且可访问的记录。启动或 Child 创建结果未知时必须先核对，不可盲目重试创建。Native 视觉细节的验证有限，火箭返程视觉效果未获直接观察验证；设计冻结但尚未施工的 UI 优化不在本说明能力范围内。

服务只绑定回环；Host HTTP 修改接口需要外部提供的 `TASKBLOCKS_HOST_TOKEN`，不得暴露给浏览器。直接 Python 调用受 Host 文件权限及本地协作信任边界约束。不要把此本地工具暴露为公网服务，不要将手动交接 bearer／恢复秘密写入普通报告或胶囊；不提供隐藏推理导出。

从点击 Fire，到胶囊投送、主窗口通知、Host 理解和处理任务、正式 Child 创建与并发接纳，再到跨窗口信息交换、用户交互修正、RESULT／Join 处理及界面状态同步，各阶段都可能出现短暂等待，使某些多窗口工作流在使用时感觉响应较慢。这是多阶段的真实协作流程，不能把全部等待时间归因于 TaskBlocks；实际速度也受 Host、模型、任务复杂度、工具调用、窗口交互和运行环境影响。某个阶段需要等待不代表任务必然失败，仍应结合状态反馈核实进展。当前优先保持任务执行、状态反馈和结果回收的正确性；后续产品优化会优先考虑减少不必要等待、改善响应体验，但不承诺具体版本日期或固定性能提升，也不表示这些优化已经完成。

## 许可、第三方与正式取得方式

Copyright (c) 2026 OnHand Core。OnHand Core 是创作者个人署名及品牌。第一方采用闭源成品发行，准确授权以中文 [LICENSE.txt](LICENSE.txt) 为准：官方完整、未经修改的原版允许免费使用和自由转发；不因此授予修改、改编或重新包装后公开分发的权利，也不授予要求提供第一方内部维护源码的合同权利。第三方原有许可及法律保留权利不受影响。

Core 以 CPython 字节码与 Native 二进制提供，不附带第一方核心维护源码；字节码可以被分析或逆向，不承诺不可逆向。薄接口和环境预检材料用于合法互操作与启动。外部运行时和第三方事项见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

获准发行的 2.0.0 Windows x64 构件（修订 windows-x64-rc8）及 SHA256 通过[官方 Releases 页面](https://github.com/onhandcore/OnHandTaskBlocks/releases)提供。公开仓库以介绍、许可及必要公开合同为主，完整产品 ZIP 单独通过 Release 分发。仓库说明不能替代完整产品包；请从经核实的官方渠道取得完整包并核对官方 SHA256。
