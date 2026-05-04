# AWS CLI コマンドリファレンス

## 初期設定

**バージョン確認**
```bash
aws --version
```

**対話形式で設定（デフォルトプロファイル）**
```bash
aws configure
```

**プロファイル指定で設定**
```bash
aws configure --profile <profile_name>
```

**現在の認証情報確認**
```bash
aws sts get-caller-identity
```

**プロファイル一覧確認**
```bash
aws configure list-profiles
```

**現在の設定確認**
```bash
aws configure list
```

## S3 操作

**バケット一覧**
```bash
aws s3 ls
```

**バケット作成**
```bash
aws s3 mb s3://<bucket_name>
```

**ファイルアップロード**
```bash
aws s3 cp ./local-file.txt s3://<bucket_name>/
```

**ファイルダウンロード**
```bash
aws s3 cp s3://<bucket_name>/remote-file.txt ./
```

**ディレクトリ同期（ローカル -> S3）**
```bash
aws s3 sync ./dist s3://<bucket_name>/dist
```

## EC2 操作

**インスタンス一覧**
```bash
aws ec2 describe-instances
```

**リージョン指定でインスタンス一覧**
```bash
aws ec2 describe-instances --region ap-northeast-1
```

**インスタンス起動**
```bash
aws ec2 start-instances --instance-ids <instance_id>
```

**インスタンス停止**
```bash
aws ec2 stop-instances --instance-ids <instance_id>
```

## CloudFormation

**テンプレート検証**
```bash
aws cloudformation validate-template --template-body file://template.yaml
```

**スタック作成**
```bash
aws cloudformation create-stack --stack-name <stack_name> --template-body file://template.yaml
```

**スタック更新**
```bash
aws cloudformation update-stack --stack-name <stack_name> --template-body file://template.yaml
```

**スタック削除**
```bash
aws cloudformation delete-stack --stack-name <stack_name>
```

## よく使うオプション

**出力形式指定（json / table / text）**
```bash
aws <service> <operation> --output table
```

**クエリで結果を絞る**
```bash
aws ec2 describe-instances --query "Reservations[].Instances[].InstanceId"
```

**プロファイル指定**
```bash
aws <service> <operation> --profile <profile_name>
```

**リージョン指定**
```bash
aws <service> <operation> --region ap-northeast-1
```
