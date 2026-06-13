# ADR-0002: データベースに DynamoDB を採用

- Date: 2026-06-13
- Status: Accepted

## Context

データベースの選定が必要だった。詳細な選定経緯は [ADR-0007](0007-aws-infrastructure.md) を参照。

## Decision

DynamoDB を採用する。

## 却下した選択肢

### RDS
無料枠が1年で終了し、その後は月数千円〜。個人開発の長期運用に不向き。

### Supabase（PostgreSQL）
AWS と組み合わせるハイブリッド構成も検討したが、管理が分散するデメリットがある。

## Consequences

**メリット**
- 従量課金でランニングコストを最小化できる
- NoSQL の設計経験を積める（学習目的も兼ねる）

**デメリット・リスク**
- アクセスパターンを起点にテーブルを設計する必要があり、RDB より設計難易度が高い（[Issue #2](https://github.com/padrone86/chekipedia/issues/2)）
