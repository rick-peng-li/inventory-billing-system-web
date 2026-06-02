<!-- Git 地址：git@github.com:rick-peng-li/inventory-billing-system-web.git -->

# 库存与开票管理系统

一个基于 MERN 思路实现的库存与账单管理项目，覆盖用户认证、商品管理、客户管理、库存扣减与发票生成等核心流程，适合用作进销存类系统的练手项目、课程设计或后台管理系统基础模板。

- 在线前端地址：https://inventory-frontend-blond.vercel.app
- 项目结构：前后端分目录维护，前端与后端可分别独立启动和部署

## 项目简介

该项目围绕“库存管理 + 销售开票”展开，后端提供 REST API，前端负责业务界面交互，数据库负责保存用户、商品、客户与发票数据。

主要能力包括：

- 用户注册与登录
- 基于 JWT 的身份认证
- 商品增删改查与库存更新
- 客户信息管理
- 购物结算与库存扣减
- 发票保存与发票列表查询
- 基于角色的权限控制（Admin / Staff）

## 项目架构

```text
inventory-billing-system-web
├─ inventory-frontend   React 前端应用
└─ inventory-backend    Express + MongoDB 后端服务
```

架构说明：

- 前端层：基于 React 构建业务界面，负责登录、商品、客户、开票等页面交互
- 接口层：后端使用 Express 提供 `/auth`、`/products`、`/customers`、`/invoices` 等接口
- 认证层：使用 JWT 鉴权，请求通过 `Authorization: Bearer <token>` 访问受保护资源
- 权限层：通过 `Admin` 与 `Staff` 角色区分敏感操作访问权限
- 数据层：使用 MongoDB + Mongoose 存储用户、商品、客户和发票数据
- 部署层：前端可部署到 Vercel，后端可部署到 Render，数据库可使用 MongoDB Atlas

## 技术栈

### 前端

- React 19
- React Router DOM 6
- Axios
- jsPDF
- react-scripts（Create React App）

### 后端

- Node.js
- Express 5
- MongoDB
- Mongoose
- jsonwebtoken
- bcryptjs
- cors
- dotenv

## 后端接口概览

### 认证模块

- `POST /auth/register`：注册用户
- `POST /auth/login`：用户登录并返回 token

### 商品模块

- `GET /products`：查询商品列表
- `POST /products`：新增商品
- `PUT /products/:id`：更新商品信息或库存
- `DELETE /products/:id`：删除商品
- `POST /products/purchase`：采购/购买流程中的库存扣减

### 客户模块

- `GET /customers`：查询客户列表
- `POST /customers`：新增客户
- `PUT /customers/:id`：更新客户信息
- `DELETE /customers/:id`：删除客户

### 发票模块

- `GET /invoices`：查询发票列表或报表数据
- `POST /invoices`：创建并保存发票，同时扣减商品库存

## 权限说明

- 所有业务接口默认需要登录后访问
- `Admin` 角色可执行部分敏感操作，例如商品新增、删除与发票查询
- `Staff` 角色可参与日常业务操作，例如登录、客户管理、开票与库存相关操作

## 数据模型

项目当前包含以下核心模型：

- `User`：用户账号、密码、角色
- `Product`：商品名称、价格、库存数量
- `Customer`：客户名称、电话、邮箱、创建时间
- `Invoice`：商品明细、税费、折扣、总金额、创建时间

## 本地启动方式

### 1. 克隆项目

```bash
git clone git@github.com:rick-peng-li/inventory-billing-system-web.git
cd inventory-billing-system-web
```

### 2. 启动后端

进入后端目录并安装依赖：

```bash
cd inventory-backend
npm install
```

在 `inventory-backend` 目录下创建 `.env` 文件：

```env
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
PORT=5000
```

启动后端服务：

```bash
npm start
```

默认启动地址：`http://localhost:5000`

### 3. 启动前端

新开一个终端，进入前端目录并安装依赖：

```bash
cd inventory-frontend
npm install
npm start
```

默认访问地址：`http://localhost:3000`

## 常用命令

### 前端

```bash
npm start
npm test
npm run build
```

### 后端

```bash
npm start
```

## 部署说明

- 前端：适合部署到 Vercel
- 后端：适合部署到 Render
- 数据库：建议使用 MongoDB Atlas
- 前后端分离部署时，前端接口地址应指向已部署的后端服务

## 适用场景

- 小型库存管理系统原型
- 销售开票与客户管理练习项目
- MERN 全栈学习与作品集展示
- 后台管理系统基础脚手架
