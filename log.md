# 开发进度与版本日志

记录本仓库的开发进度与 commit 版本。每次有实质进展或完成一次提交后更新本文件。

提交前须遵循 [commit.md](commit.md)：构建完成 → 测试通过 → 才能 `git commit`。

---

## Commit 版本

| Commit | 日期 | 说明 |
|--------|------|------|
| `8d67314` | 2026-09-27 | 开头增加回归 + Precision/Recall/F1 评估；指标测试通过后推送 |
| `edd1848` | 2026-09-27 | 在 log.md 记入首次提交 hash |
| `1798a0d` | 2026-09-27 | 首次提交：Tree ensemble XGBoost 复刻图 + SHAP interaction / explanation clustering；commit.md 测试通过后提交 |

**远程仓库：** https://github.com/lanjiangFSA/shap-tree-ensemble-xgboost

### 2026-09-27 — 开头增加模型评估指标章节

**状态：** 指标测试通过；已 commit `8d67314` 并 push。

**新增（训练之后、SHAP 之前）：**

- 训练/测试划分（`test_size=0.2`）
- 回归指标：R²、RMSE、MAE
- 按训练集房价中位数二值化后的 Accuracy / Precision / Recall / F1、混淆矩阵与 classification report


---

## 开发进度

### 2026-09-27 — Tree ensemble（XGBoost）示例初版

**状态：** 构建与测试已通过；尚未 commit。

**完成内容：**

1. 复刻 [shap/shap](https://github.com/shap/shap) README 中的 **Tree ensemble example (XGBoost)**，以及该节全部图。
2. 新增 [tree_ensemble_xgboost.ipynb](tree_ensemble_xgboost.ipynb)
   - 数据：`shap.datasets.california()`
   - 模型：`xgboost.XGBRegressor(random_state=0)`
   - 解释：`shap.Explainer`（兼容失败时回退 `TreeExplainer`）
   - 图：waterfall、单条 force（交互 + matplotlib）、前 500 条 force、Latitude scatter、beeswarm、bar
3. 新增 [requirements.txt](requirements.txt)：`shap`、`xgboost`、`matplotlib`、`pandas`、`numpy`、`scikit-learn`、`ipykernel`、`nbconvert`
4. 新增 [commit.md](commit.md)：规定 build 完成后必须测试，通过后才能 `git commit`
5. 按 `commit.md` 执行构建与验收
   - `pip install -r requirements.txt` 成功
   - `jupyter nbconvert --execute` 退出码 0（单格超时 600s）
   - notebook 无 `error` cell；6 张目标图均在输出中

**当前工作区文件：**

- `tree_ensemble_xgboost.ipynb`
- `requirements.txt`
- `commit.md`
- `log.md`（本文件）

**下一步（待确认）：**

- `git init`（如需要）
- 测试通过后按 `commit.md` 做首次 commit，并把 hash 记入上表

### 2026-09-27 — 导出加州房价数据副本

**状态：** 仅导出数据，不 commit。

**说明：**

- `shap.datasets.california()` 内部调用 `sklearn.datasets.fetch_california_housing()`
- sklearn 缓存文件：`C:\Users\alan_\scikit_learn_data\cal_housing_py3.pkz`
- 已导出可读 CSV 到 [data/california_housing.csv](data/california_housing.csv)（20640 行 × 9 列：8 特征 + `MedHouseVal`）
- 字段含义与单位见 [data/README.md](data/README.md)

### 2026-09-27 — 修复 notebook 本地运行环境

**状态：** 环境已配置；未 commit。

**问题：** 手动跑 cell 报 `ModuleNotFoundError: No module named 'xgboost'`，原因是内核指向了别的项目（如 `Multi-Agent` → `D:\P0712\2\.venv`），而不是装过依赖的解释器。

**处理：**

1. 新建本仓库专用 `.venv`，并 `pip install -r requirements.txt`
2. 注册 Jupyter 内核 `shap-xgboost`（显示名：`SHAP XGBoost (6. SHAP)`）
3. notebook metadata 改为使用该内核
4. 新增 `.vscode/settings.json`，默认解释器指向 `.venv`
5. 新增 `.gitignore`（忽略 `.venv/` 等）
6. 更新 [commit.md](commit.md) 的环境与构建命令

### 2026-09-27 — 增加 interaction / explanation clustering 章节

**状态：** 已 commit `1798a0d`，测试通过。

**新增：**

1. SHAP interaction values（前 2000 样本）：成对交互强度、热力图、Latitude×Longitude 与 MedInc×AveOccup dependence
2. Clustering by explanation similarity：KMeans on SHAP 向量、PCA 散点、簇平均 SHAP 剖面、分簇 beeswarm
