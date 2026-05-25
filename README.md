# PCA（主成分分析）学習教材

主成分分析（Principal Component Analysis）の学習用教材です。データセット、問題集、解答例を含みます。

## 📁 ファイル構成

```
PCA Learning Materials/
├── README.md                      # このファイル
├── PCA_FORMULAS.md               # 詳細な数学公式
├── PCA_CHEATSHEET.md             # 要点集（短版）
├── pca_dataset.py                # データセット生成スクリプト
├── pca_problems.py               # 問題集（★～★★★）
├── pca_solutions.py              # サンプル解答例
├── pca_formula_examples.py       # 計算例（7例）
├── datasets/                     # 学習データ
│   ├── student_scores.csv       # 学生成績データ（150×5）
│   ├── customer_data.csv        # 顧客データ（200×5）
│   ├── sensor_data.csv          # センサーデータ（200×5）
│   └── iris_data.csv            # Irisデータ（150×4+label）
└── outputs/                      # グラフ出力
    ├── problem_1_solution.png
    ├── problem_2_solution.png
    ├── problem_4_solution.png
    ├── problem_6_solution.png
    ├── formulas_example_scree.png
    └── formulas_example_loading.png
```

## 🚀 クイックスタート

### 1. 環境構築

```bash
pip3 install numpy pandas scikit-learn matplotlib scipy
```

### 2. データセットの生成

```bash
python3 pca_dataset.py
```

### 3. 問題集を表示

```bash
python3 pca_problems.py
```

### 4. 解答例を実行

```bash
python3 pca_solutions.py
```

### 5. 計算例を実行

```bash
python3 pca_formula_examples.py
```

## 📚 学習コンテンツ

### ファイル説明

| ファイル | 説明 | サイズ |
|---------|------|--------|
| README.md | 全体ガイド | 8.3KB |
| PCA_FORMULAS.md | 詳細な数学式 | 13KB |
| PCA_CHEATSHEET.md | 要点まとめ | 6.5KB |
| pca_dataset.py | 4種類のデータセット生成 | - |
| pca_problems.py | 8問の問題集 | - |
| pca_solutions.py | 4問のサンプル解答 | - |
| pca_formula_examples.py | 7つの計算例 | - |

### 問題集（8問）

**★ 基礎問題**
1. PCAの基本
2. 相関行列と固有値

**★★ 中級問題**
3. 可視化と解釈
4. 最適な主成分数の決定
5. 時系列データの次元削減

**★★★ 上級問題**
6. PCAの手動実装
7. 外れ値検出
8. クラスタリングとの組み合わせ

## 📐 主要な式

### 共分散行列
$$\Sigma = \frac{1}{n-1} X_{std}^T X_{std}$$

### 分散説明率（寄与率）
$$\text{Explained Variance Ratio}_k = \frac{\lambda_k}{\sum_{i=1}^{p} \lambda_i}$$

### 主成分スコア
$$T = X_{std} \cdot V_m$$

### ローディング（寄与度）
$$L_{jk} = v_{jk} \sqrt{\lambda_k}$$

## 💡 Pythonコード（最小例）

```python
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
import numpy as np

# 標準化
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# PCA実行
pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)

# 分散説明率
print(pca.explained_variance_ratio_)  # [0.7296, 0.2285]
print(np.cumsum(pca.explained_variance_ratio_))  # [0.7296, 0.9581]
```

## 📊 実行結果サンプル（Irisデータ）

```
【分散説明率】
PC1: 72.96%
PC2: 22.85%
累積: 95.81%

【ローディング】
                    PC1      PC2
sepal length     -0.8932   0.3620
sepal width       0.4617   0.8857
petal length     -0.9949   0.0235
petal width      -0.9682   0.0642
```

## 🎓 学習ロードマップ

1. **基礎理解** → README.md と PCA_CHEATSHEET.md を読む
2. **詳細学習** → PCA_FORMULAS.md で全ての式を理解
3. **実装練習** → pca_problems.py で8問を解く
4. **検証学習** → pca_formula_examples.py で計算を追跡
5. **応用実践** → 自分のデータで実装

## ✨ 主な特徴

- ✓ 理論と実装の並行学習設計
- ✓ 3つのレベルの資料（詳細版、短版、実装版）
- ✓ 8問の実践的な問題集
- ✓ 4つの異なるデータセット
- ✓ 7つの計算例（ステップバイステップ）
- ✓ 手動実装 vs scikit-learn の比較検証
- ✓ グラフを使った可視化
- ✓ よくある質問Q&A付き

## 📚 参考資料

- [Scikit-learn PCA Documentation](https://scikit-learn.org/stable/modules/decomposition.html#pca)
- [Wikipedia: Principal Component Analysis](https://en.wikipedia.org/wiki/Principal_component_analysis)

## 📧 使用ライブラリ

- NumPy: 数値計算
- Pandas: データ処理
- Scikit-learn: 機械学習
- Matplotlib: 可視化
- SciPy: 統計計算

---

**作成日**: 2026年5月25日  
**最終更新**: 2026年5月25日