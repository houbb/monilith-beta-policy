# Monilith Beta Policy

Monolith 内测版本的公开策略配置中心。

## 仓库定位

本仓库**仅存放完全可以公开的信息**：

- 最新版本信息
- 最低可用版本
- 被撤销的 license_id hash
- 被撤销的 watermark_id hash
- 内测公告
- 更新链接
- 协议版本

**不存放**：有效激活码、用户信息、设备信息、私钥、签名 secret。

## 结构

```
public/
  v1/
    index.json + index.sig
    policy.json + policy.sig
    revoked/licenses.json + licenses.sig
    updates/latest.json + latest.sig
    legal/terms.json + terms.sig
    notices/notice.json + notice.sig
```

## 签名

所有 JSON 文件都有对应的 `.sig` 签名文件，客户端使用内置公钥验签后才使用。

## 部署

本仓库启用 GitHub Pages，从 `public/` 目录发布静态文件。

## 更新流程

使用 monolith 项目内的 `tools/beta-policy/` 签发工具更新策略文件：

```bash
cd tools/beta-policy
npm run sign          # 签名所有文件
npm run revoke -- ... # 管理撤销名单
```

然后将 `tools/beta-policy/public/` 内容复制到本仓库并推送。
