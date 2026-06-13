# ADR-0001: IaC に Terraform を採用

- Date: 2026-06-13
- Status: Accepted

## Context

インフラをコードで管理する IaC ツールの選定が必要だった。

## Decision

Terraform を採用する。

## 却下した選択肢

### AWS CDK
TypeScript でインフラを書ける点は魅力だが、内部的に CloudFormation に変換されるため diff が見えにくく、何が起きているか把握しにくい。

## Consequences

**メリット**
- `terraform plan` で変更の diff が明示的に確認できる
- 使い慣れているため、学習コストが発生しない
- 将来 AWS 以外のリソース（DNS 等）を管理する場合も技術スタックが増えない

**デメリット・リスク**
- state ファイルの管理（S3 + DynamoDB）が別途必要になる
