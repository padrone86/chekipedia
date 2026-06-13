# chekipedia

地下アイドルの特典会レギュレーションを横断的に検索・閲覧できるまとめサイト。

グループごとのレギュレーションは公式情報を追えば見つかることもありますが、手間がかかります。chekipedia はその手間を省き、横断的に確認できるようにします。コンテンツはファンによる自発的な投稿（Wikipedia 的モデル）で育てていきます。

## ドキュメント

| ドキュメント | 内容 |
|---|---|
| [CLAUDE.md](CLAUDE.md) | AI 向けプロジェクト概要・開発ルール |
| [docs/domain.md](docs/domain.md) | ドメイン知識 |
| [docs/architecture.md](docs/architecture.md) | アーキテクチャ設計 |
| [docs/features.md](docs/features.md) | 機能要件 |
| [docs/data-design.md](docs/data-design.md) | データ設計 |

## 技術スタック

| レイヤー | 技術 |
|---|---|
| フロントエンド | Next.js（静的書き出し） |
| ホスティング | S3 + CloudFront |
| API | Lambda + API Gateway |
| DB | DynamoDB |
| 認証 | Cognito（Twitter OAuth） |
| IaC | Terraform |
| 機密管理 | SSM Parameter Store SecureString |

## ライセンス

MIT
