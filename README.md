# Anime-mall-app
这是一个基于Python Flask后端API和前后端分离的动漫周边电商平台，包含用户端前端、管理端前端和统一的后端API服务。

## 架构设计

- **后端API服务** (端口 5000): 提供统一RESTful API接口
- **管理端前端** (端口 5001): 管理员界面，支持商品管理、分类管理、订单管理、用户管理
- **用户端前端** (端口 5002): 用户界面，支持商品浏览、购物车、订单、收藏等功能
- **数据库**: MongoDB，存储用户、商品、订单、分类等数据

## 技术栈

- **后端**: Flask 2.3.3
- **数据库**: MongoDB 4.4.27
- **数据库连接**: PyMongo 4.5.0
- **密码加密**: bcrypt 4.0.1
- **前端**: HTML/CSS/JavaScript
- **跨域处理**: Flask-CORS 4.0.0
- **容器化**: Docker & Docker Compose
- **HTTP客户端**: requests 2.31.0

## 快速开始

### 方法一：本地运行

1. **克隆项目**
   ```bash
   git clone <your-repo-url>
   cd <repo-directory>
   ```

2. **安装依赖**
   ```bash
   pip install -r requirements.txt
   ```

3. **启动MongoDB服务**
   ```bash
   # 如果本地没有MongoDB，可以跳过此步骤，使用Docker方式
   ```

4. **初始化数据库**
   ```bash
   python init_data.py
   ```

5. **启动服务**
   ```bash
   python start_servers.py
   ```

   服务将运行在以下端口：
   - API服务：http://127.0.0.1:5000 或 http://localhost:5000
   - 管理端：http://127.0.0.1:5001 或 http://localhost:5001
   - 用户端：http://127.0.0.1:5002 或 http://localhost:5002

### 方法二：Docker部署

1. **构建并启动服务**
   ```bash
   docker-compose up --build -d
   ```

2. **查看服务状态**
   ```bash
   docker-compose logs -f
   ```

3. **访问应用**
   - API服务：http://localhost:5000
   - 管理端：http://localhost:5001
   - 用户端：http://localhost:5002

4. **停止服务**
   ```bash
   docker-compose down
   ```

## 功能说明

### 用户端功能（用户端前端 - 端口5002）

1. **用户认证**
   - 新用户注册：输入用户名、邮箱和密码
   - 老用户登录：输入用户名和密码

2. **商品浏览**
   - 查看所有商品
   - 按分类筛选商品
   - 搜索特定商品

3. **购物功能**
   - 添加商品到购物车
   - 查看购物车内容
   - 修改购物车商品数量
   - 删除购物车中的商品

4. **订单管理**
   - 创建订单
   - 查看我的订单
   - 查看订单详情

5. **收藏功能**
   - 收藏喜欢的商品
   - 查看我的收藏
   - 取消收藏

6. **评价功能**
   - 对已完成的订单进行评价
   - 查看其他用户的评价

### 管理端功能（管理端前端 - 端口5001）

1. **管理员登录**
   - 使用管理员账号登录系统

2. **商品管理**
   - 添加新商品：输入名称、描述、价格、库存、分类等
   - 查看所有商品
   - 修改商品信息
   - 删除商品

3. **分类管理**
   - 添加新分类
   - 查看所有分类
   - 修改分类信息
   - 删除分类

4. **订单管理**
   - 查看所有订单
   - 查看订单详情
   - 更新订单状态（待付款→已付款→已发货→已完成）

5. **用户管理**
   - 查看所有用户
   - 查看用户详情

## 默认登录凭据

### 管理员账号
- **admin1**，密码：**admin1231**
- **admin2**，密码：**admin1232**
- **admin3**，密码：**admin1233**
- **admin4**，密码：**admin1234**
- **admin5**，密码：**admin1235**

### 用户账号
- **user1** 到 **user50**，密码：**password1** 到 **password50**

## 数据库结构

- **数据库名**: anime
- **集合**:
  - user：用户信息
  - goods：商品信息
  - order：订单信息
  - category：分类信息
  - admin：管理员信息
  - cart：购物车信息
  - favorite：收藏信息
  - review：评价信息

## 项目结构

