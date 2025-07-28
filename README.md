# TLS MCP 配置项目

这个项目用于配置和运行 TLS MCP 与火山引擎的 MCP 服务。

## 物业工单系统设计

基于此MCP配置，我们设计了一个物业工单系统，用于处理维修报修业务。详细设计请参考 [PROPERTY_WORK_ORDER_SYSTEM_DESIGN.md](PROPERTY_WORK_ORDER_SYSTEM_DESIGN.md) 文件。

## 后端API设计

后端API设计文档请参考 [BACKEND_API_DESIGN.md](BACKEND_API_DESIGN.md)

## 后端服务

本项目包含一个基于Node.js的后端服务实现，用于处理物业工单系统的核心功能。

### 依赖安装

在首次运行之前，请安装项目依赖：

```bash
npm install
```

### 启动服务

安装依赖后，可以通过以下命令启动服务：

```bash
# 生产环境启动
npm start

# 开发环境启动（需要先安装nodemon）
npm install -g nodemon
npm run dev
```

服务默认运行在端口3000，启动后可以看到默认的管理员账户信息。

### 默认账户

- 管理员账户：
  - 用户名：XINZHONG
  - 密码：xinzhong

- 客户账户：需要自行注册

## 前端界面

项目包含一个简单的前端界面原型 `work-order-frontend.html`，展示了物业工单系统的用户界面设计，支持：

- 客户注册和登录
- 客户创建维修工单
- 客户查看自己的工单进度
- 管理员查看所有工单
- 管理员分配工单给师傅
- 管理员标记工单完成
- 管理员导出工单数据
- 管理员同步数据到飞书表格

### 使用方法

1. 启动后端服务：`npm start`
2. 在浏览器中打开 `work-order-frontend.html` 文件
3. 使用默认管理员账户或注册新客户账户登录

> 注意：前端界面需要后端服务支持，确保后端服务已在运行。

## 初始化步骤

1. 初始化 Git 仓库: `git init`
2. 创建 MCP 配置文件
3. 安装必要的依赖

## 常见问题解决

如果遇到 `--with` 需求解析失败的问题，请检查:
- MCP 配置文件是否正确
- 依赖项是否完整安装
- 网络连接是否正常

## 测试 MCP 连接

你可以运行以下命令来测试 MCP 连接:

```bash
./test-mcp-connection.sh
```

如果连接成功，你会看到 "成功: 能够连接到 MCP 服务器" 的消息。

如果连接失败，请检查:
- MCP 配置文件中的服务器 URL 是否正确
- 网络连接是否正常
- 防火墙设置是否阻止了连接

## RDS MySQL MCP 端口配置问题

如果遇到 RDS MySQL MCP 服务器启动时出现 `ValueError: invalid literal for int() with base 10: 'MCP server监听端口'` 错误，请运行以下命令:

```bash
./fix-rds-mysql-mcp.sh
```

这个脚本会:
1. 设置正确的环境变量 `MCP_SERVER_PORT=8000`
2. 安装 `mcp-server-rds-mysql` 包（如果尚未安装）
3. 启动 RDS MySQL MCP 服务器