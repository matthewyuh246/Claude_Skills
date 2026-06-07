# Claude Skills

このプロジェクトで利用できるカスタムSkill（スラッシュコマンド）の一覧です。
各SkillはClaude Code上で `/<コマンド名>` を入力するだけで実行できます。

## Skill一覧

| コマンド | 説明 |
|----------|------|
| `/commit-message` | Gitにステージングされている変更からコミットメッセージを考え、許可を求めずそのままコミットする |
| `/create-pr` | 現在のブランチの変更内容からPRを作成する。タイトルはユーザー入力か、提案を承認して決定する |
| `/design-doc` | 新機能の設計ドキュメント（Mermaid図入りMarkdown）を作成し、関連ドキュメントの更新と最新公式ドキュメントによる妥当性検証まで行う |
| `/explain-file` | 指定したファイルを1行ずつ、できるだけわかりやすく日本語で説明する |
| `/fix-ci` | GitHub ActionsのCIログを確認し、失敗の原因を特定・提示した上で、修正まで行う |
| `/investigate-issue` | 自分にアサインされたGitHub issueから対象を選び、コードやWebで調査して詳しい内容を簡潔にissueへ追記する |
| `/list-skills` | このプロジェクトにあるSkillの一覧を、簡単な説明と呼び出しコマンドとともに提示する |
| `/resolve-review-comment` | 現在のブランチのPRの未対応レビューコメントを1件処理し、修正・コミット・push・返信まで行う |
| `/review-pr` | 現在のブランチのPRの変更ファイルをレビューし、確実に修正すべき箇所のみをGitHubにコメントする |
| `/update-docs` | システム全体を調査し、十分な調査を終えた上でドキュメントの更新内容を提案する。ファイル編集は許可制 |

## 使い方

Claude Code上で対象のコマンドを入力するだけで実行されます。一部のSkillは対象や概要を添えて指定できます。

- 例: `/explain-file src/main.py を説明して`
- 例: `/fix-ci の PR #42 の失敗を直して`
- 例: `/investigate-issue #2 を調査して`

Skillの定義は `.claude/skills/<コマンド名>/SKILL.md` にあります。

## 権限設定

`.claude/settings.json` で、確認プロンプトを省くための権限（`permissions.allow`）を設定しています。

- **git（読み取り系 + commit）**: `git diff` / `status` / `log` / `show` / `rev-parse` / `branch` / `commit`
- **gh（issue操作など）**: `gh issue list` / `view` / `comment` / `gh repo view` / `gh auth status`

`git push` や `git reset` など影響の大きい操作は許可しておらず、実行時に確認プロンプトが出ます。
