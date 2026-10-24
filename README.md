# OnHandTaskBlocks

English | [简体中文](README.zh-CN.md)

Official **2.0.0** [Release](https://github.com/onhandcore/OnHandTaskBlocks/releases/tag/v2.0.0) · [Download ZIP](https://github.com/onhandcore/OnHandTaskBlocks/releases/download/v2.0.0/OnHandTaskBlocks-2.0.0-windows-x64-rc8.zip) · [SHA256 file](https://github.com/onhandcore/OnHandTaskBlocks/releases/download/v2.0.0/OnHandTaskBlocks-2.0.0-windows-x64-rc8.zip.sha256). Published: 2026-10-24T17:33:03Z (UTC).

OnHandTaskBlocks is a visual task console for AI Hosts. Turn work into editable task blocks, confirm a plan, control delivery, track progress, select results, and recover work orders through one visible workflow.

## From a task to traceable results

The Host interprets your input and proposes steps and dependencies. You confirm the plan before firing. The console shows delivery, execution, and result states, with work-order recovery and artifact selection.

- **Organize work visually:** edit tasks, confirm plans, arrange dependent steps, and inspect progress and results.
- **Make your preference for external matrix Skills explicit:** enable “Prefer OnHand matrix for task execution” in settings (off by default) to ask the Host to prioritize consideration of currently connected, applicable, and authorized external OnHand matrix Skills. For Hosts that usually favor native capabilities, this communicates your preference directly and can help relevant Skills receive active consideration and use.
- **Fire manually or automatically:** sequential submission is the default. Explicit salvo mode allows a capacity of 2–20. Settings alone never Fire; actual concurrency remains subject to lawful Host and ForkJoin admission.
- **Stop and recover:** STOP submits a stop request. Pausing automatic submission and stopping a Child are separate operations. Recovering an explicitly selected work order pauses automatic mode and preserves selections; data recovery does not transfer an old Host's management rights.
- **Deliver and synchronize:** full task capsules are delivered in emission order. The main-window probe provides mechanical notifications and coordination; the console displays results verified and synchronized by the Host. Delivery, reading, or copying is not execution success.

The Windows Native console is the verified initial interface. The package also includes `web/index.html` and a loopback HTTP service with browser task-interface capabilities. This does not establish a verified cross-platform Web product or a publicly hosted service. Windows starts through the Native supervisor by default; opening the HTML file alone is not a complete installation.

The matrix setting conveys a user preference and a suggested invocation priority. It does not change internal model weights or guarantee that the Host will choose an external Skill every time. Each Fire freezes the current preferences. The Host contract requires that snapshot to accompany the task to its Child, across window handoffs, and through recovery; later settings changes do not rewrite tasks already fired. The Host retains semantic judgment, permission checks, and the final execution decision. The setting does not automatically install, approve, or activate any Skill, or replace OnHandBestFit's candidate-selection role, OnHandThoroughfare's connection and mechanical-routing role, or OnHandForkJoin's actual concurrent execution role. Separate “Default OnHandDrudge” and “Default RecallLedger search” options are on by default. They express an orchestration preference when applicable and a retrieval preference at relevant knowledge boundaries, respectively, subject to each product's formal contract and authorization. They do not require calls on every task or imply automatic knowledge writes.

## TaskBlocks, the Host, and ForkJoin

TaskBlocks handles visual organization, user actions, Fire/STOP requests, capsule delivery, main-window probe coordination, and result display. The Host owns task meaning, actual admission, permission decisions, and execution through lawful mechanisms. It creates real independent Child tasks using its own authorized task-creation facilities.

OnHandForkJoin is a separate product. Its formal contract covers Child concurrency coordination, cooperative STOP, formal RESULT, Join, and related execution controls. TaskBlocks does not include a ForkJoin execution engine. Its delivery probe does not replace ForkJoin's Group Probe or the Parent's Join. Clicking STOP does not prove a Child has stopped; a Fire receipt does not prove creation; UI counts do not establish formal success.

The products are introduced together, retain independent identities, and are intended for coordinated releases without claiming each other's capabilities. Coordinated release does not mean bundled installation or mutual dependency. ForkJoin can run independently of TaskBlocks, and standalone ForkJoin does not require Thoroughfare. Both products are approved for this joint publication batch. See [OnHandForkJoin](https://github.com/onhandcore/OnHandForkJoin) for its independent package and contract.

## Install and start

Extract the complete official Windows x64 ZIP into a separate writable directory. Keep every file and the directory structure, and do not overwrite a running installation. `FILES.sha256` lists individual file hashes.

You need Windows x64, .NET Framework 4.x WinForms, and complete **CPython 3.12 x64**, including its standard library and extension modules such as ctypes. These runtimes are not bundled. The backend needs no additional pip packages. Other Python minor versions cannot load this bytecode. Obtain runtimes from lawful sources; Python is available from python.org.

For example, from PowerShell in the extracted directory:

```powershell
$env:TASKBLOCKS_PYTHON = 'C:\Path\To\Python312\python.exe'
& '.\Start-TaskBlocks.cmd' --check-python
& '.\Start-TaskBlocks.cmd'
```

Replace the example path. `TASKBLOCKS_PYTHON` accepts only the full path to a real interpreter EXE, without arguments; otherwise the launcher uses `python.exe` from PATH. Directories, Office launchers, and Store placeholder aliases are unsupported. Preflight checks implementation, version, architecture, standard library, and interpreter file. Failure starts no instance; passing preflight alone does not prove task execution.

You can also double-click `Start-TaskBlocks.cmd`. No administrator rights or PowerShell Bypass are needed; CMD calls Python directly. The optional PS1 entry remains subject to organizational execution policy. `native/OnHandTaskBlocks.exe` is another launch entry and uses the same interpreter selection. The script runs `python -B -m taskblocks.launch` from the installation directory, opening editing/recovery without creating Child tasks.

User data defaults to `state` inside the installation. Set `TASKBLOCKS_STATE_DIR` before launch to use another writable directory. The related Host, backend, and frontend must share that data root. `TASKBLOCKS_PORT` defaults to 8765. Separate instances must not share ports or data directories.

## Connect a Host and invoke

The editing interface can start on its own. Full task execution requires a compatible, authorized Host, OnHandThoroughfare, and OnHandForkJoin, obtained and integrated separately; none is included. Other Skills are used only when applicable, connected, and authorized. Capability preferences grant no permissions and do not install or automatically execute other products.

The Host must follow the [public Host contract](HOST_CONTRACT.md), complete the reviewed wiring and formal installation lifecycle, and use this installation's actual root and current session/Binding facts. Formal integration uses Thoroughfare ON_DEMAND / DIRECT_HOST_RETURN. The interface is `taskblocks.invoke.invoke(surface, payload)` with `PublicHostSurface(root, task_run_id=None)`. Host imports also require CPython 3.12 x64. Launch payloads use the contractual `contract_version` and `operation=launch`; a prompt requires a stable delivery_id. Read the contract rather than guessing version values or reusing another session's credentials.

The Host must handle the returned lawful GUI handoff and bounded waits in the same turn, continuing through input, plan confirmation, Fire, and result boundaries until business finalization or Native session exit. A connection does not guarantee active selection or execution, and no scheduler wakes an ended Host turn. This package does not register itself, change Host configuration or Bindings, or install dependencies.

## Exit, disconnect, and remove

First have the Host resolve running or uncertain work through the formal protocol, including necessary STOP, Join, and administrative closure. Closing the window does not stop independent Child tasks. Close Native normally and wait for that instance's supervisor and loopback HTTP service to exit. Business completion leaves the window open for result inspection; closing it does not cause a background restart.

For an extracted installation that was never formally registered, remove the program by deleting its directory after exit. It creates no registry entries, services, scheduled tasks, or global shortcuts. For a formally connected installation, first verify quiescence and disconnect it through the lawful lifecycle, then remove its program directory. Do not edit central state manually.

`state` contains work orders, history, and runtime receipts, not disposable cache. Back it up or use an external `TASKBLOCKS_STATE_DIR` when needed. Removing the program leaves external data intact. After the instance exits and diagnostics are no longer needed, the user may clean up temporary `ui-runtime` receipts and bootstrap copies in that data root. Preserve other installations' data.

## Verified scope and limitations

Windows x64 Native is the verified scope. This candidate reuses existing Windows business and installation acceptance covering identical runtime bytes. Real Linux/macOS operation, complete cross-platform browser workflows, and equivalent behavior on other or newer Hosts have not been comprehensively verified. A separate regression on the latest WorkBuddy release is unavailable. Host tools, independent-task creation, and automation differ; check the actual contract and capabilities before integration.

Automatic submission depends on the original Host continuing to process events; it is not an unattended background service. Failure pauses automatic mode, as does opening or recovering a work order. Recovery uses explicitly selected accessible records. Unknown launch or Child-creation outcomes require reconciliation before any retry. Native visual verification is limited: the rocket-return effect has not been directly observed and verified. Frozen UI designs that have not been implemented are outside these capability claims.

The service binds only to loopback. Host HTTP mutations require an externally supplied `TASKBLOCKS_HOST_TOKEN` that must not reach the browser. Direct Python calls remain governed by Host filesystem permissions and local cooperative trust. Do not expose this local tool as a public service or persist manual-handoff bearer/recovery secrets in ordinary reports or capsules. Hidden reasoning export is not provided.

Brief waits can occur throughout the workflow: from Fire to capsule delivery and main-window notification, Host interpretation and processing, formal Child creation and concurrency admission, cross-window information exchange, user corrections during interaction, RESULT/Join processing, and UI state synchronization. Some multi-window workflows may therefore feel slow to respond. This is a real collaboration process with multiple stages; its total waiting time cannot all be attributed to TaskBlocks. Actual speed also depends on the Host, model, task complexity, tool calls, window interactions, and runtime environment. A wait at one stage does not necessarily mean the task has failed; use status feedback to check progress. The current priority is correctness in task execution, status feedback, and result collection. Future product optimization will prioritize reducing unnecessary waits and improving responsiveness, without promising a release date or a fixed performance gain, or claiming those improvements are already implemented.

## License, third parties, and official distribution

Copyright (c) 2026 OnHand Core. OnHand Core is the creator's personal signature and brand. First-party software is distributed as a closed-source product. The Chinese [LICENSE.txt](LICENSE.txt) defines the actual grant: official, complete, unmodified copies may be used free of charge and freely forwarded. This does not grant public distribution rights for modified, adapted, or repackaged versions, or a contractual right to internal first-party maintenance source. Third-party license rights and non-excludable legal rights remain intact. This paragraph is a summary, not a replacement license.

Core is supplied as CPython bytecode and a Native binary without first-party Core maintenance source. Bytecode can be analyzed or reverse engineered; there is no promise that it cannot be reversed. Thin interfaces and environment checks support lawful interoperability and startup. See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for external runtimes and third-party matters.

Download the approved 2.0.0 Windows x64 distribution (build revision windows-x64-rc8) and SHA256 from the [official Releases page](https://github.com/onhandcore/OnHandTaskBlocks/releases). The public repository contains product information, licensing, and necessary public contracts; the complete ZIP is distributed as a Release attachment. Repository documents do not replace the complete package. Obtain it through a verified official channel and compare its SHA256 with the official value.
