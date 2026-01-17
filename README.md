# Dependabot

Dependabotを使ったワークフローを作成してみた

## 運用概要

このリポジトリでは、以下の運用を行っています。

1. **GitHub Actionsを使用したCI/CDパイプライン**
   - `.github/workflows/example.yml` に定義されたワークフローに基づき、`master` ブランチへのプッシュやプルリクエストをトリガーとして以下の処理を実行します。
     - コードのチェックアウト
     - Python環境のセットアップ
     - 必要な依存関係のインストール（`requirements.txt` を使用）
     - `pytest` を用いたテストの実行

2. **Dependabotによる依存関係の自動更新**
   - `.github/dependabot.yml` に設定を記載しています。
   - 以下のエコシステムの依存関係を毎週チェックし、必要に応じてPull Requestを作成します。
     - `pip` (Pythonの依存関係管理)
     - `github-actions` (GitHub Actionsのバージョン管理)

3. **DependabotのPull Requestの自動マージ**
   - `.github/workflows/auto-merge.yml` に定義されたワークフローにより、Dependabotが作成したPull Requestを自動的にマージします。
   - Pull Requestに特定のラベルが付与されると、このワークフローがトリガーされます。
   - マージ方法は `squash` を使用しています。

4. **ローカルでのGitHub Actionsのテスト**
   - `act` を使用して、ローカル環境でGitHub Actionsのワークフローをテストできます。
   - `.actrc` ファイルを作成し、`act` 実行時の設定を記載しています。

### 注意点
- `requirements.txt` ファイルに必要なPythonパッケージを記載してください。
- テストは `tests/` ディレクトリ内に配置し、`pytest` で実行可能な形式で記述してください。
- Dependabotが作成するPull Requestを定期的に確認し、必要に応じてラベルを付与してください。
- 自動マージ機能を使用する際は、セキュリティに注意してください。
