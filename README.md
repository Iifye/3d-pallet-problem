# 3D Pallet Problem

## 簡介
這是一個關於三維托盤擺放問題的數學模型，旨在最小化使用托盤數量，同時滿足訂單需求。

## 文件結構
- `model/`: 包含模型代碼
- `.gitignore`: 忽略不必要的文件
- `LICENSE`: MIT License

## 模型說明
### 集合定義
- **O**: 訂單集合
- **M**: 料號集合
- **S**: 使用托盤集合
- **R**: 組托規則碼集合
- **L, W, H**: 托盤長、寬、高的集合

### 參數定義
- **mb**: 每個料號的袋數
- **Box**: 一個理貨箱的最大容量
- **Dom**: 訂單 o 中料號 m 的需求量
- **r**: 組托規則碼
- **V**: 托盤容量
- **rf**: 是否使用平碼規則碼垛
- **mixr**: 是否使用混合料號碼垛
- **maxr**: 混托限制量

### 決策變數
- **xijks**: 若料號 m 被擺放在托盤 s 的座標 (i, j, k) 上，則為 1，否則為 0
- **Us**: 若托盤 s 被使用，則為 1，否則為 0
- **Cs**: 若托盤 s 上有存在料號 m，則為 1，否則為 0

### 目標函數
- 最小化使用托盤的總數量: Min Z = ∑ Us

### 約束條件
- 托盤容量限制: ∑ xijks ≤ V, ∀s ∈ S
- 每個托盤上是否有料號 m: xijks ≤ Cs, ∀m ∈ M, s ∈ S, i, j, k
- 每個托盤上不同料號 m 的數量限制: ∑ Cs ≤ maxr, ∀s ∈ S
- 平碼規則：∑ xijks + (1 - rf) ≥ ∑ xi+1jks, ∀m ∈ M, s ∈ S, i, j, k
- 平碼規則：∑ xijks + rf ≥ ∑ xij+1ks, ∀m ∈ M, s ∈ S, i, j, k

## 使用說明
### 安裝和運行
1. 克隆儲存庫：
    ```sh
    git clone https://github.com/Iifye/3d-pallet-problem.git
    cd 3d-pallet-problem
    ```
2. 安裝所需的依賴包：
    ```sh
    pip install -r requirements.txt
    ```
3. 運行模型：
    ```sh
    python model/model.py
    ```

## 貢獻
歡迎提出問題和拉取請求。詳細請參見[貢獻指南](CONTRIBUTING.md)。

## 許可證
本項目基於MIT License，詳細請參見[LICENSE](LICENSE)文件。
