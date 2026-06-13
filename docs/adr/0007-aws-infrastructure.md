# ADR-0007: インフラ・ホスティングに AWS フルサーバーレス構成を採用

- Date: 2026-06-13
- Status: Accepted

## Context

フロントエンド・バックエンド・DB のホスティング先とその構成を決める必要があった。
開発者はクラウドエンジニアで AWS に習熟している。個人開発のため長期的なランニングコストの最小化が重要。

## Decision

AWS でフルサーバーレス構成（S3 + CloudFront / Lambda + API Gateway / DynamoDB / Cognito）を採用する。

## 却下した選択肢

### Vercel + Supabase
ランニングコストとしては最安だが、AWS に統一できずノウハウが分散する。開発者はクラウドエンジニアのため AWS 一本で経験値を積む方が資産になると判断。

### Amplify
フロント〜バックエンドを統合管理できるが、AppSync（GraphQL）が間に入り構造が把握しにくい。DynamoDB を深く理解したい目的と相性が悪く、「Amplify のノウハウ」になりがちで汎用性が低い。

### GCP Cloud Run / OCI Always Free
OCI Always Free は個人開発界隈で評判が高く魅力的だが、今回は DynamoDB・Cognito・フルサーバーレス構成の習得が主目的。別プロジェクトで挑戦する候補として残す。

## Consequences

**メリット**
- 開発者が AWS に習熟しているため、インフラ管理コストが低い
- DynamoDB・Cognito・フルサーバーレス構成の経験値を業務にも活かせる
- フルサーバーレス構成でアイドル時のコストがほぼゼロ
- 将来の App Runner 移行・スマホアプリ化も AWS 内で完結できる

**デメリット・リスク**
- AWS に依存した構成のため、マルチクラウド化は困難
- Lambda のコールドスタートによるレイテンシが発生しうる
