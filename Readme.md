# osc_niigata_2023-demo

2023/11/25 (土) [Open Source Conference 2023 Niigata](https://ospn.connpass.com/event/297587/) で披露したデモのソースコードです。

Google Colaboratoryで動作します。

## 準備

### DALL-Eの場合

1. OpenAIのAPIキーを取得します。
2. `openai.env` という名前のテキストファイルを作成し、以下の内容を記述します。
    `<OPENAI APIキー>` の部分を実際のAPIキーに置き換えてください。
    ```bash
    OPENAI_API_KEY=<OPENAI APIキー>
    ```
3. Googleドライブのマイドライブ直下に `openai.env` ファイルをアップロードします。

### Stable Diffusionの場合 (Amazon Bedrock使用)

1. AWSのマネジメントコンソールを開き、オレゴンリージョン(us-west-2)のAmazon Bedrockにて、基幹モデルの利用申請をします。
    - 参考: [Amazon Bedrock をマネジメントコンソールからちょっと触ってみたいときは Base Models（基盤モデル）へのアクセスを設定しましょう | DevelopersIO](https://dev.classmethod.jp/articles/if-you-want-to-try-out-amazon-bedrock-from-the-management-console-you-can-set-up-access-to-base-models/)
2. IAMユーザを作成し、APIキーを取得します。
3. IAMユーザの権限に以下を追加します。インラインポリシーで良いです。
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "BedrockFullAccess",
                "Effect": "Allow",
                "Action": [
                    "bedrock:*"
                ],
                "Resource": "*"
            }
        ]
    }
    ```
4. `bedrock_iam_key.env` という名前のテキストファイルを作成し、以下の内容を記述します。
    `<AWS ACCESS KEY ID>` や `<AWS SECRET ACCESS KEY>` の部分を実際のAPIキーに置き換えてください。
    ```bash
    AWS_ACCESS_KEY_ID=<AWS ACCESS KEY ID>
    AWS_SECRET_ACCESS_KEY=<AWS SECRET ACCESS KEY>
    ```
5. Googleドライブのマイドライブ直下に `bedrock_iam_key.env` ファイルをアップロードします。

## 実行

- 先頭のセルから順番に実行すると、画像が生成されます。
    - ライブラリのバージョンを固定してないので、ライブラリバージョンアップ時に動作しなくなるかもしれません。
- 実行時にGoogleドライブのマウントをしますので、マウントしたいGoogleアカウントを指定し、アクセス許可をしましょう。
- 生成された画像は、マイドライブ直下に保存されます。

