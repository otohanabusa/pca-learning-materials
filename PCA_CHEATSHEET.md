# PCA 数式チートシート（短版）

## 🎯 最も重要な5つの式

### 1️⃣ 共分散行列
```
Σ = (1/(n-1)) × X_scaled^T × X_scaled

意味: 標準化したデータから分散・共分散を計算
```

### 2️⃣ 固有値・固有ベクトルの条件
```
Σ × v = λ × v

意味: 固有ベクトル v と固有値 λ は特別な関係を持つ
```

### 3️⃣ 主成分スコア（削減データ）
```
T = X_scaled × V_m

T: 変換後のデータ (n × m)
X_scaled: 標準化されたデータ (n × p)
V_m: 最初の m 個の固有ベクトル (p × m)

意味: 元のデータを新しい座標系（主成分）に投影
```

### 4️⃣ 分散説明率（寄与率）
```
分散説明率_k = λ_k / Σ(λ_i)

意味: k番目の主成分が全体の分散のどれだけを説明しているか
```

### 5️⃣ ローディング（寄与度）
```
L_{jk} = v_{jk} × √(λ_k)

L: ローディング行列 (p × m)
v: 固有ベクトル
λ: 固有値

意味: 各特徴が各主成分にどれだけ寄与しているか
```

---

## 💻 Pythonコード（最小限）

### 標準化と共分散行列

```python
from sklearn.preprocessing import StandardScaler
import numpy as np

# 標準化
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# 共分散行列
cov_matrix = np.cov(X_scaled.T)
```

### 固有値分解

```python
# 固有値・固有ベクトル
eigenvalues, eigenvectors = np.linalg.eigh(cov_matrix)

# ソート（大きい順）
idx = np.argsort(eigenvalues)[::-1]
eigenvalues = eigenvalues[idx]
eigenvectors = eigenvectors[:, idx]
```

### 主成分スコアとローディング

```python
# 2次元に削減
m = 2
V_m = eigenvectors[:, :m]
T = X_scaled @ V_m  # 主成分スコア

# ローディング
L = V_m * np.sqrt(eigenvalues[:m])
```

### 分散説明率

```python
# 分散説明率
explained_ratio = eigenvalues / eigenvalues.sum()

# 累積
cumulative_ratio = np.cumsum(explained_ratio)

print(f"PC1: {explained_ratio[0]:.2%}")
print(f"PC1-PC2: {cumulative_ratio[1]:.2%}")
```

### scikit-learnの簡潔な方法

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)
T = pca.fit_transform(X_scaled)

print(pca.explained_variance_ratio_)  # [0.7296, 0.2285]
print(pca.components_)  # ローディング（正規化版）
```

---

## ❓ よくある質問と回答

### Q1: 固有値と分散説明率の関係は？
```
固有値 = その主成分の分散

分散説明率 = 固有値 / 全固有値の和
         = その主成分の分散 / 全体の分散

大きい固有値 → 大きい分散説明率 → 重要な主成分
```

### Q2: ローディングとスコアの違い
```
スコア = T = X_scaled @ V
       → 各サンプルが主成分空間でどこに位置するか

ローディング = L = V × √λ
            → 各特徴が各主成分にどう寄与するか
```

### Q3: 何個の主成分を選ぶ？
```
方法1: 累積分散説明率で95%または90%に達するまで
方法2: Elbow Method で肘のポイントまで
方法3: スクリープロットで急に平坦になる地点まで

Iris(4次元)の場合: PC1-PC2 で 95.81% → 2次元でOK
```

### Q4: 情報損失の計算
```
情報損失率 = 1 - 累積分散説明率
          = (失われた固有値の和) / (全固有値の和)

Iris で 2次元削減:
損失 = 1 - 0.9581 = 4.19%
```

---

## 📐 Irisデータの結果

```
【固有値】
λ1 = 2.9381 → 分散説明率 72.96%
λ2 = 0.9202 → 分散説明率 22.85%
λ3 = 0.1477 → 分散説明率  3.67%
λ4 = 0.0209 → 分散説明率  0.52%
     ────────
      4.0269    100%

【ローディング】
特徴                     PC1      PC2
sepal length (cm)    -0.8932   0.3620
sepal width (cm)      0.4617   0.8857
petal length (cm)    -0.9949   0.0235
petal width (cm)     -0.9682   0.0642

【解釈】
PC1: sepal length, petal length/width が強く影響
     → 花の「大きさ」を表す

PC2: sepal width が強く影響
     → 花の「幅広さ」を表す
```

---

## 🎓 記号の意味確認

```
n : サンプル数
p : 元の特徴数
m : 削減後の次元数
X : 元のデータ (n × p)
X_scaled : 標準化されたデータ (n × p)
Σ : 共分散行列 (p × p)
λ_k : k番目の固有値（スカラー）
v_k : k番目の固有ベクトル（p次元ベクトル）
V_m : 最初のm個の固有ベクトル (p × m)
T : 主成分スコア (n × m)
L : ローディング行列 (p × m)
```

---

**最後に重要なこと**：
数式を理解することより、**データを標準化して、固有値分解して、主成分を取る**という流れを実践で身につけることが大切です！