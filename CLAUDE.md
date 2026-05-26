# LP - AIエージェント向け指示

Prize Hunterアプリの公開ランディングページ（静的HTML/CSS、GitHub Pages）。

---

## 報告方法

```bash
tmux send-keys -t prize-hunter:all.0 '【受領】lp: 内容'; tmux send-keys -t prize-hunter:all.0 Enter
tmux send-keys -t prize-hunter:all.0 '【完了】lp: 結果'; tmux send-keys -t prize-hunter:all.0 Enter
```

---

## 技術スタック

- HTML5 / CSS3
- GitHub Pages（ホスティング）

---

## 開発コマンド

```bash
python -m http.server 8000
# http://localhost:8000
```

---

## コーディング規約

- セマンティックHTML
- モバイルファースト
- ARIA属性を適切に使用

---

## 禁止事項

- JavaScriptフレームワーク導入
- 不要な外部ライブラリ
- 個人情報フォーム（お問い合わせのみ可）

---

## 完了前チェック

@../docs/development/agent-definition-of-done.md

### lp 固有の最小検証

```bash
python -m http.server 8000
```

ブラウザで確認:
- `http://localhost:8000` — index.html が表示される
- 利用規約・プライバシーポリシーのリンクが動作する
- 変更したページ・セクションが意図通りに表示される
