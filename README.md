# claude-ui-text

| 項目 | 内容 |
| --- | --- |
| 対象 | 画面に表示する文言（ボタン・見出し・フォーム・エラー・確認ダイアログ・空状態・完了の通知）と、サービスが利用者へ自動で送るメールの本文 |
| 動作環境 | Claude Code |
| ライセンス | MIT（[LICENSE](LICENSE)） |

Claude Code に画面の文言を書かせるときの決まりをまとめたスキル `ui-text` を配布する。文言を作る・直す依頼を受けると、Claude がこのスキルを読み込み、エンドユーザーが次の操作に迷わない文言を書く。

## 1. このスキルでできること

| できること | 頼み方の例 |
| --- | --- |
| 敬体で、ユーザーの行動を主語にした短い文言を書く | 「この画面の文言を考えて」 |
| ボタンを、押した結果が分かる動詞にする。同じ操作を画面ごとに別の語で呼ばない | 「ボタンのラベルを決めて」 |
| エラーメッセージを「何が起きたか」と「どうすればよいか」の文型で、責めない言い方にする | 「エラーメッセージを書いて」 |
| 確認ダイアログを、タイトル・元に戻せるかを書いた本文・動作名のボタンで組む | 「確認ダイアログの文言を作って」 |
| `lang`・`title`・`alt`・`aria-label`・`label` など、画面に出ないが読み上げやタブに出る文言を埋める | 「HTML の文言を直して」 |
| 既存の文言を提出前チェックの項目で見直す | 「この文言おかしくない？」 |

## 2. 使いどころの例

| 頼み方 | Claude が行うこと |
| --- | --- |
| 「保存に失敗したときのメッセージを書いて」 | 「保存できませんでした。時間をおいてもう一度お試しください」のように、次の行動を示す。入力済みの内容は消さない |
| 「削除の確認ダイアログを作って」 | 対象と件数を本文に入れ、元に戻せないことを書く。ボタンは `削除する` と `キャンセル` にし、危険な側を既定にしない |
| 「一覧が0件のときの表示を考えて」 | 「データがありません」で終わらせず、次の一手を書く |

## 3. 扱わないこと

| 扱わないもの | 代わりに使うもの |
| --- | --- |
| 業務資料と、人が業務の連絡として送るメール | [claude-doc-writing](https://github.com/yuu0706/claude-doc-writing) |
| 画面の見た目・配置・構造 | [claude-ui-design](https://github.com/yuu0706/claude-ui-design) |

## 4. 入れ方

### 4.1 プラグインとして入れる

Claude Code の会話の中で、次を実行する。

```
/plugin marketplace add yuu0706/claude-ui-text
/plugin install ui-text@claude-ui-text
```

シェルから入れる場合は次のとおり。

```sh
claude plugin marketplace add yuu0706/claude-ui-text
claude plugin install ui-text@claude-ui-text
```

入れた後に新しい会話を始めると、スキルが読み込まれる。スキルの名前は `ui-text:ui-text` になる。

### 4.2 clone してリンクを張る

プラグインの仕組みを使わずに、スキル置き場へ直接置くこともできる。

```sh
git clone https://github.com/yuu0706/claude-ui-text ~/claude-tools/claude-ui-text
ln -s ~/claude-tools/claude-ui-text/plugins/ui-text/skills/ui-text ~/.claude/skills/ui-text
```

## 5. 更新・外し方

| 入れ方 | 更新 | 外し方 |
| --- | --- | --- |
| プラグイン | `/plugin marketplace update claude-ui-text`。会話の中の `/plugin` の **Marketplaces** で自動更新も有効にできる | `/plugin uninstall ui-text@claude-ui-text` |
| clone とリンク | clone した場所で `git pull` | `rm ~/.claude/skills/ui-text` |

プラグインの更新は、`plugins/ui-text/.claude-plugin/plugin.json` の `version` が変わったときだけ届く。

## 6. 関係するスキル

| スキル | 関係 |
| --- | --- |
| [claude-ui-design](https://github.com/yuu0706/claude-ui-design) | 画面の見た目と配置を受け持つ。本スキルと対になる |
| [claude-doc-writing](https://github.com/yuu0706/claude-doc-writing) | 業務資料を受け持つ。表記はどちらも JTF 日本語標準スタイルガイドに従う |
| [claude-git-conventions](https://github.com/yuu0706/claude-git-conventions) | 文言だけを変えたコミットは、その旨を件名に書く |

## 7. ライセンス

MIT License である。全文は [LICENSE](LICENSE) にある。
