# ADR-0003: 認証に Amazon Cognito + Twitter OAuth を採用

- Date: 2026-06-13
- Status: Accepted

## Context

ユーザー認証の仕組みが必要だった。地下アイドルファンは Twitter（X）の利用率が高い。

## Decision

Amazon Cognito + Twitter（X）OAuth によるソーシャルログインを採用する。

## 却下した選択肢

### メールアドレス + パスワード認証
ファン層に馴染みのある Twitter ログインの方が UX として優れる。独自パスワード管理のリスクも避けられる。

## Consequences

**メリット**
- ファンにとって馴染みのある Twitter アカウントでログインできる
- Cognito の無料枠内で運用できる（月 50,000 MAU まで）
- OAuth の実装経験を積める（学習目的も兼ねる）

**デメリット・リスク**
- Twitter API の仕様変更リスクを受ける
