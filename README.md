## 启动

### 启动方式1：父工程维度（推荐）
1. 父工程的pom文件里添加了tomcat7插件；
2. 可以配置端口和path，不配置默认端口8080，默认path是/模块名称；
3. 修改数据库连接配置，dao模块下的 `resources.spring.applicationContext.xml`；
4. 可以在idea里的maven里找到父工程的tomcat7插件，双击 `tomcat7:run` 启动；

### 启动方式2：web工程维度
1. 父工程的pom文件里添加了tomcat7插件；
2. 可以配置端口和path，不配置默认端口8080，默认path是/模块名称；
3. 使用 `install` 命令，将 dao 和 servise 模块打包发布到本地仓库，或者直接将整个父工程打包发布到本地仓库；
4. 修改数据库连接配置，dao模块下的 `resources.spring.applicationContext.xml`；
5. 可以在idea里的maven里找到web工程的tomcat7插件，双击 `tomcat7:run` 启动；
> 注意：父工程是通过 modules 标签聚合子模块，但是子模块 web 依赖了 service，service 模块又依赖了 dao，本地仓库没有 service 和 dao 的 jar 包，需要将所需要的模块打包发布到本地仓库。

## 默认访问地址
http://localhost:8080/demo-maven-parent-web/items/findDetail

## 测试表、数据创建脚本
```sql
CREATE TABLE `items`  (
  `id` int(11) NOT NULL,
  `name` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL,
  `price` decimal(10, 2) NULL DEFAULT NULL,
  `pic` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL,
  `createtime` datetime NULL DEFAULT NULL,
  `detail` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_general_ci ROW_FORMAT = Dynamic;

INSERT INTO `items` VALUES (1, '张三', 123.00, '2', '2022-11-22 15:52:49', 'XXXX');
```