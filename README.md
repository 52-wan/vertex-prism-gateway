# Vertex Prism Gateway

面向多上游模型服务的轻量级 AI API 网关，专注于高可用路由、熔断降级、可观测性与单二进制交付。

## 核心特性

- **多上游 Vertex AI / OpenAI 兼容路由**：统一对外暴露兼容 OpenAI 的请求入口，支持在多个 Vertex AI 区域/凭证及 OpenAI 兼容上游之间按策略路由与故障切换。
- **滑动窗口 429 / 5xx 熔断与 TTFT 监控**：基于滑动时间窗口实时追踪上游限流（429）与服务端错误（5xx），自动触发熔断隔离与健康探测恢复，并持续采集首字延迟（TTFT）等关键性能指标。
- **虚拟 API Key 限流**：支持签发与管理虚拟 API Key，针对不同调用方配置独立的速率限制（RPM / TPM）与访问权限。
- **单二进制 `go:embed` + SQLite WAL 架构**：前端控制台静态资源通过 `go:embed` 直接内嵌至单个 Go 可执行文件，配置、路由状态与监控记录基于本地 SQLite（WAL 模式）持久化，零外部中间件依赖即可部署运行。

## 快速开始

### 本地运行

```bash
go run ./cmd/gateway
```

默认监听 `:8080`，健康检查端点：

```bash
curl http://localhost:8080/health
```

### 编译构建

```bash
go build -o gateway ./cmd/gateway
```
