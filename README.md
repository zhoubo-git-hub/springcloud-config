# springcloud-config

用于 Spring Cloud Config 学习或测试的集中配置仓库。不同环境的示例配置分别存放在独立 YAML 文件中，由 Config Server 或其他配置读取方按环境加载。

## 配置文件

| 文件 | 环境 | 当前内容 |
|---|---|---|
| `config-dev.yml` | 开发环境 | `config.info` 开发配置标识 |
| `config-test.yml` | 测试环境 | `config.info` 测试配置标识 |
| `config-prod.yml` | 生产环境 | `config.info` 生产配置标识 |

默认分支为 `master`。

## 命名约定

当前文件遵循：

```text
{application}-{profile}.yml
```

其中：

- `application`：配置名称，本仓库示例为 `config`
- `profile`：环境名称，如 `dev`、`test`、`prod`
- Git 分支可作为 Config Server 的 label 使用

具体访问路径取决于 Spring Cloud Config Server 的配置。常见请求形式为：

```text
/{application}/{profile}/{label}
```

例如：

```text
/config/dev/master
```

## 使用建议

1. 在 Config Server 中配置本仓库地址和读取凭据。
2. 客户端使用与自身环境对应的 profile。
3. 修改配置后，通过配置中心的刷新机制或重启客户端使其生效。
4. 每次修改提交清晰的版本说明，避免只写模糊的“update”。

## 安全规范

这是公开仓库，禁止提交：

- 数据库、Redis 或消息队列真实密码
- API Key、Token、私钥和证书
- 内网地址、真实账号或个人信息
- 生产环境敏感开关和业务机密

敏感值应通过环境变量、密钥管理服务或配置中心的加密能力注入。示例值必须使用明显的占位符。

## 当前定位

仓库目前只包含简单的 `config.info` 示例，适合验证 Spring Cloud Config 的环境切换和版本读取，不应直接作为生产配置仓库使用。

## License

尚未指定许可证。除非后续明确添加开源许可证，否则保留所有权利。
