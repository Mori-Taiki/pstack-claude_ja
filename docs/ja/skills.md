# スキル一覧 日本語訳

[日本語ドキュメント](README.md) | [原文](../reference.md#slash-commands)

パッケージには63個のスキルディレクトリがあり、公開スキル39個と `principle-*` の参照用スキル24個で構成されます。Claude Code は `/pstack:<name>`、Pi は `/skill:<name>` で呼び出します。Codex ではスキル名を指定するか、[任意のショートカット](../reference.md#codex)をインストールして、表の `/name` 形式を使います。

以下は原文の用途一覧の翻訳です。コマンドのリンク先は各スキルの英語本文です。中心スキルには [poteto-mode の全文日本語訳](poteto-mode.md)があります。

| コマンド | 使う場面 |
| --- | --- |
| [/poteto-mode](../../plugins/pstack/skills/poteto-mode/SKILL.md) | 単純ではないタスク全般の標準的な入口。 |
| [/how](../../plugins/pstack/skills/how/SKILL.md) | サブシステムがどう動くかを順に調べる。 |
| [/why](../../plugins/pstack/skills/why/SKILL.md) | なぜその形で作られたかを調査する。複数の MCP を使って並行して証拠を集める。 |
| [/architect](../../plugins/pstack/skills/architect/SKILL.md) | 関数の境界をまたぐコードを書く前に、型とモジュール構造を決める。 |
| [/arena](../../plugins/pstack/skills/arena/SKILL.md) | 同じタスクへの N 個の試行を並行実行し、優れた部分を選ぶ。 |
| [/interrogate](../../plugins/pstack/skills/interrogate/SKILL.md) | 3つの異なるモデルに差分の欠陥を探させる。 |
| [/automate-me](../../plugins/pstack/skills/automate-me/SKILL.md) | 最近の会話記録から、自分専用の -mode スキルの草案を作る。 |
| [/reflect](../../plugins/pstack/skills/reflect/SKILL.md) | 長いタスクから得た教訓をスキルの編集として残す。 |
| [/correct](../../plugins/pstack/skills/correct/SKILL.md) | リポジトリでエージェントが繰り返す間違いを見つけ、実効性のある最上位の仕組みで、それぞれを起こせなくする。 |
| [/tdd](../../plugins/pstack/skills/tdd/SKILL.md) | まず失敗するテストを書き、その後に修正してバグを直す。 |
| [/benchmark-checklist](../../plugins/pstack/skills/benchmark-checklist/SKILL.md) | 測定した高速化や退行を報告・判断に使う前に、制約要因、調整、誤差、反復測定、処理全体との関係を点検する。 |
| [/typescript-best-practices](../../plugins/pstack/skills/typescript-best-practices/SKILL.md) | 型システムの原則を TypeScript の具体的な構文へ落とし込む。 |
| [/teach](../../plugins/pstack/skills/teach/SKILL.md) | how と why を組み合わせて、サブシステムを平易に説明する。 |
| [/swarm](../../plugins/pstack/skills/swarm/SKILL.md) | N 個のワーカーを範囲分担または競争の形で並行実行し、統合した1つの報告を返す。 |
| [/technical-writing](../../plugins/pstack/skills/technical-writing/SKILL.md) | 文書、RFC、README、PR の説明、コミットメッセージを、階層化された共通の基準で書く。 |
| [/bro](../../plugins/pstack/skills/bro/SKILL.md) | 直前のメッセージを専門用語のない平易な言葉で言い直す。 |
| [/in-your-own-words](../../plugins/pstack/skills/in-your-own-words/SKILL.md) | 着手前に、目標と問題を理解した内容として言い返す。 |
| [/sharpen](../../plugins/pstack/skills/sharpen/SKILL.md) | 手順を細かく指定しすぎず、一流の専門家のように、タスクの狙いを本当に求める成果へ定め直す。 |
| [/figure-it-out](../../plugins/pstack/skills/figure-it-out/SKILL.md) | 同梱のプレイブックが合わないタスクに、厳密で監査可能な専用の手順書を設計する。 |
| [/show-me-your-work](../../plugins/pstack/skills/show-me-your-work/SKILL.md) | 判断を、レビュー可能な TSV 形式の判断記録に残す。 |
| [/blast-radius](../../plugins/pstack/skills/blast-radius/SKILL.md) | 差分の外側で変更が壊しうるものを見つけ、コードの実行で安全性を示す。 |
| [/recall](../../plugins/pstack/skills/recall/SKILL.md) | チャット履歴、現在の状態、共有記録から最近の作業文脈を把握する。 |
| [/ketchup](../../plugins/pstack/skills/ketchup/SKILL.md) | ユーザーの前回のメッセージ以降に、このチャットで起きたことを把握し、各アクション項目の要点をまとめる。 |
| [/setup-pstack](../../plugins/pstack/skills/setup-pstack/SKILL.md) | pstack の役割ごとのモデル選択を設定する。 |
| [/poteto-help](../../plugins/pstack/skills/poteto-help/SKILL.md) | pstack への質問に、送るべきプロンプトと回答の根拠となったファイルを添えて答える。 |
| [/unslop](../../plugins/pstack/skills/unslop/SKILL.md) | AI 特有の不自然な表現を取り除いて文章を整える。 |
| [/no-comments](../../plugins/pstack/skills/no-comments/SKILL.md) | レビュー前にコメントを削り、受け入れた指摘を修正し、主張されている制約を実際の仕組みに組み込む。 |
| [/create-verification-skill](../../plugins/pstack/skills/create-verification-skill/SKILL.md) | プロジェクト専用の検証スキルと機能マップを生成する。 |
| [/maintain-verification-skill](../../plugins/pstack/skills/maintain-verification-skill/SKILL.md) | 実態とずれた検証スキルと機能マップを再同期する。 |
| [/deslop](../../plugins/pstack/skills/deslop/SKILL.md) | コミット前に、差分から AI が加えがちな不要なコードを除く。 |
| [/babysit](../../plugins/pstack/skills/babysit/SKILL.md) | 開いている PR を監視し、CI とコメントへ対応して、マージ準備完了の状態を保つ。 |
| [/thermo-nuclear-review](../../plugins/pstack/skills/thermo-nuclear-review/SKILL.md) | ブランチの変更について、バグ、破損、セキュリティ上の問題、開発体験の退行、機能ゲートの抜けを監査する。 |
| [/thermo-nuclear-code-quality-review](../../plugins/pstack/skills/thermo-nuclear-code-quality-review/SKILL.md) | 保守性を極めて厳格に監査する。 |
| [/thermos](../../plugins/pstack/skills/thermos/SKILL.md) | 2種類の thermo-nuclear レビューをサブエージェントで並行実行し、結果を統合する。 |
| [/make-pr-easy-to-review](../../plugins/pstack/skills/make-pr-easy-to-review/SKILL.md) | レビュー前に、雑然とした履歴を整理し、PR の説明を改善する。 |
| [/fix-ci](../../plugins/pstack/skills/fix-ci/SKILL.md) | 失敗している PR のチェックを探し、ログを確認して、対象を絞った修正を行う。 |
| [/fix-merge-conflicts](../../plugins/pstack/skills/fix-merge-conflicts/SKILL.md) | 対話操作なしでマージ競合を解消し、検証して完了させる。 |
| [/get-pr-comments](../../plugins/pstack/skills/get-pr-comments/SKILL.md) | 現在の PR のレビューコメントを取得して要約する。 |
| [/what-did-i-get-done](../../plugins/pstack/skills/what-did-i-get-done/SKILL.md) | ユーザーが選んだ期間に作成したコミットを要約する。 |

24個の原則の用途は [Poteto mode の「原則」](poteto-mode.md#原則)にあります。
