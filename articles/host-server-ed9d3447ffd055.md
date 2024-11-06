---
title: "【個人規模】Next.jsデプロイにおすすめのサーバーを比較しました"
emoji: "👺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Nextjs","Netlify","Vercel","CloudflarePages","CloudRun"]
published: true
---

## 本記事ではフリープランで利用することを想定しています(CloudRun、Amplify除く)

比較したホスティングサービス

| サービス               | 商用利用        | コスト                                       |
|----------------------|----------------|----------------------------------------------|
| **Vercel**           | 不可（Freeプラン） | 無料でデプロイ可能（商用利用にはProプラン以上が必要） |
| **GitHub Pages**     | 不可            | 無料（静的ホスティングのみ対応）                      |
| **Cloudflare Pages** | 可能            | 無料                          |
| **Netlify**          | 可能            | 無料                        |
| **AWS Amplify**      | 可能            | 従量課金制　詳細は調査中|
| **Cloud Run**        | 可能            | 従量課金制 (コストを抑えやすい。月数十円程度)                 |

今回初めて**Cloudflare Pages**と**Cloud Run**を知った方は、ぜひそれだけでも目を通してみて欲しいです！すごくいいサービスなので！

今後も良さそうなサービスがあれば、随時アップデートしていきます！

## 本題の前に

VercelはNext.jsに最適化されたサーバーなので、**迷ったらVercel**を使いたいです。

公式ドキュメントを見ても見つけられなかったので、ここの明確な根拠はありません。
しかし、**VercelとNext.jsは開発元が同じ**なので、Next.jsをデプロイするのに最適なインフラストラクチャが構築されていると考えられます。
何よりもNext.jsで破壊的な変更がこの先起こらないとも限りません。その時にいち早く対応するのは開発元が同じであるVercelなのは必然かなと思います。
よって、安定とパフォーマンスを選ぶならVercelが良いと考えています。

しかし、このあたりは **サービスの要件(底コストや商用利用、コンテナ技術を使いたいなど)** によると思います。
Vercelを使っていた方もこの記事を見て、「CloudRunの方がいいんじゃないか？」「いいや、Cloudflare Pagesだね」などなど、みなさんの最適を見つける判断材料になれれば嬉しいです。

:::message
Vercelのfreeプランでは商用利用が禁止されていますが、商用利用が必要なほどユーザーからのトラフィックが増えている場合は、サーバーのスペックを上げる必要があるかもしれません。
その場合、Vercelの有料プランを検討をしてもいいかもです。
:::

<!--**アナリティクス**-->

## 知っておきたい用語

:::details .htaccess
Webサーバーの動作をディレクトリ単位で制御することができるので、GitHub Pagesでカスタムヘッダーを付与することが可能かもしれないと思い、今回調査しました。

:::

::: details HTTPヘッダー
HTTPヘッダーは、HTTPリクエストやレスポンスに付加情報を提供するためのものです。
CORSなどのヘッダーを付与し、特殊な挙動を実現できます。
<https://apidog.com/jp/blog/how-to-check-http-headers/>

> HTTP ヘッダーにより、 HTTP リクエストやレスポンスでクライアントやサーバーが追加情報を渡すことができます。
> <https://developer.mozilla.org/ja/docs/Web/HTTP/Headers>
:::

## Vercel

### 特徴

- 商用利用の不可
- Next.jsと開発元が同じ
- 高パフォーマンス
- アナリティクス利用可（期限あり）

商用利用が不可ですが、デプロイもしやすいので初期リリース時にホストするのはありだと考えています。

### 商用利用不可

freeプランでは、Webサイトに広告を貼るなどの行為も禁止しています。

>商用利用
>趣味のチームは非営利の個人使用のみに制限されています。プラットフォームを商用目的で使用する場合は、Pro プランまたは Enterprise プランのいずれかが必要です。
>参考 : <https://vercel.com/docs/limits/fair-use-guidelines#commercial-usage>

:::message
途中で商用利用したい場合には、Cloudflare Pages(商用可)への移行も簡単なので、最初にVercelをホスト先にするのはありだと思います。
:::

### Next.jsと開発元が同じ

 Next.jsと開発元が同じなので、Next.jsに大きな変更が起きてもいち早く対応されると考えられます。

### 高パフォーマンス

Nextjsに最適化されたインフラストラクチャが構築されていると考えられます。
>
> Vercel では、 Serverless Functionsを使用した Node.js ランタイム (デフォルト)またはEdge Functionsを使用した Edge ランタイムのいずれかで Next.js アプリケーションをサーバー レンダリングできます。これにより、ページごとに最適なレンダリング戦略を選択できます。
参考 : <https://vercel.com/docs/frameworks/nextjs#server-side-rendering-ssr>
>
### アナリティクス

