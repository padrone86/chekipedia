# ADR-0004: フロントエンドに Next.js 静的書き出しを採用

- Date: 2026-06-13
- Status: Accepted

## Context

フロントエンドのホスティング方式を決める必要があった。詳細な選定経緯は [ADR-0007](0007-aws-infrastructure.md) を参照。

## Decision

Next.js を静的書き出し（`next export`）モードで採用し、S3 + CloudFront で配信する。

## 却下した選択肢

### Vercel
ランニングコストは最安水準だが、AWS に統一できずノウハウが分散する（[ADR-0007](0007-aws-infrastructure.md) 参照）。

### Amplify
フロント〜バックエンドを統合管理できるが、AppSync（GraphQL）が間に入り構造が把握しにくい。DynamoDB を深く理解したい目的と相性が悪く、「Amplify のノウハウ」になりがちで汎用性が低い。

## Consequences

**メリット**
- S3 + CloudFront の配信コストはほぼ無料枠内に収まる
- アクセスが増えた場合、CloudFront のオリジンを App Runner に切り替えるだけで SSR へ移行できる

**デメリット・リスク**
- 静的書き出しの制約上、ページごとの動的ルーティングに制限がある
