# Vibe Coding 上线前安全检测清单

> 让“AI 帮我做了一个能跑的产品”，再向前走一步：上线前先问对 100 个安全问题。

这是一个面向 **vibe coding / Web coding / AI 生成应用** 的上线前安全检查项目。它不是给安全专家看的论文，而是给完全不懂代码的产品负责人、独立开发者、运营人员和创始人用的“上线前刹车系统”。

当一个 MVP 从本地 Demo 走向真实用户，风险会突然变成现实：

- 短信验证码可能被刷爆账单
- UGC 评论、头像、昵称可能引发内容事故
- 支付金额可能被前端篡改
- 普通用户可能通过改 ID 看见别人的数据
- AI 助手可能吐出系统提示词、内部规则或敏感上下文
- 后台可能没有 MFA、没有角色权限、没有操作日志
- 数据库可能没有备份，或者有备份但从未恢复过

这个项目的目标很直接：**帮助 vibe coding 项目在上线前完成最基础、最全面、最可执行的安全自查。**

## 项目亮点

- **20 个安全维度，100 个检查项**  
  覆盖账号登录、权限、输入、Web、App、小程序、AI、UGC、支付、隐私、云服务、备份、API、后台、监控、发布、法务、应急、供应链和用户体验安全边界。

- **专为非技术人员设计**  
  每个检查项都包含“非技术检查方法”和“要问开发/AI 的问题”，不用懂代码也能推动上线评审。

- **围绕 vibe coding 真实风险**  
  不只讲传统漏洞，也覆盖 AI 陪聊、提示词泄露、短信成本、UGC 内容治理、云账单、后台运营、支付回调和发布回滚。

- **AI 可读取、可复用**  
  核心数据在 [`data/checklist.json`](data/checklist.json)，页面可复制当前筛选 JSON、Markdown 摘要和 AI 审查提示词，方便交给 ChatGPT、Codex、Claude 审查具体项目。

- **静态网页，打开即用**  
  无需后端。可直接部署到 GitHub Pages、Vercel、Netlify 或任意静态托管。

## 在线体验

如果启用 GitHub Pages，入口是：

```text
https://<your-github-username>.github.io/<repo-name>/
```

本地查看：

```bash
npm run build
npm run serve
```

然后打开终端输出的本地地址。

## 清单适用对象

这个项目适合：

- 用 AI / Cursor / Claude / Codex / Bolt / Lovable / v0 做 MVP 的独立开发者
- 想把 Demo 公开给真实用户的非技术创始人
- 正在做粉丝社区、AI 陪聊、内容平台、工具站、小程序或 App 的团队
- 没有安全工程师，但需要一个上线前基础安全门槛的项目负责人
- 想让 AI 帮忙 review 自己项目上线风险的人

## 不是攻击教程

本项目避免提供可直接用于攻击的细节。清单只保留产品负责人识别风险所需的信息：

- 这个问题为什么危险
- 普通人怎么做基础检查
- 应该问开发或 AI 什么
- 行业里通常怎么修
- 哪些信号意味着不能上线

## 数据结构

每个检查项包含：

```json
{
  "id": "auth-001",
  "category_id": "auth",
  "priority": "P0",
  "severity": "high",
  "title": "弱密码与撞库",
  "risk": "用户账号或后台账号被批量尝试登录...",
  "nontechnical_check": "用常见弱密码注册或登录测试...",
  "ask_dev_or_ai": "登录失败是否按账号、IP、设备限速？",
  "best_practice": "密码加盐哈希，登录失败限速...",
  "red_flags": ["输错密码无限尝试"],
  "tags": ["login", "password", "mfa"]
}
```

优先级定义：

- `P0`：上线前必须处理
- `P1`：上线前应处理，或必须有明确补偿控制
- `P2`：上线后短期治理，但不能长期忽略

## 用 AI 审查你的项目

网页里可以直接点击 **复制 AI 审查提示词**。也可以手动使用下面的模板：

```text
你是一名资深应用安全与产品风险审查顾问。请基于 data/checklist.json，审查这个 vibe coding MVP 项目。

产品信息：
- 产品名称：
- 产品网址或代码仓库：
- 产品类型：
- 目标用户：
- 当前阶段：
- 审查目标：

审查要求：
1. 不要泛泛评价，必须基于可观察证据。
2. 每个发现输出：问题、证据、影响、建议、优先级、关联 checklist item id、置信度。
3. 如果信息不足，列出需要补充的证据，不要假设已经安全。
4. 优先指出 P0 和会导致数据泄露、资金损失、内容事故、云费用失控、后台接管的问题。
5. 如果审查代码仓库，请先找真实用户路径、后端 API、后台、配置和第三方服务，不要只看 UI。
```

## 项目结构

```text
.
├── index.html                  # 静态网页应用
├── data/
│   └── checklist.json           # AI 可读安全清单数据
├── scripts/
│   └── generate-checklist.mjs    # 生成清单数据
├── package.json
├── LICENSE
└── README.md
```

## 开发

```bash
npm run build
npm run validate
npm run serve
```

## 参考基线

清单内容参考并面向 MVP 场景重写：

- [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/)
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [OWASP Top 10](https://owasp.org/Top10/2021/)
- [OWASP API Security Top 10](https://owasp.org/API-Security/editions/2023/en/0x00-header/)
- [OWASP File Upload Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html)
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [NIST SP 800-63B](https://pages.nist.gov/800-63-4/sp800-63b.html)
- [CISA Secure by Design](https://www.cisa.gov/securebydesign)

## License

MIT
