# Ruyi SDK 测试报告

## 一、测试概述
本次测试针对 Ruyi SDK 0.46.0 版本进行全流程验证，核心目标是确认包管理器的核心功能在该版本下的可用性与兼容性，保障 RISC-V 64 架构基础开发流程的顺畅性。

## 二、测试范围
- 工具链安装与卸载
- 虚拟环境创建、激活与使用
- 自诊断与缓存清理功能
- 收尾与环境清理流程

## 三、测试环境
- 操作系统：Fedora 39（Linux x86_64）
- Ruyi SDK 版本：0.46.0
- 测试工具链：toolchain/gnu-plct（版本 0.20250912.0）
- 虚拟环境名称：my_riscv_env
- 目标架构：RISC-V 64

## 四、测试用例执行情况
### TC01 安装工具链 toolchain/gnu-plct
- **测试步骤**：执行 `ruyi install toolchain/gnu-plct`
- **测试结果**：工具链安装成功，可通过绝对路径调用
- **状态**：通过

### TC02 创建虚拟环境 my_riscv_env
- **测试步骤**：执行 `ruyi env --toolchain toolchain/gnu-plct generic my_riscv_env`
- **测试结果**：虚拟环境创建成功，目录包含 `bin`、`sysroot` 等核心组件
- **状态**：通过

### TC03 激活虚拟环境
- **测试步骤**：执行 `source /home/pingguo/.config/ruyi/my_riscv_env/bin/ruyi-activate`
- **测试结果**：激活成功，终端可直接使用 `riscv64-plct-linux-gnu-gcc` 编译器
- **状态**：通过

### TC04 交叉编译测试程序
- **测试步骤**：编写 `hello.c` 并执行 `riscv64-plct-linux-gnu-gcc -o hello hello.c`
- **测试结果**：成功生成 `hello` 可执行文件，`file` 命令验证为 RISC-V 格式
- **状态**：通过

### TC05 卸载工具链
- **测试步骤**：执行 `ruyi uninstall toolchain/gnu-plct`
- **测试结果**：toolchain/gnu-plct 工具链卸载成功
- **状态**：通过

### TC06 清理程序缓存
- **测试步骤**：执行 `ruyi self clean --progcache`
- **测试结果**：程序缓存清理命令执行成功，无报错
- **状态**：通过

### TC07 删除虚拟环境
- **测试步骤**：执行 `rm -rf /home/pingguo/.config/ruyi/my_riscv_env`
- **测试结果**：虚拟环境目录被成功删除，环境清理完成
- **状态**：通过

## 五、缺陷分析
本次测试覆盖 Ruyi SDK 包管理器全核心操作流程，所有测试项均按预期执行，未发现功能性、兼容性缺陷，无报错及异常问题。

## 六、测试结论
Ruyi SDK 0.46.0 版本包管理器核心功能稳定可靠，工具链管理、虚拟环境操作、缓存清理、环境收尾等功能均能正常执行，可完全满足 RISC-V 64 架构基础开发的全流程需求。