# PrizeHunter Landing Page

PrizeHunter アプリの静的ランディングページです。

## 構成

- `index.html` - ランディングページ
- `terms.html` - 利用規約
- `privacy.html` - プライバシーポリシー
- `styles.css` - スタイルシート

## GitHub Pages での公開

1. リポジトリの Settings > Pages に移動
2. Source で「Deploy from a branch」を選択
3. Branch で「main」と「/ (root)」を選択
4. Save をクリック

数分後に `https://<username>.github.io/prize-hunter-lp/` で公開されます。

## ローカルでの確認

```bash
# Python 3
python -m http.server 8000

# または npx
npx serve
```

ブラウザで `http://localhost:8000` を開いて確認できます。
