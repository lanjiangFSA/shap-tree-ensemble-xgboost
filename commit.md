# 提交前测试流程

每次 build 完成后必须先测试。测试通过之后才允许 `git commit`。

测试失败、未跑测试、或 notebook 里仍有报错 cell 时，停止，不提交。

## 0. 环境（本仓库专用）

本项目使用根目录 `.venv`，不要用别的项目的内核（例如 `Multi-Agent` / `D:\P0712\2\.venv`）。

首次或换机时：

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m ipykernel install --user --name=shap-xgboost --display-name="SHAP XGBoost (6. SHAP)"
```

在 Cursor / VS Code 里打开 notebook 时：

1. 右上角 Kernel 选 **SHAP XGBoost (6. SHAP)**
2. 或确认解释器是 `D:\P0712\6. SHAP\.venv\Scripts\python.exe`（已写入 `.vscode/settings.json`）
3. 若刚换过内核：点 **Restart** 后再跑 cell

## 1. 构建

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=600 --ExecutePreprocessor.kernel_name=shap-xgboost tree_ensemble_xgboost.ipynb
```

构建以进程退出码 0 为准。加州房价数据首次加载需要联网。

## 2. 测试

构建成功后立刻检查已执行的 `tree_ensemble_xgboost.ipynb`，不能跳过：

- 没有任何 `output_type` 为 `error` 的 cell
- 输出里能找到官方 README 图：waterfall、单条 force（matplotlib）、Latitude scatter、beeswarm、bar
- 新增章节有输出：interaction 热力图、interaction dependence、explanation clustering PCA / 剖面图
- 单条 force 的 matplotlib 静态图也在输出里

## 3. 提交

只有第 1、2 步都通过，才可以 `git commit`。

- 提交信息说明这次改了什么、为什么改
- 不提交密钥、缓存、`.venv/`、或执行失败留下的半成品输出