```
mongodbApp1/
├── api_server.py              # 后端API服务
├── admin_app.py               # 管理端前端服务
├── user_app.py                # 用户端前端服务
├── config.py                  # 数据库配置
├── init_data.py               # 数据初始化脚本
├── ensure_data_consistency.py # 数据一致性保障脚本
├── start_servers.py           # 多服务启动脚本
├── requirements.txt           # 依赖包列表
├── .env                       # 环境变量配置
├── admin-frontend/            # 管理端前端
│   └── index.html             # 管理端主页面
├── user-frontend/             # 用户端前端
│   └── index.html             # 用户端主页面
├── check_db.py                # 数据库连接检查
├── start_app.py               # 应用启动脚本
├── Dockerfile                 # Docker镜像定义
├── docker-compose.yml         # Docker容器编排
└── README.md                  # 项目说明
```

## 🔧 API接口说明

### 公共接口 (5000端口)

#### 用户注册
- POST /api/user/register
- 请求体: {"username": "用户名", "password": "密码", "email": "邮箱"}

#### 用户登录
- POST /api/user/login
- 请求体: {"username": "用户名", "password": "密码"}

#### 查看商品
- GET /api/goods
- 参数: category_id, keyword

#### 添加购物车
- POST /api/cart/add
- 请求体: {"user_id": "用户ID", "good_id": "商品ID", "quantity": "数量"}

#### 查看购物车
- GET /api/cart
- 参数: user_id

#### 删除购物车项目
- DELETE /api/cart/{cart_item_id}

#### 创建订单
- POST /api/order/create
- 请求体: {"user_id": "用户ID", "items": [], "total_price": "总价"}

#### 查看订单（用户）
- GET /api/order
- 参数: user_id, status

#### 查看订单详情
- GET /api/order/{order_id}

#### 评价订单
- POST /api/order/{order_id}/review
- 请求体: {"user_id": "用户ID", "rating": "评分", "comment": "评价内容"}

#### 添加收藏
- POST /api/favorite/add
- 请求体: {"user_id": "用户ID", "good_id": "商品ID"}

#### 查看收藏
- GET /api/favorite
- 参数: user_id

#### 删除收藏
- DELETE /api/favorite/{favorite_id}

#### 管理员登录
- POST /api/admin/login
- 请求体: {"username": "用户名", "password": "密码"}

#### 添加商品
- POST /api/goods
- 请求体: {"name": "名称", "description": "描述", "price": "价格", "stock": "库存", "category_id": "分类ID", "image_url": "图片链接"}

#### 修改商品
- PUT /api/goods/{good_id}
- 请求体: {"name": "名称", "description": "描述", "price": "价格", "stock": "库存", "category_id": "分类ID", "image_url": "图片链接"}

#### 删除商品
- DELETE /api/goods/{good_id}

#### 添加分类
- POST /api/category
- 请求体: {"name": "名称", "description": "描述"}

#### 修改分类
- PUT /api/category/{category_id}
- 请求体: {"name": "名称", "description": "描述"}

#### 删除分类
- DELETE /api/category/{category_id}

#### 修改订单状态
- PUT /api/order/{order_id}/status
- 请求体: {"status": "状态"}

#### 查看订单（管理员）
- GET /api/orders
- 参数: status

#### 查看分类
- GET /api/category

#### 查看用户（管理员）
- GET /api/user

#### 查看用户详情
- GET /api/user/{user_id}

## 初始化数据

运行 [init_data.py](file://f:\云计算与云服务\mongodbApp1\init_data.py) 脚本将创建:
- 5个管理员
- 50个分类
- 50个用户
- 50件商品
- 50个订单

## 注意事项

- 生产环境中请修改默认管理员密码
- 数据库配置中的IP地址和端口可能需要根据实际环境调整
- 定期备份数据库以防数据丢失
- 在Docker部署时，MongoDB数据会持久化存储
- 请勿在生产环境中使用默认的认证凭据

## 故障排除

1. **无法访问服务**
   - 检查服务是否已启动
   - 确认防火墙设置允许相应端口通信
   - 尝试使用 127.0.0.1 替代 localhost

2. **数据库连接失败**
   - 确认 MongoDB 服务正在运行
   - 检查 config.py 中的数据库配置

3. **页面加载失败**
   - 检查浏览器控制台是否有错误信息
   - 确认 API 服务正在运行且可访问

4. **功能异常**
   - 查看服务日志获取详细错误信息
   - 确认依赖包已正确安装

## 贡献

欢迎提交Issue和Pull Request来帮助改进这个项目！

## 许可证

此项目仅供学习和参考使用。
