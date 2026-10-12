# ER クイックリファレンス（ER_quickref）

ER 研修医向けの速攻参照型ツール。44 症候 × Killer/Common 鑑別 + 10 スコア計算機。

**作成**：鯨岡裕平（湘南台病院 救急科）
**用途**：教育用。臨床判断は必ず主治医・指導医と行うこと。

---

## ファイル構成

```
publish/
├── index.html            # メイン（PWA メタタグ入り）
├── manifest.json         # PWA 設定
├── service-worker.js     # オフラインキャッシュ
├── icon-192.png          # ホーム画面アイコン小
├── icon-512.png          # ホーム画面アイコン大
└── README.md             # これ
```

---

## GitHub Pages でデプロイ（15 分）

### Step 1：GitHub リポジトリ作成

1. [github.com](https://github.com) にログイン（アカウントなければ無料登録）
2. 右上「+」→「New repository」
3. 設定：
   - Repository name: `er-quickref`
   - Description: `ER クイックリファレンス（教育用）`
   - **Private** を選択（院内のみ公開なら）／ Public でも可
   - 「Add a README file」は **チェックしない**（既に用意済）
4.「Create repository」をクリック

### Step 2：ローカルから Git アップロード

Mac のターミナルで：

```bash
cd ~/Desktop/ERクイックリファレンス/publish/
git init
git add .
git commit -m "初版 v6"
git branch -M main
git remote add origin https://github.com/[USERNAME]/er-quickref.git
git push -u origin main
```

※ `[USERNAME]` は GitHub のユーザー名に置換

初回 push で GitHub の認証を求められたら、Personal Access Token を使用（パスワードは廃止済）：
1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2.「Generate new token」→ 名前と期限設定、`repo` にチェック →「Generate」
3. 表示されたトークンをコピー（二度と見られない）
4. push 時にパスワードの代わりに貼り付け

### Step 3：GitHub Pages 有効化

1. リポジトリページ →「Settings」
2. 左メニュー「Pages」
3. "Build and deployment"：
   - Source：**Deploy from a branch**
   - Branch：**main** / **(root)** → Save
4. 数分待つ → ページ上部に URL が表示される
   - 例：`https://[username].github.io/er-quickref/`

### Step 4：アクセス確認

- Chrome で URL を開く
- Chrome DevTools → Application → Manifest / Service Workers が認識されているか
- iPhone Safari で開く → 共有 → 「ホーム画面に追加」でアプリ化

---

## 更新手順

内容を変更したら：

```bash
cd ~/Desktop/ERクイックリファレンス/publish/
# ER_quickref.html を変更したら index.html に再コピー
cp ../ER_quickref.html index.html
# PWA メタタグとSW登録を再追加（下記参照）

git add .
git commit -m "v7：XXX を追加"
git push

# サービスワーカーも更新するため service-worker.js の CACHE_NAME を変更
# (例) const CACHE_NAME = 'er-quickref-v7';
```

**注意**：`ER_quickref.html` を更新した時は `index.html` にコピーし直す必要がある。かつ PWA 対応の `<head>` 追加・SW 登録スクリプトも再度追加する必要がある。

将来的には `index.html` 側で直接編集するか、ビルドスクリプトを作ると安全。

---

## iPhone での使い方（研修医向け 1 枚ガイド雛形）

1. iPhone Safari で `https://[username].github.io/er-quickref/` を開く
2. 画面下の「共有」アイコン（□↑）をタップ
3. 「ホーム画面に追加」を選択
4. アプリ名「ERquickref」で「追加」
5. ホーム画面にアイコン追加 → オフラインでも動作

---

## プライバシー・法的扱い

- データ送信・個人情報収集：**なし**（完全ローカル）
- 教育用ツール：臨床判断は主治医責任
- 医療機器該当性：非該当（診断支援でなく参照用）
- 著作権：鯨岡裕平、湘南台病院 救急科

---

## ライセンス

内部教育用。外部配布は要相談。