アナリティクスを提供しているが、1ヶ月という期間しか見れないようです。

**アナリティクスのパフォーマンスも高い**
> Vercel Web アナリティクスは**Google アナリティクスの 44 分の 1 のサイズ**なので、優れたサイト パフォーマンスを維持できます。
参考 : <https://vercel.com/blog/vercel-web-analytics-is-now-generally-available>
>

:::message
アナリティクスの部分は、より詳細にみれて無料であるSentryやDatadogにしてもいいかも知れません。
:::

## **GitHub Pages**

### 特徴

- 商用利用不可
- 開発者側でのヘッダー付与が不可(静的ホストしかできない)
- サーバーサイド言語のデプロイはできない

開発をGitHubで統一して行えるのは、開発効率も上がると思うのでメリットだと思います。

### 商用利用不可

商用利用が禁止されています。
>
>GitHub Pages は、オンライン ビジネス、eコマース サイト、主に商取引の円滑化またはサービスとしての商用ソフトウェア (SaaS) の提供のどちらかを目的とする、その他の Web サイトを運営するための無料の Web ホスティング サービスとしての使用を意図したものではなく、またそのような使用を許可するものでもありません。
>参考 : <https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages#prohibited-uses>

### 開発者側でのヘッダー付与が不可(静的ホストしかできない)

開発者側でのヘッダー付与が不可だと思われます。
<https://stackoverflow.com/questions/26416727/cross-origin-resource-sharing-on-github-pages>

よって、ヘッダーをカスタマイズしたい場合には向かないと考えられます。

しかし、CloudflareのようなCDN（コンテンツデリバリーネットワーク）サービスを使用することで、リバースプロキシを介してカスタムヘッダーを追加することが可能なようです。Cloudflareは、GitHub Pagesに対するリクエストを中継する際に、必要なヘッダーを付与できます。

やり方はありますが、ちょっと手間かかりそうですね。
:::message
自分はsqlite.wasmを利用したかったのですが、このヘッダー付与が難しそうだったのでGitHub Pagesの利用は断念しました。

