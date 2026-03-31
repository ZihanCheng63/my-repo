# Ruyi SDK IDE (VS Code 插件) 测试报告

## 一、测试概述
本次测试聚焦 Ruyi SDK VS Code 插件核心功能，验证其在 WSL 环境下的完整性与可用性，确认插件与 Ruyi SDK 包管理器的联动能力，保障 RISC-V 程序开发全流程的顺畅执行。

## 二、测试范围
- 虚拟环境创建与激活
- Ruyi 工具链的安装与识别
- RISC-V 程序编写、编译、运行全流程
- 插件界面交互与功能稳定性

## 三、测试环境
- 操作系统：WSL (Ubuntu 24.04)
- VS Code 版本：最新稳定版
- Ruyi SDK 版本：0.46.0
- 硬件配置：标准 x86_64 开发机

## 四、测试用例执行情况

### TC01 源码包提取
- **测试项**：源码包提取
- **测试步骤**：在 VS Code 中使用 RuyiSDK 插件 → 执行 `Extract RuyiSDK Package`
- **测试结果**：成功弹出包列表，可正常选择并解压 `coremark` 等源码包到工作目录
- **状态**：通过

---

### TC02 安装工具链 toolchain/gnu-plct
- **测试项**：安装工具链 toolchain/gnu-plct
- **测试步骤**：执行 `ruyi install toolchain/gnu-plct`
- **测试结果**：工具链安装成功，可通过绝对路径调用
- **状态**：通过

---

### TC03 创建虚拟环境 my_riscv_env
- **测试项**：创建虚拟环境 my_riscv_env
- **测试步骤**：执行 `ruyi env --toolchain toolchain/gnu-plct generic my_riscv_env`
- **测试结果**：虚拟环境创建成功，目录包含 `bin`、`sysroot` 等核心组件
- **状态**：通过

---

### TC04 激活虚拟环境
- **测试项**：激活虚拟环境
- **测试步骤**：执行 `source /home/pingguo/.config/ruyi/my_riscv_env/bin/ruyi-activate`
- **测试结果**：激活成功，可直接使用 `riscv64-plct-linux-gnu-gcc`
- **状态**：通过

---

### TC05 交叉编译测试程序
- **测试项**：交叉编译测试程序
- **测试步骤**：编写 `hello.c` 并执行 `riscv64-plct-linux-gnu-gcc -o hello hello.c`
- **测试结果**：生成 `hello` 可执行文件，`file` 命令验证为 RISC-V 格式
- **状态**：通过

---

### TC06 插件功能测试
- **测试项**：插件功能测试
- **测试步骤**：测试插件界面、按钮、菜单及命令触发
- **测试结果**：所有功能可正常触发，无崩溃、无报错，整体可用性良好
- **状态**：通过

## 五、缺陷分析
本次测试未发现影响核心功能的严重缺陷，不影响整体使用。

## 六、测试结论
插件核心功能全部达标，可用于基础 RISC-V 程序开发与测试。
