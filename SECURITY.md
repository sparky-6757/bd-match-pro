# Security Policy · 安全策略

## Scope · 范围

BD Match Pro is a single-file static web app — no backend, no user data collection, no authentication. The threat surface is limited, but we still take security reports seriously.

BD Match Pro 是单文件静态网页应用——无后端、不收集用户数据、无认证。安全攻击面有限，但我们仍认真对待安全报告。

## Reporting a vulnerability · 报告漏洞

**Please do not open a public Issue for security vulnerabilities.**

**请不要通过公开 Issue 报告安全漏洞。**

Instead, please report privately via one of:

请改用以下方式之一私下报告：

- 🔒 GitHub Security Advisories: [Report a vulnerability](https://github.com/sparky-6757/bd-match-pro/security/advisories/new)
- 📧 Direct contact: see [README · Contact](README.md#contact)

We will respond within **5 business days** and aim to ship a fix or mitigation within **30 days** of confirmed reports.

我们将在 **5 个工作日**内回复，并力争在确认漏洞后 **30 天**内发布修复或缓解措施。

## Scope of "security" · 何为安全问题

In scope:
- XSS or content-injection vulnerabilities in the live app
- Supply-chain risks via the few CDN-loaded fonts/scripts
- Misleading methodology that could materially harm a user's decision (please file as a methodology Issue, not a security report)

Out of scope:
- Outputs being "wrong" or imprecise — outputs are research-grade estimates by design (see [DISCLAIMER](DISCLAIMER.md))
- Issues affecting only your local fork's modifications

属于安全范畴：
- 在线应用中的 XSS 或内容注入漏洞
- 通过 CDN 加载的字体/脚本可能带来的供应链风险

不属于安全范畴：
- 输出"不准"或精度不足——本应用输出本就是研究级估算（见 [DISCLAIMER](DISCLAIMER.md)）
- 仅影响你本地 fork 后修改版本的问题

---

Thank you for helping keep BD Match Pro safe for everyone.
感谢协助维护 BD Match Pro 的安全。
