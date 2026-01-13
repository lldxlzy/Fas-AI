# Fas-AI

一个本地运行的“课堂知识点思维导图”演示小工具。基于本地 Ollama（示例使用 Qwen 模型）生成 JSON 格式的思维导图并在浏览器中可视化。

主要文件
- index.html — 单页前端应用，包含 UI、绘图逻辑与 Ollama 调用逻辑
- LICENSE — 项目许可文件

特性
- 支持本地 Ollama（默认通过 http://localhost:11434 调用）
- 使用本地模型 `Qwen` 进行文本到思维导图 JSON 的生成
- 在画布上可视化思维导图，并支持导出 PNG / JSON

先决条件
- 已安装并运行 Ollama，启动命令（宿主机/容器中）:

	ollama serve

- Ollama 默认监听 `http://localhost:11434`，前端会调用 `/api/generate` 接口。

使用方法
1. 在浏览器中打开 [index.html](index.html)
2. 在侧栏填写：科目、知识点主题、课程内容、选择深度（2~4层）
3. 点击“生成思维导图”按钮，页面会向本地 Ollama 发送请求并解析返回的 JSON，然后绘制到画布上
4. 使用右侧按钮可导出 PNG 或 JSON

调试和常见问题
- 若提示 Ollama 未响应，请确保已运行：`ollama serve`，或通过命令测试：

	curl http://localhost:11434/api/tags

- 如遇 AI 返回非纯 JSON（含代码块），前端会尝试去除代码块并解析；若仍然解析失败，请在 Ollama 返回结果中检查格式

开发说明
- 前端在 `index.html` 中实现，核心点包含：
	- 配置项：`OLLAMA_API_URL`、`MODEL_NAME`
	- 生成流程：`buildPrompt()` → `callOllamaAPI()` → `parseAIResponse()` → `drawMindmap()`

许可证
- 见 `LICENSE` 文件

备注
- 这是一个轻量示例，便于在本地结合 Ollama 快速演示教学场景中的思维导图自动生成。欢迎补充 README 或扩展后端适配其它模型/服务。
