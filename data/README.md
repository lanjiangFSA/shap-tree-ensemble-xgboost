# California Housing 字段说明

本目录的 `california_housing.csv` 来自 scikit-learn 的
`sklearn.datasets.fetch_california_housing()`，也是
`shap.datasets.california()` 使用的同一份数据。

官方说明可通过 `fetch_california_housing().DESCR` 查看。

## 数据概况

| 项目 | 说明 |
|------|------|
| 行数 | 20640 |
| 粒度 | 每个 census **block group**（街区组）一行，不是单套房子 |
| 来源 | 1990 年美国人口普查 |
| 缺失值 | 无 |
| 原始出处 | Pace & Barry, *Sparse Spatial Autoregressions*, Statistics and Probability Letters, 33:291-297, 1997 |
| StatLib | https://lib.stat.cmu.edu/datasets/houses.zip |

一个 block group 是美国人口普查局发布抽样数据的最小地理单元，人口通常约 **600–3000** 人。

## 目标变量

| 列名 | 含义 | 单位 |
|------|------|------|
| `MedHouseVal` | 该街区组房价中位数 | **10 万美元**（`$100,000`）。例如 `4.526` ≈ **$452,600** |

## 特征（表头）

| 列名 | 含义 | 单位 / 说明 |
|------|------|-------------|
| `MedInc` | 街区组收入中位数 | **万美元量级**（`$10,000`）。例如 `8.3252` ≈ **$83,252** |
| `HouseAge` | 街区组房屋年龄中位数 | **年** |
| `AveRooms` | 每户平均房间数 | 房间数 / 户 |
| `AveBedrms` | 每户平均卧室数 | 卧室数 / 户 |
| `Population` | 街区组人口 | **人** |
| `AveOccup` | 每户平均居住人数 | 人 / 户 |
| `Latitude` | 纬度 | 度 |
| `Longitude` | 经度 | 度 |

## 注意

- **household（户）**：住在同一住所里的一组人。
- `AveRooms` / `AveBedrms` 有时会特别大：度假区等「户很少、空房很多」的街区组会被拉高。
- CSV 由本仓库从 sklearn 缓存导出，便于直接查看；notebook 仍可通过 `shap.datasets.california()` 加载。
