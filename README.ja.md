# pstack 日本語版

[English](README.md) | [日本語ドキュメント](docs/ja/README.md)

> この文書は原文 README の日本語訳です。コマンド・スキル名・設定値は原文のまま記載しています。インストール例は原作者のリポジトリを参照します。

[![コーヒーで支援](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-support-yellow?logo=buy-me-a-coffee&logoColor=white)](https://buymeacoffee.com/codenyer)

Lauren Tan の [pstack](https://github.com/cursor/plugins/tree/main/pstack) は、エージェントの成果を改善するための、明確な設計方針を持った Cursor 向けスキル集です。このリポジトリは、それを Claude Code、Codex、Pi、GitHub Copilot などのエージェント実行環境へ移植したものです。上流の更新を追跡しつつ、この移植版独自の方針変更も取り込んでいます。それぞれの変更は [`tools/forks.json`](tools/forks.json) に宣言されています。

`poteto-mode` に目標を伝えると、タスクに合ったワークフローを呼び出します。コードを簡潔で単純な状態に保ち、検証まで進めます。

テストでは捉えられない並行処理のバグや不変条件には、別のプラグイン [agent-formal-verify](https://github.com/michael-denyer/agent-formal-verify) を参照してください。TLA+ によるモデル検査と Lean による証明を追加できます。

## インストール

### Claude Code

Claude Code 内で実行します。

```text
/plugin marketplace add michael-denyer/pstack-claude
/plugin install pstack@pstack-claude
```

### Codex

ターミナルで実行します。

```shell
codex plugin marketplace add michael-denyer/pstack-claude
codex plugin add pstack@pstack-claude
```

### Pi

ターミナルで実行します。

```shell
pi install git:github.com/michael-denyer/pstack-claude
```

パッケージはスキルと pstack の Pi 拡張を読み込みます。この拡張は、スキルが使うサブエージェント、質問、ウェイクアップのツールに加えて、`/loop` とワークフローへの振り分け指示を提供します。スキルは `/skill:<name>` で呼び出します。

### GitHub Copilot

ターミナルで実行します。

```shell
copilot plugin marketplace add michael-denyer/pstack-claude
copilot plugin install pstack@pstack-claude
```

これにより、`~/.copilot` を共有する Copilot CLI と GitHub Copilot アプリに pstack がインストールされます。その後、新しいセッションを開始してください。Copilot 向けには既定のモデルを同梱していません。モデルを必要とするスキルを初めて実行すると、`setup-pstack` が起動し、そのアカウントで利用できるモデルから選択します。以降のセッションでは、その選択を再利用します。

Copilot 版は Copilot CLI 1.0.87〜1.0.92 でテストされています。これらのバージョンでは、振り分けフックのコンテキストが、他のプラグインのセッション開始時コンテキストとともにセッションへ渡されます。今後のバージョンで1つのプラグインのコンテキストしか保持されなくなった場合、`setup-pstack` は代わりに `~/.copilot/copilot-instructions.md` に記載する[常設の指示](plugins/pstack/skills/setup-pstack/copilot.md#wire-it-in)を提示します。1.0.92 では、CLI が computer-use 実験への割り当てをキャッシュすると、`copilot -p` セッションにプラグインのスキルが表示されず、`skill` の呼び出しが「Skill not found」を返します。対話セッション、フック、エージェントは影響を受けません。

モデルの既定値を変更する、役割ごとの推論量を指定する、または自動振り分けを無効にするには、`setup-pstack` を実行してください。たとえば `arena runners: opus @xhigh, fable @max` と指定できます。Claude Code はプラグインの `pstack:effort-<level>` または `pstack:poteto-agent-<level>` エージェントを通じて、その設定で実行します。推論量を指定していない役割は、設定シートの `default effort` 行に指定がある場合を除き、セッションの推論量を引き継ぎます。

プラグインは Claude Code、Codex、GitHub Copilot に振り分けフックをインストールします。Codex では、実行前に `/hooks` で信頼することを求められます。Pi では、拡張が同じ振り分け指示を挿入します。Claude Code と Copilot CLI では `/pstack:setup-pstack` を使用してください。

### その他の実行環境

OpenCode（CLI とデスクトップアプリ）、Gemini CLI、Prime Agent、およびスキルのみを導入した Codex は、`~/.agents/skills/` からスキルを読み込みます。ターミナルで実行します。

```shell
git clone https://github.com/michael-denyer/pstack-claude
cd pstack-claude
mkdir -p ~/.agents/skills
for s in plugins/pstack/skills/*/; do
  target=~/.agents/skills/"$(basename "$s")"
  test -e "$target" || test -L "$target" || ln -s "$(pwd)/$s" "$target"
done
```

更新時は、クローン先で `git pull` を実行し、その後もう一度 `for` ループを実行して、前回以降に追加されたスキルへのリンクを作成してください。この方法では振り分けフックが入らないため、`poteto-mode` を名前で指定するか、実行環境の指示ファイルに常設の指示を追加します。環境ごとの注意点やアンインストール方法は、[共通スキルのインストール](docs/reference.md#shared-skills-installation)を参照してください。

## 使い始める

```text
poteto-mode を使って、ページを切り替えると検索フィルターがリセットされる不具合を修正してください。
```

バグの場合は、失敗を再現し、`how` と `why` で調査し、修正を委任してから、失敗していたケースを再実行します。修正が関数の境界をまたぐ場合は、実装前に `architect` を使います。最終的に、修正と、修正前に失敗し修正後に成功したことを示す証拠が返されます。

[その他のプレイブック（作業手順書）](plugins/pstack/skills/poteto-mode/SKILL.md#playbooks)は、計画、機能開発、リファクタリング、性能問題、調査、試作、PR の保守、変更の取り込み、長期プロジェクトを扱います。

![Claude Code、Codex、Pi 上の poteto-mode は依頼を検証済みの成果へと進めます。プレイブックを選択し、architect、arena、swarm で計画と委任を行い、interrogate、テスト、計測でレビューと検証を行います。プロジェクト独自のプレイブックで手順を調整でき、setup-pstack で役割ごとのモデルと推論量を設定できます。how、why、unslop などの補助スキルもあります。](assets/pstack-overview.png)

## 詳細

- [スキルとスラッシュコマンド](docs/reference.md#slash-commands)
- [実行環境の設定](docs/reference.md#runtime-support)
- [モデルと依存関係](docs/reference.md#configuration-and-dependencies)
- [保守と移植範囲](docs/reference.md#maintenance)

## データの取り扱い

pstack 自体にはサーバーもテレメトリーもありません。スキルの指示によってエージェントが読み取る内容は、セッションの会話記録も含め、利用しているモデルの提供元へ送られます。スクリプトはローカルで実行され、PR 関連のツールは GitHub CLI のログイン情報を使用します。

## 貢献

この移植版の改善への協力を歓迎します。バグ報告、文書の修正、実行環境への対応改善を受け付けています。必要なチェックと変更を加える場所については [CONTRIBUTING.md](CONTRIBUTING.md) を参照してください。脆弱性は [SECURITY.md](SECURITY.md) の説明に従い、非公開で報告してください。

移植版の保守を支援したい方は、[保守担当者にコーヒーをおごる](https://buymeacoffee.com/codenyer)ことができます。

## ライセンス

この移植版と、その変更・追加部分も [MIT ライセンス](LICENSE)で公開されています。© 2026 Michael Denyer。元の pstack は © 2026 Lauren Tan、取り込まれた cursor-team-kit および thermos のスキルは © 2026 Cursor です。[LICENSE-cursor-team-kit](LICENSE-cursor-team-kit)、[LICENSE-thermos](LICENSE-thermos)、[NOTICE.md](NOTICE.md) を参照してください。
