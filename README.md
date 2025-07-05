以下是为租借管理系统用户界面模块编写的完整 `README.md` 文件，包含了项目概述、安装指南、使用说明、技术细节等内容：

# 人工智能学院租借管理系统

该项目是云南经贸外事职业学院人工智能学院开发的租借管理系统的前端用户界面部分，旨在为学院师生提供便捷的物品租借申请和管理功能。系统采用现代化设计，具有良好的用户体验和交互效果。

## 功能特性

1. **租借申请功能**
   - 完整的租借申请表单，包含物品名称、借用理由、日期选择等字段
   - 表单验证机制，确保数据的有效性
   - 防止重复提交功能，避免刷新页面导致的表单重复提交问题

2. **租借记录展示**
   - 历史租借记录表格，清晰展示所有申请状态
   - 不同状态使用颜色区分（待审核、已批准、已拒绝、已归还）
   - 自动识别逾期未归还物品并高亮显示

3. **响应式设计**
   - 适配各种屏幕尺寸，从手机到桌面设备
   - 优化的移动端体验，确保在小屏幕设备上也能方便操作

4. **视觉体验**
   - 现代化UI设计，采用卡片式布局和阴影效果
   - 平滑的动画过渡和交互反馈
   - 专业的配色方案，符合学院形象

## 技术栈

- **前端框架**：Tailwind CSS v3
- **交互效果**：原生JavaScript
- **后端支持**：PHP
- **数据库**：MySQL

## 安装与配置

### 环境要求

- Web服务器（如Apache、Nginx）
- PHP 7.4+
- MySQL 5.7+

### 安装步骤

1. **克隆项目**
   ```bash
   git clone https://github.com/your-repo/ai-college-rental-system.git
   cd ai-college-rental-system
   ```

2. **创建数据库**
   - 在MySQL中创建新的数据库
   - 执行以下SQL语句创建必要的表：
     ```sql
     CREATE TABLE IF NOT EXISTS users (
         id INT AUTO_INCREMENT PRIMARY KEY,
         username VARCHAR(50) NOT NULL UNIQUE,
         password VARCHAR(255) NOT NULL,
         college VARCHAR(100) NOT NULL,
         class VARCHAR(50) NOT NULL,
         name VARCHAR(50) NOT NULL,
         contact VARCHAR(20) NOT NULL,
         role ENUM('user', 'admin') NOT NULL DEFAULT 'user',
         created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
     );

     CREATE TABLE IF NOT EXISTS rentals (
         id INT AUTO_INCREMENT PRIMARY KEY,
         user_id INT NOT NULL,
         item_name VARCHAR(100) NOT NULL,
         borrow_reason TEXT NOT NULL,
         borrow_date DATE NOT NULL,
         return_date DATE NOT NULL,
         status ENUM('pending', 'approved', 'rejected', 'returned') NOT NULL DEFAULT 'pending',
         created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
         FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
     );

     INSERT INTO users (username, password, role, college, class, name, contact)
     VALUES ('admin', '$2y$10$gD7v8rPZJZ2kK6nJZJZ2kOJZJZ2kK6nJZJZ2kOJZJZ2kK6nJZJ', 'admin', '人工智能学院', '管理组', '系统管理员', '13800138000')
     ON DUPLICATE KEY UPDATE username = username;
     ```

3. **配置数据库连接**
   - 创建 `config.php` 文件，内容如下：
     ```php
     <?php
     // 数据库配置
     $host = 'localhost';
     $dbname = 'your_database_name';
     $username = 'your_username';
     $password = 'your_password';

     // 创建数据库连接
     try {
         $conn = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8", $username, $password);
         $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
     } catch(PDOException $e) {
         die("数据库连接失败: " . $e->getMessage());
     }
     ?>
     ```
   - 修改上述配置为你的数据库实际信息

4. **部署文件**
   - 将所有文件上传到Web服务器的文档根目录

5. **访问系统**
   - 通过浏览器访问部署地址，如：`http://localhost/client_dashboard.php`

## 使用指南

### 作为普通用户

1. 访问系统登录页面，使用分配的账号密码登录
2. 在主界面填写租借申请表单
3. 提交申请后可在租借记录表格查看申请状态
4. 已批准的申请若逾期未归还，系统会自动标记为逾期

### 作为管理员

1. 使用管理员账号登录
2. 可以在管理界面查看和处理所有用户的租借申请
3. 可以修改申请状态（批准、拒绝、标记归还）

## 项目结构

```
ai-college-rental-system/
├── client_dashboard.php    # 用户主界面
├── config.php              # 数据库配置
├── login.php               # 登录页面
└── ...
```

## 自定义与扩展

1. **修改样式**
   - 可以通过修改Tailwind配置文件 `tailwind.config.js` 自定义颜色和字体
   - 直接修改HTML中的Tailwind类来调整布局和样式

2. **添加功能**
   - 如需添加新功能，可在现有PHP文件中扩展逻辑
   - 如需添加新页面，可参考现有页面结构创建

3. **表单验证**
   - 客户端验证：修改JavaScript部分的表单提交逻辑
   - 服务器端验证：在PHP文件中调整验证规则

## 贡献指南

1. 提交问题前请先搜索现有issue，避免重复提交
2. 提交Pull Request时请确保代码风格一致
3. 对于重大功能变更，请先创建issue讨论
4. 所有新功能需提供相应的测试和文档

## 许可证

本项目采用 [MIT License](LICENSE)

## 支持与反馈

如有任何问题或建议，请通过以下方式联系我们：
- 邮箱：2141516768@qq.com
