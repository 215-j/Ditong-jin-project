# 🐱🐶 猫狗分类器 · Web 版

基于 ResNet18 迁移学习训练的猫狗图像二分类器,模型已转为 ONNX 格式,在前端浏览器里用 onnxruntime-web 推理,**无需服务器,纯静态部署**。

## 在线访问

部署到 GitHub Pages 后,访问:

```
https://<你的GitHub用户名>.github.io/Ditong-jin-project/
```

## 功能

- 📷 浏览器摄像头实时拍照识别
- 📁 本地图片上传识别
- 📊 类别 + 置信度 + 概率条可视化
- 🚀 100% 纯前端推理,无需后端服务器

## 部署步骤

### 1. 创建 GitHub 仓库

1. 登录 GitHub,点右上角 `+` → **New repository**
2. Repository name 填 `Ditong-jin-project`
3. 选择 **Public**(否则 Pages 在免费账户不可用)
4. 勾选 "Add a README file"
5. 点击 **Create repository**

### 2. 上传文件

把 `deploy/` 目录下的所有文件拖到 GitHub 网页的 "Add file → Upload files" 上传:

- `index.html`(主页面)
- `best_model.onnx`(模型,~42MB,因 GitHub 单文件 < 100MB 限制可直接上传)
- `banner.jpg`(顶部图片)
- `.gitignore`(可选)
- `README.md`(覆盖默认)

**注意**:`best_model.onnx` 是 42MB,网页上传可能慢,请耐心等待。

### 3. 启用 GitHub Pages

1. 进入仓库 → **Settings** → 左侧 **Pages**
2. Source 选 **Deploy from a branch**
3. Branch 选 **main** / 文件夹选 **/(root)**
4. 点击 **Save**
5. 等待 1-2 分钟,页面顶部会显示:
   ```
   Your site is live at https://<用户名>.github.io/Ditong-jin-project/
   ```

### 4. 访问

打开上面那个链接,即可使用猫狗分类器!

## 本地预览

```bash
cd deploy
# 用 Python 自带 http.server 启动
py -m http.server 8000
# 浏览器打开 http://localhost:8000/
```

## 模型信息

- 架构:ResNet18(ImageNet 预训练 + 冻结 backbone + 微调 fc 头)
- 输入:1×3×224×224 RGB,ImageNet 归一化
- 输出:2 维 logits(cat, dog)
- 训练数据:猫狗数据集 100 张(80 训练 + 20 验证)
- 验证准确率:约 90%
- ONNX 算子集:opset 13,与 onnxruntime-web 1.19 兼容

## 技术栈

- 前端:纯 HTML/CSS/JS(无框架)
- 推理:[onnxruntime-web 1.19.2](https://cdn.jsdelivr.net/npm/onnxruntime-web@1.19.2/dist/ort.min.js)
- 部署:GitHub Pages(免费静态托管)

## 浏览器兼容性

- Chrome / Edge / Firefox 现代版本 ✅
- 摄像头 API 在 https 或 localhost 下才可用
- GitHub Pages 是 https,所以拍照功能可用

## 仓库结构

```
deploy/
├── index.html         ← 主页面
├── best_model.onnx    ← ONNX 模型 (42 MB)
├── banner.jpg         ← 顶部图片
├── README.md          ← 本文件
└── .gitignore
```

## 许可

仅供学习交流使用。模型权重基于 ImageNet 预训练 + 自采集猫狗数据集微调。
