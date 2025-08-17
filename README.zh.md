# 🌍 带邮件验证的全栈Todo应用程序

使用Spring Boot后端和React前端构建的综合Todo应用程序，通过邮件验证系统提供安全的身份验证功能。

## 🌐 可用语言 / Available Languages / 言語選択

- [🇰🇷 한국어](README.md) (默认)
- [🇺🇸 English](README.en.md)
- [🇯🇵 日本語](README.ja.md)
- [🇨🇳 中文](README.zh.md)
- [🇪🇸 Español](README.es.md)

---

## 🚀 主要功能

### 核心功能
- **用户身份验证**: 安全的注册和登录系统
- **邮件验证**: 通过SMTP发送6位验证码
- **Todo管理**: 创建、读取、更新、删除和切换完成状态
- **用户资料**: 个人信息和设置管理
- **JWT身份验证**: 使用刷新令牌的无状态身份验证

### 邮件验证系统
- **6位验证码**: 安全的数字验证码
- **10分钟过期**: 安全性的自动代码过期
- **速率限制**: 防止邮件轰炸（1分钟冷却时间）
- **重新发送功能**: 用户可以请求新的验证码
- **专业模板**: 美观的HTML邮件模板
- **账户激活**: 登录前需要邮件验证

### 安全功能
- **密码哈希**: BCrypt加密
- **输入验证**: 全面的服务器端验证
- **CORS配置**: 安全的跨域请求
- **基于角色的访问**: 用户和管理员角色管理
- **受保护路由**: 前端路由保护

## 🛠️ 技术栈

### 后端
- **框架**: Spring Boot 3.x
- **语言**: Java 17+
- **数据库**: H2（内存数据库）
- **安全**: 使用JWT的Spring Security
- **邮件**: 使用Thymeleaf模板的Spring Boot Mail
- **构建工具**: Gradle

### 前端
- **框架**: React 18+
- **语言**: JavaScript/JSX
- **HTTP客户端**: 带拦截器的Axios
- **路由**: React Router v6
- **状态管理**: Context API
- **样式**: 带响应式设计的CSS模块

## 📋 先决条件

在运行此应用程序之前，您需要：

- **Java 17+** 已安装并配置
- **Node.js 16+** 和npm已安装
- **Gradle 7+** （或使用包含的包装器）
- **邮件账户** 用于SMTP配置（推荐Gmail）

## 🚀 安装和设置

### 1. 克隆存储库
```bash
git clone <repository-url>
cd fullstack-practice-cursor
```

### 2. 后端设置

#### 导航到后端目录
```bash
cd backend
```

#### 配置邮件设置
在后端目录中创建`.env`文件或设置环境变量：

```bash
# Gmail SMTP配置
export EMAIL_USERNAME=your-email@gmail.com
export EMAIL_PASSWORD=your-app-password
export EMAIL_FROM=noreply@todoapp.com

# 或创建.env文件：
EMAIL_USERNAME=your-email@gmail.com
EMAIL_PASSWORD=your-app-password
EMAIL_FROM=noreply@todoapp.com
```

#### Gmail应用密码设置
1. 在Gmail账户中启用两步验证
2. 生成应用密码：
   - 转到Google账户设置
   - 安全 → 两步验证 → 应用密码
   - 为"邮件"生成密码
   - 使用此密码作为`EMAIL_PASSWORD`

#### 构建和运行后端
```bash
# 使用Gradle包装器
./gradlew build
./gradlew bootRun

# 或使用系统Gradle
gradle build
gradle bootRun
```

后端在`http://localhost:8080`启动

### 3. 前端设置

#### 导航到前端目录
```bash
cd app
```

#### 安装依赖
```bash
npm install
```

#### 启动开发服务器
```bash
npm start
```

前端在`http://localhost:3000`启动

## 📧 邮件配置

### SMTP设置
应用程序预配置为Gmail SMTP：

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=${EMAIL_USERNAME}
spring.mail.password=${EMAIL_PASSWORD}
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

### 替代邮件提供商
您可以为其他提供商修改`application.properties`：

#### Outlook/Hotmail
```properties
spring.mail.host=smtp-mail.outlook.com
spring.mail.port=587
```

#### Yahoo
```properties
spring.mail.host=smtp.mail.yahoo.com
spring.mail.port=587
```

## 🔐 默认管理员账户

应用程序在启动时创建默认管理员用户：

