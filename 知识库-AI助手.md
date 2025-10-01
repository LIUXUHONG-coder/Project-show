# AI助手V1

一个基于 Flask 的轻量级知识库与 AI 助手管理系统。
<img width="2802" height="1478" alt="image" src="https://github.com/user-attachments/assets/470ac1e2-2db3-4833-90a4-06665ef270c0" />
<img width="2804" height="1458" alt="image" src="https://github.com/user-attachments/assets/fb93dbed-8b1b-4780-a055-f6df68d7bd4e" />
<img width="2804" height="1472" alt="image" src="https://github.com/user-attachments/assets/0e6069b9-f888-493d-a5b6-1d0dfa6aa38c" />

- 语言：Python 3.8+
- 框架：Flask
- 数据库：SQLite（`app.db`）

## 主要功能：
- 知识条目 CRUD、回收站管理
- 评论与点赞（含按天限制的点赞机制）
- 批量导入（TXT / DOCX / XLSX / XLS）与导出（XLSX / DOCX / TXT）
- 基于本地检索（BM25）实现的 RAG 检索与 AI 生成接口
- AI 建议（`ai_suggestions`）管理、评论与点赞
- 备份/恢复功能与备份历史记录

## 快速开始

1. 克隆或拷贝代码到本地：

   git clone <your-repo-url>

2. 建议使用虚拟环境（Windows PowerShell 示例）：

   python -m venv .venv
   .\.venv\Scripts\Activate.ps1

3. 安装依赖（没有 requirements.txt 时可按需安装）：

   pip install Flask requests python-docx openpyxl xlrd

4. 初始化数据库（只需执行一次）：

   python -c "from app import init_db; init_db()"

   （该命令会在当前目录生成或更新 `app.db`，并创建必要的表）

5. 启动服务：

   python app.py

   默认监听：`0.0.0.0:5001`（调试模式下）。访问 `http://localhost:5001/`。

## 配置说明

- 配置文件：`config.json`（用于保存回收站策略、备份设置、LLM 配置等）。
- LLM 集成：在 `config.json` 中填写 `llm.models`、`default_model` 等信息后，可通过 `/api/assistant/config` 管理和测试模型。

## 常见命令

- 运行一次性 DB 初始化（如果需要）：
  python -c "from app import init_db; init_db()"

- 导入数据（通过前端或 `/api/import` 接口上传文件）
- 导出数据：调用 `/api/knowledge/export` 接口

## 常见问题与排错

- 如果在推送到远程仓库时遇到 `error: src refspec main does not match any` 或 `Updates were rejected`：
  - 可能的原因：远程仓库已包含初始化提交（如 README），或远程有比你本地更新的提交。
  - 解决：
    - 先 fetch/merge：`git fetch origin && git merge origin/main` 或 `git pull --rebase origin main`
    - 如果本地没有提交，先 `git add . && git commit -m "Initial commit"`，再推送。
    - 如需强制覆盖远程（不推荐），使用：`git push --force-with-lease origin main`。

- 无法访问 GitHub（HTTPS 超时）：检查网络/代理/防火墙，或改用 SSH 推送（添加并使用 SSH key）。

## 注意事项

- 可选依赖：`python-docx`（docx 导入/导出）、`openpyxl`/`xlrd`（Excel 导入导出）。如果不安装，相关功能会提示不可用。
- 上传目录：`uploads/`（包含 `avatars`、`assets` 等），应用会在运行时自动创建。

## 贡献与扩展

欢迎按照常规 Git 工作流提交 PR，或在本地开发新模块（`modules/` 目录）后合并。

## 许可证

请根据需要添加许可证文件（如 `LICENSE`）。

---

如果你想我把 `README.md` 内容再精简或增加示例（例如 `config.json` 样例或常用 curl 请求示例），告诉我需要的部分，我会继续更新。

