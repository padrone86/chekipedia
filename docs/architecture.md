# アーキテクチャ設計

## 概要

フルサーバーレス構成の AWS 環境で運用する。
ランニングコストを最小限に抑えつつ、将来的なスケールアップに対応できる設計とする。

## 構成図

```
ユーザー
  │
  ▼
CloudFront
  ├── S3（フロントエンド静的ファイル）
  └── API Gateway
        └── Lambda（APIサーバー）
              └── DynamoDB（データ）
                  Cognito（認証）
                  SSM Parameter Store（機密情報）
```

## 各サービスの役割

### フロントエンド
- **Next.js**（静的書き出しモード）
- `next export` でビルドした静的ファイルをS3に配置
- CloudFront経由で配信

### API
- **Lambda + API Gateway**
- RESTful API
- 認証が必要なエンドポイントはCognitoで保護

### データベース
- **DynamoDB**
- NoSQL、従量課金
- アクセスパターンを設計の起点とする（別途データ設計ドキュメント参照）

### 認証
- **Amazon Cognito**
- Twitter（X）OAuthによるソーシャルログイン
- 初期は管理者のみ編集権限、将来的に申請ベースで投稿者を開放

### IaC
- **Terraform**
- 全リソースをコードで管理

### 機密管理
- **SSM Parameter Store SecureString**
- APIキーや認証情報を管理
- Secrets Managerより低コスト、個人開発規模では十分

## コスト方針

- 月額5,000円以下を目標
- スモールスタート時はほぼ無料枠内で運用可能
- アクセス増加に応じてApp Runnerへの移行を検討（SSR対応）

## 将来的な拡張

### App Runner移行（SSR対応）
- アクセスが増えSEO強化が必要になった段階で検討
- フロントのコードはほぼ変更不要、インフラ側の変更のみ
- CloudFrontのオリジンをS3からApp Runnerに切り替え

### スマホアプリ化
- Lambda + API GatewayのAPIをそのまま流用可能
- フロントエンドのみReact Nativeなどで実装

## セキュリティ方針

初期フェーズで対応するもの：

| 対応 | 手段 | コスト |
|---|---|---|
| HTTPS強制 | CloudFront設定 | 無料 |
| S3直接アクセス禁止 | バケットポリシー | 無料 |
| IAM最小権限 | Terraformで設定 | 無料 |
| 機密情報管理 | SSM SecureString | 無料 |
| 認証・認可 | Cognito | 無料枠内 |

WAFはアクセスが増えた段階で検討（月$5〜6）。