> Warning
For this to work, you need to set the following headers on your server:
`Cross-Origin-Opener-Policy: same-origin`
`Cross-Origin-Embedder-Policy: require-corp
参考 : <https://github.com/sqlite/sqlite-wasm>

:::

**.htaccessをサポートしてない（たぶん）**
.htaccessの設定をいじることでカスタムヘッダーを利用できると思ったのですが、GitHub Pagesはその辺りをサポートしていないっぽいです。
公式ドキュメントでは触れられていないですが、そういった(古い)記事を見ます。

### サーバーサイド言語のデプロイはできない

Next.jsを静的ホストする場合に使えます。
> GitHub Pages は、PHP、Ruby、Python などのサーバーサイド言語はサポートしていません。
> 参考 : <https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages#static-site-generators>

### 参考

<https://github.com/orgs/community/discussions/23723>

## Cloudflare Pages

### 特徴

- 商用利用が可能
- 簡単デプロイ&セキュリティ意識が高い
- 帯域幅が無制限
- アナリティクス利用可
- 高パフォーマンス

商用利用が可能なホスティングサービスであり、Cloudflareの他サービスとの連携もできるのでセキュリティとパフォーマンスの2つを兼ねることが可能です。

### 商用利用が可能

公式もfreeプランでの商用利用を許可しています。

>![q](https://storage.googleapis.com/zenn-user-upload/e4fc46e38c69-20241102.png)
>![a](https://storage.googleapis.com/zenn-user-upload/c71926c361be-20241102.png)
>参考 : <https://community.cloudflare.com/t/is-cloudflare-pages-workers-free-plan-free-for-commercial-use/291741>

### 簡単デプロイ&セキュリティ意識が高い

Cloudflare Pagesは簡単にデプロイすることができ、WAFやCDNとも統合することが可能です。
また、HTTP/3、QUICなどもサポートし、画像圧縮やSSLもすぐ使えます。
>
> ![](https://storage.googleapis.com/zenn-user-upload/131fc43f2638-20241103.png)
> 参考 : <https://www.cloudflare.com/ja-jp/developer-platform/products/pages/>

### 帯域幅が無制限

ユーザーからのトラフィックが急増しても、帯域幅の問題で通信速度が落ちる心配はなくなります。
> ![帯域幅無制限](https://storage.googleapis.com/zenn-user-upload/f659105aeb04-20241103.png)
>参考 : <https://www.cloudflare.com/ja-jp/developer-platform/products/pages/>
>
### アナリティクス利用可

アナリティクス機能を無料で利用できます。

> Cloudflare Web Analytics は、DNS を変更したり Cloudflare のプロキシを使用したりすることなく、Web サイトのプライバシーを第一に考えた分析を無料で提供します。Cloudflare Web Analytics は、サイト訪問者が体験する Web ページのパフォーマンスを理解するのに役立ちます。
>参考 : <https://developers.cloudflare.com/pages/how-to/web-analytics/>

### 高パフォーマンス

Cloudflareは世界中にCDNエッジサーバーを配置しているため、パフォーマンスを高めることができます。

> ![Cloudflareエッジサーバー](https://storage.googleapis.com/zenn-user-upload/afe467c879a1-20241102.png)
> 参考 : <https://www.cloudflare.com/ja-jp/network/>

### 参考

<https://www.cloudflare.com/application-services/products/cdn/>
<https://developers.cloudflare.com/pages/how-to/web-analytics/>
<https://community.cloudflare.com/t/is-cloudflare-pages-workers-free-plan-free-for-commercial-use/291741>
<https://www.cloudflare.com/ja-jp/network/>

## Netlify

### 特徴

- 商用利用可
- 簡単デプロイ

調べると日本だと応答速度が遅いらしいという情報が検索で引っかかりました。
しかし、現在ではエッジサーバーはTokyoにある感じがするのでこの問題も解消されたのだと思っています。
> Netlify UI を通じて、リージョンを次のいずれかのリージョンに変更できます。
> ap-northeast-1 - アジア太平洋 (東京)
> 参考 : <https://docs.netlify.com/functions/optional-configuration/?fn-language=ts#region>

現状日本でNext.jsを商用利用したい&無料でホストする場合、Cloudflare Pagesがライバル候補になりそうです。

### 参考

<https://qiita.com/benjuwan/items/4a2f175b648791412203>

## Amplify

AWSサービスとの連携ができるのは強みだと思います。

### 特徴

- 簡単デプロイ
- 他AWSサービスとの連携

### 簡単デプロイ

Vercelにデプロイするのと同じノリでデプロイできます。

### 他AWSサービスとの連携

認証サービスであるAmazon Cognito、NoSQL データベースサービスのDynamoDB、オブジェクトストレージサービス（画像などを保存）であるS3などとの連携が手軽にできます。

ただ、コスト面がまだ調査不足で判明していないので後ほど追記します。
便利そうだけど、コストによるという感じになりそうです。この後紹介するCloud Runもそうですが、従量課金制なので気をつけて使いたいですね。

### 参考

<https://docs.amplify.aws/gen1/nextjs/prev/build-a-backend/auth/set-up-auth/>
<https://blog.ashcolor.jp/blog/programming/vercel-vs-amplify>
<https://docs.aws.amazon.com/ja_jp/amplify/latest/userguide/ssr-supported-features.html>

## Cloud Run

### 特徴

- 簡単デプロイ
- コンテナの知見と運用経験を得られる
- どんな言語でもOK
- 従量課金制
- オートスケーリング
- 他GCPサービスとの連携
- コンテナ構築が任意となっている
- コールドスタート

Cloud Runは、GCP(Google Cloud Platform)の提供するサービスの1種で、類似サービスはAWS Fargateです。
AWS Fargateはインフラを構築するのに学習コストがかかるほか、サーバー代も割とでかいです。
しかし、AWS Fargateと異なり、デプロイのしやすさと費用の観点でとても良いサービスなので、Cloud Runを今回紹介させていただきます。
料金はかかりますが、月数十円に抑えることも可能です。

コストのかかるAWS FargateやGKEでのサービス運用をいきなり始めるのではなく、まずCloud Runでの運用を選択する現場も増えてきているようです。

### 簡単デプロイ

一見するとデプロイが難しそうなサービスに見えますが、実際にはコンテナイメージをレジストリにプッシュし、Vercelのように画面でぽちぽち操作をするだけで簡単にデプロイできます。
デプロイはしやすいですが、今回比較している他サービスに比べると手間はかかってしまいます。

### コンテナの知見と運用経験を得られる

Cloud Runを使う場合、ある程度コンテナ技術への理解が必要です。
そのため、コンテナの学習、運用を経験するにはちょうどいい題材だと思います。

### どんな言語でもOK

Cloud Runはコンテナをベースとしているので、任意の言語でコードを作成でき、任意のバイナリやフレームワークを使用できます。
そのため、バックエンドでGoやRailsなどをデプロイしたいと言った場合にも活用できます。
> 任意の言語で書かれたコードのサポート : Cloud Run はコンテナをベースとしているので、任意の言語でコードを作成でき、任意のバイナリやフレームワークを使用できます。
> 参考 : <https://cloud.google.com/blog/ja/products/containers-kubernetes/when-to-use-google-kubernetes-engine-vs-cloud-run-for-containers>

### 従量課金制

必要な時に必要な分だけインスタンスを稼働させる仕組みなので、常にインスタンスを稼働させる必要がなく費用を抑えることができます。
リクエストがない場合には、インスタンスが起動しないので料金が発生しません。
> ゼロおよび最小インスタンスへのスケーリング
> 参考 : <https://cloud.google.com/run/docs/overview/what-is-cloud-run?hl=ja#scale-to-zero>

### オートスケーリング

インスタンスの数を自動調整することができ、リクエストが突然増えても処理することが可能です。
> ゼロおよび最小インスタンスへのスケーリング
>
>
> Cloud Run は、すべての受信リクエストを処理するため、また、[CPU 割り当て](https://cloud.google.com/run/docs/configuring/cpu-allocation?hl=ja)が `always on` に設定されている場合はリクエスト以外の CPU 使用率の増加に対応するため、[インスタンスを自動的に追加または削除](https://cloud.google.com/run/docs/about-instance-autoscaling?hl=ja)します。サービスに対する受信リクエストがない場合は、最後に残ったインスタンスまで削除されます。この動作は一般にゼロにスケーリングと呼ばれています。
>
> 参考 : <https://cloud.google.com/run/docs/overview/what-is-cloud-run?hl=ja#scale-to-zero>
>

### 他GCPサービスとの連携

他GCPサービスとの連携が可能であり、特にDBとして無料枠の大きいFirestoreを利用することができます。
AWS、GCPなどのCloudサービスは、特にDBの費用が大きいです。しかし、このDBの部分をFirestoreにすることでコストを最小限に抑えてサービスを運営していくことが可能になります。

ただ、 **FirestoreはNoSQLデータベース**なので、要件によっては合わないこともあるかもしれません。

> Google では、Google Cloud 上の他のサービスと連携できるように Cloud Run を構築しているため、さまざまな機能を備えたアプリケーションを構築できます。
>
>
> つまり、Cloud Run を使用すると、Cloud Run サービスの運用、構成、スケーリングに必要な時間がほとんどなくなるため、デベロッパーはコードの作成に時間を費やすことができます。クラスタの作成やインフラストラクチャの管理をすることなく Cloud Run で生産性を向上できます。
> 参考 : <https://cloud.google.com/run/docs/overview/what-is-cloud-run?hl=ja>
>

### GKEへの移行可能

サービスが拡大してきたらGKEへの移行もできます。

### コンテナ構築が任意となっている

> お好みの言語、フレームワーク、ライブラリを使用してコードを記述し、それをコンテナとしてパッケージ化して「gcloud run deploy」を実行すれば、本番環境での稼働に必要なものがすべて揃った状態でアプリがデプロイされます。コンテナの構築は完全に任意です。Go、Node.js、Python、Java、.NET Core、Ruby を使用している場合は、使用している言語のベスト プラクティスに従って、コンテナをビルドする[ソースベースのデプロイ](https://cloud.google.com/run/docs/deploying-source-code) オプションを使用できます。
参考 : <https://cloud.google.com/run?hl=ja>
>

### コールドスタート

コンテナの起動に時間がかかる(コールドスタート)ため、最初のリクエストに対する応答が遅くなることがあります。
> インスタンスは必要に応じてスケーリングされるため、起動時間がサービスのレイテンシに影響します。Cloud Run は、インスタンスの起動とリクエストの処理を切り離しますが、リクエストは新しいインスタンスが起動するまで待機してから処理されることがあります。これは特にゼロからスケーリングする場合に起こります。これは「コールド スタート」と呼ばれます。
> 参考 : <https://cloud.google.com/run/docs/tips/general?hl=ja#start_containers_quickly>

### 参考

<https://cloud.google.com/blog/ja/products/containers-kubernetes/when-to-use-google-kubernetes-engine-vs-cloud-run-for-containers>
<https://cloud.google.com/run?hl=ja>
<https://cloud.google.com/run/docs/overview/what-is-cloud-run?hl=ja>
<https://envader.plus/article/413>
**Cloud Runコストについて**
<https://cloud.google.com/run/pricing>
<https://zenn.dev/tellernovel_inc/articles/d200f595aa68e5>

## 類似の記事

<https://zenn.dev/knagano/scraps/d772707b4909b0>
<https://qiita.com/benjuwan/items/4a2f175b648791412203#netlify>
<https://zenn.dev/catnose99/scraps/6780379210136f>
