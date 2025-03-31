# Example Plugin

这是一个为luo9_bot框架开发的示例插件，展示了如何创建和使用luo9_sdk来扩展机器人功能。

## 功能特点

- 演示插件的基本结构
- 展示如何处理消息事件
- 提供异步操作的示例
- 说明如何与luo9_sdk进行交互

## 项目结构
example_plugin/
├── src/
│   └── lib.rs       # 插件主要代码
├── Cargo.toml       # 项目依赖配置
└── README.md        # 项目说明文档

## 技术栈

- Rust 2021 Edition
- tokio 异步运行时
- serde 用于序列化/反序列化
- anyhow 错误处理
- async-trait 异步特性支持
- tracing 日志记录

## 开发说明

### 插件结构

插件通过实现`luo9_sdk`提供的特性(trait)来与机器人框架交互。主要包括：

1. 创建一个实现了必要特性的结构体
2. 实现消息处理逻辑
3. 注册插件到框架

### 依赖配置

插件的`Cargo.toml`配置如下：

```toml
[package]
name = "example_plugin"
version = "0.1.0"
edition = "2021"
authors = ["luoy-oss <2557657882@qq.com>"]

[lib]
crate-type = ["cdylib"]

[dependencies]
luo9_sdk = "1.0.0"
anyhow = "1.0"
async-trait = "0.1"
tokio = { version = "1.0", features = ["full"] }
serde = { version = "1.0", features = ["derive"] }
serde_json = "1.0"
tracing = "0.1"
```

注意 crate-type = ["cdylib"] 配置，这使得插件被编译为动态链接库，可以被主程序动态加载。

## 使用方法
1. 确保已安装Rust工具链
2. 克隆仓库
3. 在项目根目录运行以下命令构建插件：
```bash
cargo build --release
```
4. 编译后的插件文件将位于 target/release/ 目录下
5. 复制编译后的.dll文件到luo9_bot的plugins目录下
6. 配置plugins目录下的config.yaml文件：
```yaml
plugins:
  - name: example_plugin
    enable: true
    priority: 10
  - name: other_plugin1
    enable: true
    priority: 100
  - name: other_plugin2
    enable: true
    priority: 10
```
7. 启动luo9_bot，插件将自动加载并运行

## 插件开发指南
要开发自己的插件，您可以：

1. 复制此示例插件作为模板
2. 修改 lib.rs 中的逻辑以实现您需要的功能
3. 更新 Cargo.toml 中的插件名称和版本
4. 按照上述步骤构建您的插件

## 许可证
GNU General Public License V3.0