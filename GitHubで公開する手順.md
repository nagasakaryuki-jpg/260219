# GitHub で「旅のしおり」を公開する手順

GitHub アカウントは作成済みの前提です。**Cursor のターミナル**で進められます。

---

## 事前にやること（ブラウザで1回だけ）

### 1. GitHub で新しいリポジトリを作る

1. ブラウザで **https://github.com** にログイン
2. 右上の **「+」→「New repository」**
3. 次のように入力：
   - **Repository name**: 例）`momoko-birthday` や `travel-guide`（何でもOK）
   - **Public** を選択
   - **「Add a README file」はチェックしない**（中身は Cursor から上げるため）
4. **「Create repository」** をクリック
5. 作成後、表示される **リポジトリのURL** をコピー  
   例：`https://github.com/あなたのユーザー名/momoko-birthday.git`

ここまでできたら、次の「Cursor でやること」に進みます。

---

## Cursor でやること

### 2. プロジェクトフォルダを Git の管理下にする

Cursor で **ターミナル** を開く（`` Ctrl+` `` または メニュー「表示」→「ターミナル」）。

**重要：** ターミナルの現在のフォルダが **`wife-birthday-trip` の中** になっているか確認してください。  
違う場合は次のコマンドで移動します。

```powershell
cd "c:\Users\nagas\.cursor\projects\openclawインストール\wife-birthday-trip"
```

続けて、以下を **1つずつ** 実行します。

```powershell
# このフォルダを Git で管理開始
git init

# すべてのファイルを追加
git add .

# 初回の保存（コミット）
git commit -m "旅のしおりを追加"
```

- 初回で `git config user.name` / `user.email` を聞かれたら、GitHub に登録した名前とメールを設定してください。
- `git add .` で「依頼内容まとめ.md」や「GitHubで公開する手順.md」も一緒に上がります。**リポジトリに含めたくないファイル**がある場合は、先に `.gitignore` で除外するか、`git add 旅のしおり.html` のようにファイル指定で追加してください。

---

### 3. GitHub のリポジトリとつなげて push する

次の **1行目** は、さきほどコピーしたリポジトリURLに置き換えてください。

- あなたのユーザー名が `nagasaka` で、リポジトリ名が `momoko-birthday` なら：  
  `https://github.com/nagasaka/momoko-birthday.git`

```powershell
# リモートを追加（URL はあなたのリポジトリに合わせて変更）
git remote add origin https://github.com/あなたのユーザー名/リポジトリ名.git

# メインブランチの名前を main にする（既に main の場合は不要なこともあります）
git branch -M main

# GitHub に送る（初回はログインを求められます）
git push -u origin main
```

- **認証**：`git push` で「Username」「Password」を聞かれた場合：
  - **Password** には、GitHub の「パスワード」ではなく **Personal Access Token (PAT)** を使います。
  - PAT の作り方：GitHub → 右上のアイコン → **Settings** → 左の **Developer settings** → **Personal access tokens** → **Tokens (classic)** → **Generate new token** で、権限に `repo` にチェックを入れて発行し、表示されたトークンをコピーしてパスワード欄に貼り付けます。
- Windows では、初回 push 時にブラウザが開いて GitHub ログインで認証できる場合もあります（Git Credential Manager を使っている場合）。

ここまで成功すると、GitHub のリポジトリにファイルが反映されています。

---

## 4. GitHub Pages で Web ページとして公開する（任意）

「旅のしおり」を **URL 1つで見られるようにする** 手順です。

1. GitHub でそのリポジトリのページを開く
2. 上部メニューの **「Settings」**
3. 左の **「Pages」**
4. **Source** で **「Deploy from a branch」** を選ぶ
5. **Branch** で **「main」**、フォルダは **「/ (root)」** を選んで **Save**
6. 数分待つと、次のような URL で表示されます：  
   `https://あなたのユーザー名.github.io/リポジトリ名/`

**注意：**  
- トップ（`/`）で開いたときに表示されるのは **`index.html`** です。  
- いまのファイル名は **`旅のしおり.html`** なので、そのままなら  
  `https://あなたのユーザー名.github.io/リポジトリ名/旅のしおり.html`  
  で開く必要があります。
- **トップでいきなり「旅のしおり」を表示したい**場合は、`旅のしおり.html` を **`index.html`** にコピー（またはリネーム）して、そのファイルをコミット・push してください。

---

## 5. 今後、内容を直したときの更新のしかた

HTML やメモを直したあと、同じフォルダで：

```powershell
git add .
git commit -m "文言を更新"
git push
```

で GitHub が更新されます。GitHub Pages も自動で数分以内に反映されます。

---

## まとめチェックリスト

- [ ] GitHub で新しいリポジトリ（空でOK）を作成した
- [ ] Cursor のターミナルで `wife-birthday-trip` に移動した
- [ ] `git init` → `git add .` → `git commit -m "旅のしおりを追加"` を実行した
- [ ] `git remote add origin ...` で自分のリポジトリURLを設定した
- [ ] `git push -u origin main` で GitHub に送った（認証は PAT またはブラウザ）
- [ ] （任意）Settings → Pages で GitHub Pages を有効にした
- [ ] （任意）トップで開きたい場合は `index.html` を用意した

不明なステップがあれば、どこで止まっているか（例：何を実行したか、画面に何と出たか）を教えてもらえれば、そこだけ詳しく書けます。
