# LP - AIエージェント向け指示

> ランディングページ（静的HTML/CSS）

## 📋 報告方法（最重要）

```bash
tmux send-keys -t prize-hunter:all.0 '【受領】lp: 内容'; tmux send-keys -t prize-hunter:all.0 Enter
tmux send-keys -t prize-hunter:all.0 '【完了】lp: 結果'; tmux send-keys -t prize-hunter:all.0 Enter
```

---

## 🎯 リポジトリの役割

Prize Hunterアプリの公開ランディングページ。利用規約・プライバシーポリシー・お問い合わせフォーム掲載。

---

## 🛠️ 技術スタック

- **HTML5**
- **CSS3**
- **GitHub Pages**: ホスティング

---

## 🔧 開発コマンド

```bash
python -m http.server 8000
# http://localhost:8000
```

---

## 📝 コーディング規約

- **セマンティックHTML**: 適切なタグ使用
- **レスポンシブ**: モバイルファースト
- **アクセシビリティ**: ARIA属性適切使用

---

## 🚫 禁止事項

- ❌ JavaScriptフレームワーク導入
- ❌ 不要な外部ライブラリ
- ❌ 個人情報フォーム（お問い合わせのみ）

---

## ✅ 完了前チェック（必須）

### 最小検証コマンド

```bash
python -m http.server 8000
```

起動後、ブラウザで以下を目視確認する:

1. `http://localhost:8000` — index.html が正しく表示される
2. 主要リンクが動作する:
   - 利用規約ページ
   - プライバシーポリシーページ
3. 変更したページ・セクションが意図通りに表示される

### 完了報告フォーマット

```
【完了】lp: <実施内容の1行要約>

検証結果:
- python -m http.server 8000 起動: ✅ PASS / ❌ FAIL
- index.html 表示: ✅ PASS / ❌ FAIL
- 利用規約リンク: ✅ PASS / ❌ FAIL
- プライバシーポリシーリンク: ✅ PASS / ❌ FAIL

未実行チェック:（該当なし or スキップ理由を記載）
- <項目>: スキップ理由

変更ファイル:
- <ファイルパス>: <変更内容1行>
```

### 記載ルール

1. **検証結果は必ず書く** — スキップした場合も「未実行チェック」に理由を明記する
2. **PASS/FAIL を明示する** — 「おそらく動く」は PASS ではない。実際に確認する
3. **FAIL が出たら止める** — 修正して再確認してから報告する
4. **変更ファイルは省略しない** — 全変更ファイルを列挙する

> 詳細ルール: [prize-hunter/docs/development/agent-definition-of-done.md](../docs/development/agent-definition-of-done.md)

---

## 📝 変更履歴の記録（重要・必須）

**重要**: タスク完了時は必ず変更履歴を記録すること

完了報告と同時に、オーケストレーターに以下を依頼:

```
【完了】lp: [実施内容]

変更履歴記録依頼:
- /docs/CHANGELOG.md への追記
```

**記録すべき変更**: 新ページ追加、デザイン大幅変更、利用規約・プライバシーポリシー更新

---

## 🔗 関連ドキュメント

- [docs/setup.md](./docs/setup.md)
- [README.md](./README.md)
- [/docs/CHANGELOG.md](/docs/CHANGELOG.md) - 変更履歴
