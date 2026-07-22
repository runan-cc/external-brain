---
title: Infrastructure as Code (IaC)
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [devops, infrastructure, automation, cloud]
sources: []
confidence: high
---

# Infrastructure as Code (IaC)

## 定义

IaC 是通过**代码声明和管理基础设施**的实践——不再手动在控制台点来点去，而是用配置文件定义服务器、网络、数据库等资源。版本化、可审查、可重现。

## 为什么 IaC

| 手动 | IaC |
|------|-----|
| 手点控制台 | `terraform apply` |
| 环境不一致（"我这能跑啊"） | 相同的配置，相同的环境 |
| 无法审计变更 | Git 日志 = 基础设施审计 |
| 灾难恢复靠运气 | 代码重建整个基础设施 |
| Snowflake Server（独一无二） | Phoenix Server（随时重建） |

## 两种范式

### 声明式 (Declarative)
你描述**想要什么**，工具搞定怎么达到。

```hcl
# Terraform
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.micro"
  count         = 3
}
```

### 命令式 (Imperative)
你描述**要做哪些步骤**。

```yaml
# Ansible
- name: Install nginx
  apt:
    name: nginx
    state: present
- name: Start nginx
  service:
    name: nginx
    state: started
```

## 主要工具

| 工具 | 类型 | 领域 | 特点 |
|------|------|------|------|
| **Terraform** | 声明式 | 资源供给 (Provisioning) | 多云、HCL 语言、State 管理 |
| OpenTofu | 声明式 | Terraform 分支 | 社区驱动，开源保障 |
| **Ansible** | 命令式 | 配置管理 (CM) | Agentless (SSH)、YAML |
| Pulumi | 声明式 | 资源供给 | 用真正的编程语言 (TS/Python/Go) |
| Chef / Puppet | 声明式 | 配置管理 | Agent 模式，Ruby DSL |
| CloudFormation | 声明式 | AWS 专用 | AWS 原生 |
| Crossplane | 声明式 | k8s 原生 IaC | Kubernetes CRD 管理云资源 |

## Terraform 核心概念

| 概念 | 说明 |
|------|------|
| Provider | 云平台插件 (AWS, Azure, GCP, k8s) |
| Resource | 要管理的具体资源 |
| State | 实际基础设施与配置的映射（关键！） |
| Plan | 预览变更 (dry run) |
| Apply | 执行变更 |
| Module | 可复用的 Terraform 配置块 |
| Backend | State 存储位置（S3 + DynamoDB 锁） |

### Terraform 工作流

```
1. 写 .tf 配置
2. terraform plan   → 预览要做哪些改动
3. 人工审查
4. terraform apply  → 执行
5. Git commit + push（IaC = 代码）
```

## CI/CD 中的 IaC

```yaml
# GitLab CI 中自动部署
deploy:
  script:
    - terraform init
    - terraform plan
    - terraform apply -auto-approve
```

## 关系

- [[docker]] — 容器化 + IaC = 基础设施即代码
- [[kubernetes]] — k8s manifests 也是 IaC
- [[ci-cd]] — IaC 通过 CI/CD 自动化执行