- **用户名**: `admin`
- **密码**: `Admin123!`
- **邮件**: `admin@example.com`
- **状态**: 邮件已验证并启用

## 📱 API端点

### 身份验证
```
POST   /api/auth/register           - 用户注册
POST   /api/auth/verify-email       - 使用代码验证邮件
POST   /api/auth/resend-verification - 重新发送验证码
POST   /api/auth/login              - 用户登录
POST   /api/auth/logout             - 用户登出
GET    /api/auth/me                 - 获取当前用户信息
```

### Todos（受保护路由）
```
GET    /api/todos          - 获取用户的todos
GET    /api/todos/{id}     - 获取特定todo
POST   /api/todos          - 创建新todo
PUT    /api/todos/{id}     - 更新todo
DELETE /api/todos/{id}     - 删除todo
PATCH  /api/todos/{id}/toggle - 切换完成状态
```

## 🔄 邮件验证流程

### 1. 用户注册
1. 用户填写注册表单
2. 系统创建账户（已禁用）
3. 生成验证码并发送
4. 用户重定向到验证页面

### 2. 邮件验证
1. 用户通过邮件接收6位验证码
2. 用户在验证表单中输入验证码
3. 系统验证验证码和过期时间
4. 账户激活并启用
5. 发送欢迎邮件
6. 用户重定向到登录页面

### 3. 登录访问
1. 用户使用凭据登录
2. 系统检查邮件验证状态
3. 如果已验证，生成JWT令牌
4. 允许用户访问受保护的路由

## 🎨 邮件模板

应用程序包含三个专业的邮件模板：

1. **验证邮件**: 包含验证码的欢迎消息
2. **欢迎邮件**: 成功验证后发送
3. **密码重置**: 用于未来的密码重置功能

所有模板都是响应式的，包括：
- 专业的品牌设计
- 清晰的行动号召按钮
- 安全通知和过期警告
- 移动友好的设计

## 🧪 测试

### 后端测试
```bash
cd backend
./gradlew test
```

### 前端测试
```bash
cd app
npm test
```

### 邮件测试
1. 使用真实的邮件账户进行测试
2. 如果邮件没有到达，检查垃圾邮件文件夹
3. 验证SMTP凭据是否正确
4. 发送多个请求测试速率限制

## 🐛 故障排除

### 常见问题

#### 邮件未发送
- 验证SMTP凭据
- 确保Gmail应用密码正确
- 检查Gmail中是否启用了2FA
- 验证防火墙/网络限制

#### 验证码问题
- 验证码在10分钟后过期
- 最多5次验证尝试
- 重新发送请求之间有1分钟冷却时间
- 检查邮件垃圾邮件文件夹

#### 构建错误
- 确保安装了Java 17+
- 检查Gradle版本兼容性
- 验证所有依赖项是否已解决

#### 前端问题
- 清除浏览器缓存和localStorage
- 检查JavaScript错误的控制台
- 确保后端在端口8080上运行

### 调试模式
在`application.properties`中启用调试日志：
```properties
logging.level.com.example.todoapp=DEBUG
logging.level.org.springframework.mail=DEBUG
```

## 🔒 安全考虑

- **验证码在10分钟后过期**
- **速率限制**防止邮件轰炸
- **最大尝试次数**防止暴力攻击
- **生产环境中需要HTTPS**
- **敏感数据的环境变量**
- **所有端点的输入验证**

## 🚀 生产部署

### 环境变量
设置生产值：
- `jwt.secret`: 强大且唯一的密钥
- `spring.mail.username`: 生产邮件账户
- `spring.mail.password`: 生产应用密码
- 数据库连接详细信息

### 安全头
在生产中启用安全头：
- HTTPS强制
- CORS限制
- 速率限制
- 输入清理

## 📝 贡献

1. 分叉存储库
2. 创建功能分支
3. 进行更改
4. 为新功能添加测试
5. 提交拉取请求

## 📄 许可证

此项目在MIT许可证下获得许可 - 详情请参阅LICENSE文件。

## 🤝 支持

支持和问题：
- 在存储库中创建问题
- 检查故障排除部分
- 查看API文档

## 🎯 路线图

- [ ] 密码重置功能
- [ ] 两步验证
- [ ] 社交登录集成
- [ ] 移动应用开发
- [ ] 高级todo功能（类别、优先级）
- [ ] 团队协作功能
- [ ] API速率限制
- [ ] 全面的测试覆盖率

---

**编码愉快！🎉**
