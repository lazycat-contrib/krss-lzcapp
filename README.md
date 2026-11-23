# krss-lzcapp

Krss 自托管 RSS 阅读器的懒猫微服打包仓库。镜像模式：直接引用上游官方多架构镜像 `ghcr.io/kue02/krss`，通过内置 GHCR 加速器拉取。

## 版本跟踪说明

上游 tag 混合 3 段（`1.1.9`）与 4 段热修复（`1.1.9.1`）两种形状：

- 自动化只跟踪 **3 段 release**（`tag_regex: '^[0-9]+\.[0-9]+\.[0-9]+$'`）。4 段 tag 不是合法 SemVer，Action 会自动过滤；已穷举正则映射方案，均无法把 4 段保序折叠进 3 段版本空间，故放弃跟踪热修复 tag。
- `exclude_regex: '^1\.2\.0$'` 排除 GHCR 上的陈旧 tag `1.2.0`（2026-10-09 从未发版的 main 提交快照，版本号高于所有 release 但内容过旧，若不过滤会被误选）。
- 上游发 1.1.10 / 1.2.0 等新 release 时自动跟进；4 段热修复（如未来的 1.1.9.2）需等下一个 3 段正式版。

## 结构

- `package.yml`：包元数据
- `lzc-manifest.yml`：运行结构（端口 8090，数据挂 `/lzcapp/var/data` → `/app/data`）
- `.github/lazycat-action.yml` + `.github/workflows/lazycat.yml`：镜像模式自动化发布

上游：[kue02/Krss](https://github.com/kue02/Krss)（GPL-2.0）
