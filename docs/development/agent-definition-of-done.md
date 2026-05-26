# Agent Definition of Done

作成: 2026-05-26
対象: Prize Hunter 全リポジトリのエージェント

## 目的

各エージェントが「完了」を宣言する前に実行すべき最小検証と、
完了報告に含める情報を標準化する。

---

## 完了報告フォーマット

```
【完了】<repo_name>: <実施内容の1行要約>

検証結果:
- <コマンド>: ✅ PASS / ❌ FAIL（失敗時は理由を記載）
- <コマンド>: ✅ PASS / ❌ FAIL

未実行チェック:（該当なし or 理由を記載）
- <コマンド>: スキップ理由

変更ファイル:
- <ファイルパス>: <変更内容1行>
```

### 記載ルール

1. **検証結果は必ず書く** — コマンドを実行しなかった場合でも「未実行チェック」に理由を明記する。
2. **PASS/FAIL を明示する** — 「おそらく動く」は PASS ではない。コマンドを実行して確認する。
3. **失敗した場合は止める** — FAIL が出た場合は修正してから再実行するか、オーケストレーターに相談する。
4. **変更ファイルは省略しない** — レビューの起点になるため、全変更ファイルを列挙する。

---

## リポジトリ別 最小検証コマンド

### admin

```bash
npm run build
```

- build が通ることを確認する。
- UI変更を含む場合: 主要画面（景品一覧、買取申請管理）の Playwright smoke を実行。

### backend

```bash
make test-unit
```

- 全 unit test が PASS であること。
- API変更・DB変更を含む場合: `make test-e2e` も実行する。

### kaitori-web

```bash
npm run build
```

- build が通ることを確認する。
- UI変更を含む場合: 買取申請フロー（検索→詳細→申請）の Playwright smoke を実行。

### lp

- `python -m http.server 8000` で起動し、以下を目視確認:
  - index.html が表示される
  - 主要リンク（利用規約・プライバシーポリシー）が動作する

### prize_hunter_app

```bash
make analyze
```

- analyze が警告・エラーなしで通ること。
- コード生成が必要な変更（freezed/retrofit）: `make gen` を先に実行する。
- build確認が必要な場合: `flutter build apk --debug` または `flutter build ios --debug --no-codesign`

### scraping

- 変更した scraper の fixture smoke を実行する:
  ```bash
  # 例: 駿河屋の場合
  python -m pytest tests/test_surugaya.py -v
  ```
- API endpoint smoke:
  ```bash
  curl -s http://localhost:8000/health | jq .
  ```

### tohobi-web

```bash
npm run build
```

- build が通ることを確認する。
- UI変更を含む場合: 主要画面の Playwright smoke を実行。

### prize-hunter-idl

```bash
npm run lint
npm run validate
npm run generate
```

または一括:

```bash
bash scripts/check.sh
```

- スキーマ変更を含む場合: breaking diff を確認する:
  ```bash
  npm run diff -- main
  ```
- breaking 変更がある場合は必ず ADR または CHANGELOG に記録し、deprecated 期間を設ける。

---

## 失敗時の扱い

### 自己解決できる場合

1. エラー内容を確認して修正する。
2. 再度コマンドを実行して PASS を確認する。
3. 完了報告に「失敗→修正→PASS」の経緯を記載する。

### 自己解決できない場合

1. 完了報告の代わりに **ブロッカー報告** をオーケストレーターに送る:
   ```
   【ブロッカー】<repo_name>: <コマンド> が FAIL。<エラー内容の要約>
   対応方針の相談が必要です。
   ```
2. オーケストレーターの指示を待つ。作業を中途半端に進めない。

---

## 未実行チェックの明記ルール

以下のケースでは「未実行チェック」に理由を書いてスキップを明示する:

| ケース | 例 |
|--------|-----|
| コマンドが環境に存在しない | `playwright` 未インストール |
| 変更対象に関係ない検証 | ドキュメントのみ変更で build skip |
| 時間・コスト上の制約 | E2E テストが 30 分以上かかる |
| 環境依存の制約 | CI 停止中で実行不可 |

**「確認できなかった」はスキップ理由にならない。** 実行して確認することが前提。

---

## 関連ドキュメント

- `docs/plans/harness-engineering-v2.md` — Phase 2 の背景と方針
- `hub.yaml` — リポジトリ別コマンド一覧
- `docs/decisions/` — 個別の設計判断 (ADR)
