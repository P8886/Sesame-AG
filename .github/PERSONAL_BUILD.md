# 自用 APK 构建

进入本仓库 **Actions → 自用 APK 构建 → Run workflow**，工作流分支选择 `main`，源码默认选择 `dev`。也可以填写 `4380-0.2.6` 等已有版本标签。

构建成功后，在该次运行页面的 **Artifacts** 下载 APK 压缩包，无需解压密码。一加手机使用 `app-arm64-v8a-release-personal.apk`，通用包为 `app-universal-release-personal.apk`。

## 更新源码

在 GitHub 切换到 `dev` 分支，再选择 **Sync fork → Update branch**。更新后重新运行自用构建。本工作流单独保存在 `main`，`dev` 保留上游源码。

## 签名与安装

APK 使用本仓库固定的个人签名，不设置官方签名标识。首次替换官方包时签名不同，通常不能覆盖安装，需要先备份账号配置再更换；后续个人构建可使用同一签名更新。

签名配置位于仓库 **Settings → Secrets and variables → Actions**：

- Secret `PERSONAL_SIGNING_KEY`：Base64 编码的 PKCS12 密钥库。
- Secret `PERSONAL_KEYSTORE_PASSWORD`：密钥库和密钥密码。
- Variable `PERSONAL_SIGNING_CERT_SHA256`：个人证书 SHA-256 指纹，大写、无冒号。

密钥别名为 `sesame-personal`。后续构建应保留同一份密钥。工作流保持上游业务代码和账号槽位上限。
