# 実行ファイル化および配布準備の実装計画 (2026-02-14 15:42:00)

この計画では、MangaBoardアプリを他の人がテストできるように実行ファイル化（ビルド）し、**ソースコードとは完全に分離された独立したリポジトリ**に実行ファイルとREADMEのみを配置して配布する手順を定義します。

## ユーザーレビューが必要な事項
- **配布用リポジトリのURL**: 新規リポジトリにプッシュするため、GitHub等のリモートURLを教えていただく必要があります。
- **配布フォルダの名前**: 現在 `MangaBoard_Release` を想定していますが、希望があれば変更可能です。

## 提案される変更

### [配布用リポジトリ]

#### [NEW] [README.md](file:///e:/Obsidian/2025/作成したプログラム/MangaBoard_Release/README.md)
- テスター向けの簡潔な使用ガイドを日本語で作成します。
- インストール不要（WebView2のみ必要）である旨を明記します。

#### [NEW] [tauri-appmangaboard-proto.exe](file:///e:/Obsidian/2025/作成したプログラム/MangaBoard_Release/tauri-appmangaboard-proto.exe)
- ビルドで生成された実行ファイル本体のみをコピーします。

### [開発用リポジトリ]

#### [MODIFY] [task.md](file:///e:/Obsidian/2025/作成したプログラム/MangaBoard/docs/distribution_setup/task.md)
- 独立リポジトリへの移行状況を追跡します。

## 手順の詳細

1. **ビルドの実行**:
   ```bash
   cd tests
   npm run tauri build
   ```
2. **配布用フォルダの作成**:
   - `e:\Obsidian\2025\作成したプログラム\MangaBoard_Release` を作成。
3. **ファイルの集約**:
   - ビルド済みの `.exe` を `MangaBoard_Release` にコピー。
   - テスター専用の `README.md` を作成。
4. **Git リポジトリの初期化**:
   - `MangaBoard_Release` で `git init` を実行。
   - `git add .` および `git commit` を実行。
5. **リモートへのプッシュ**:
   - ユーザーから提供されたURLを `origin` に追加。
   - `git push -u origin main` を実行。

## 検証計画

### 手動検証
- `MangaBoard_Release` フォルダにソースコード（`src`, `tests`, `node_modules` 等）が混入していないことを確認。
- 配布用の `.exe` を単体で起動し、正常に動作することを確認。
