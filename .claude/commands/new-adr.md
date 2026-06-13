docs/adr/ 以下に新しい ADR（Architecture Decision Record）ファイルを作成する。

手順：
1. docs/adr/ 内の既存ファイルを確認し、次の連番（4桁ゼロ埋め）を決定する
2. タイトルを引数から取得する。引数がなければユーザーに聞く
3. ファイル名: `docs/adr/NNNN-<kebab-case-title>.md`
4. 以下のテンプレートで作成する：

```markdown
# ADR-NNNN: タイトル

- Date: YYYY-MM-DD
- Status: Accepted

## Context

（なぜこの決定が必要だったか）

## Decision

（何を決めたか）

## 却下した選択肢

### 選択肢名
（なぜ選ばなかったか）

## Consequences

**メリット**
-

**デメリット・リスク**
-
```

5. 却下した選択肢がない場合はそのセクションを省略してよい
6. ファイルを作成したら、パスをユーザーに伝える
