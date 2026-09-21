# 雨课堂自动答题 · Safari Userscripts

一个面向 Safari Userscripts 的雨课堂辅助脚本：识别当前课堂习题，调用 DeepSeek 生成答案，并自动填写、提交。

> 请仅在获得课程与教师明确许可的场景使用，并自行核对生成结果。模型可能出错，使用 API 会产生费用。

![脚本在 iPhone Safari / WebKit 中的运行界面](assets/panel-preview.png)

## 功能

- 自动识别单选、多选与填空题
- 支持题目图片，并将图片一并发送给支持视觉的模型
- 可配置题目、选项、填空框和提交按钮的 CSS 选择器
- 支持暂停、立即检测、API 连通性测试与最近 300 条运行日志
- 悬浮窗可拖动、收起；收起后以触发位置为中心显示 Gemini 风格星标
- 针对 iPhone/iPad 缺少 viewport meta、缩放和安全区做了适配

## 安装

1. 在 iPhone、iPad 或 Mac 的 **Safari** 安装并启用 Userscripts 扩展。
2. 下载 [yuketang-autopilot.safari.user.js](yuketang-autopilot.safari.user.js)，并在 Userscripts 中导入或保存它。
3. 在 Safari 打开 `https://www.yuketang.cn/`，从扩展菜单启用 Userscripts。
4. 在右上角悬浮窗打开“API 与页面设置”，填写 DeepSeek API Key，保存后按需开启自动答题。

Userscripts 只能运行在 Safari 网页中，不能注入雨课堂原生 App。

## 使用说明

- 第一次使用先保持“暂停”状态，打开一题后点击“立即检测”，确认页面识别与答案输出符合预期。
- 默认模型为 `deepseek-flash`；图片题需要使用支持视觉输入的模型。
- 如果某个课程页面的结构特殊，在“高级：页面选择器”中填写对应的 CSS 选择器。
- 点击“收起”后，圆形星标会停在手指点击位置；拖动星标可移动悬浮窗。

## 隐私与费用

- API Key 保存在 Userscripts 的本地存储中。
- 启用后，题干、选项和题目图片会发送到 `api.deepseek.com`，用于生成答案。
- 请求按 DeepSeek 的账户用量计费；请在使用前确认账户余额与模型价格。

## 验证

```bash
PLAYWRIGHT_BROWSERS_PATH="$PWD/.tmp-harness/browsers" node tests/mobile-panel.test.mjs --engine=webkit
node tests/mobile-panel.test.mjs --engine=chromium
```

回归测试覆盖悬浮窗的加载、缩放、拖动、收起/展开、触摸与鼠标交互。

## 文件

- `yuketang-autopilot.safari.user.js`：Userscripts 脚本
- `tests/mobile-panel.test.mjs`：移动端悬浮窗回归测试
- `assets/panel-preview.png`：WebKit 中加载脚本生成的运行界面截图

## 免责声明

本项目仅供学习与自动化测试用途。使用者应遵守所在机构的学术诚信规范、课程规定和相关法律，并对自己的使用行为负责。
