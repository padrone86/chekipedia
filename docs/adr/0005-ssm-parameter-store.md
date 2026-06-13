# ADR-0005: 機密管理に SSM Parameter Store SecureString を採用

- Date: 2026-06-13
- Status: Accepted

## Context

APIキーや認証情報などの機密情報の管理方法を決める必要があった。

## Decision

SSM Parameter Store SecureString を採用する。

## 却下した選択肢

### AWS Secrets Manager
自動ローテーションなど高機能だが、月 $0.40/シークレットのコストがかかる。個人開発規模では過剰。

## Consequences

**メリット**
- Standard Tier であれば無料枠内で運用できる
- 個人開発規模の要件を十分に満たせる

**デメリット・リスク**
- 自動ローテーションが必要になった場合は Secrets Manager への移行を検討する
