---
title: "(個人開発者向け)　Next.jsをホストする代表的なサーバーを比較"
emoji: "🕺"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Next.js","Netlify","Vercel","Github Pages","Cloudflare Pages","Cloud Run"]
published: true
---
## 前提

VercelはNext.jsに最適化されたサーバーなので、迷ったらVercelを使いたいです。

公式ドキュメントを見ても見つけられなかったので、ここら辺の明確な根拠はありません。
しかし、**VercelとNext.jsは開発元が同じ**なので、Next.jsにホストするのに最適なインフラストラクチャが構築されていると考えられます。
何よりもNext.jsで破壊的な変更がこの先起こらないとも限りません。その時にいち早く対応するのは開発元が同じであるVercelなのは必然かなと思います。
よって、安定とパフォーマンスを選ぶならVercelが良いと考えています。

しかし、このあたりはサービスの要件によると思います。
Vercelを使っていた方もこの記事を見て、「CloudRunの方がいいんじゃないか？」「いいや、cloud Pagesだね」などなど、自分の最適を見つけていただければ嬉しいです。

**本記事ではフリープランで利用することを想定しています(CloudRun除く)。**

比較するホスティングサービス

- Vercel (商用不可)
- Github Pages (商用不可)
- Cloudflare Pages (商用可)
- Netlify (商用可)
- Cloud Run (商用可)
- Amplify　追加予定

:::message
有料にするくらいユーザーからのトラフィックがある場合、Vercelの有料プランは必要になるかもしれないのでそこも考慮する必要があるかもしれません。
:::

## 知っておきたい用語

:::details .htaccess
Webサーバーの動作をディレクトリ単位で制御することができるので、Github Pagesでカスタムヘッダーを付与することが可能かもしれないと思い、今回調査しました。

:::

::: details httpヘッダー
CORSなどのヘッダーを付与し、セキュリティを高めることができます。

REST fullに基づいたWeb APIで、httpヘッダーが利用される。カスタムヘッダーとして柔軟にヘッダーを活用してサーバー側にデータを送信することが可能になります

<https://apidog.com/jp/blog/how-to-check-http-headers/>
:::

## Vercel

### 特徴

- 商用利用の不可
- Next.jsと開発元と同じ
- 高パフォーマンス
- アナリティクス（期限あり）

商用利用が不可ですが、デプロイもしやすいので初期リリース時にホストするのはありだと考えています。

### 商用利用不可

freeプランでは、Webサイトに広告を貼るなどの行為を禁止しています。

>商用利用
趣味のチームは非営利の個人使用のみに制限されています。プラットフォームを商用目的で使用する場合は、Pro プランまたは Enterprise プランのいずれかが必要です。
>参考 : <https://vercel.com/docs/limits/fair-use-guidelines#commercial-usage>
VercelはNext.jsと相性がいいのでパフォーマンスが高いと考えられます。

:::message
途中で商用利用したい場合には、cloudflare pages(商用可)への移行も可能なので最初にVercelをホスト先にするのはありだと思います。
:::

### Next.jsと開発元と同じ

 Next.jsと開発元と同じなので、Next.jsに大きな変更が起きてもいち早く対応されると考えられます。

### 高パフォーマンス

Nextjsに最適化されたインフラストラクチャが構築されていると考えられます。
>
> Vercel では、 Serverless Functionsを使用した Node.js ランタイム (デフォルト)またはEdge Functionsを使用した Edge ランタイムのいずれかで Next.js アプリケーションをサーバー レンダリングできます。これにより、ページごとに最適なレンダリング戦略を選択できます。
参考 : <https://vercel.com/docs/frameworks/nextjs#server-side-rendering-ssr>
>
### アナリティクス

アナリティクスを提供しているが、1ヶ月という期間しか見れないようです。

**アナリティクスのパフォーマンスも高い**
> Vercel Web アナリティクスは**Google アナリティクスの 44 分の 1 のサイズな**ので、優れたサイト パフォーマンスを維持できます。
参考 : <https://vercel.com/blog/vercel-web-analytics-is-now-generally-available>
>

## **Github Pages**

### 特徴

- 商用利用不可
- 開発者側でのヘッダー付与が不可(静的ホストしかできない)
- サーバーサイド言語のデプロイはできない

開発をGithubで統一して行えるのは、開発効率も上がると思うのでメリットだと思います。

### 商用利用不可

商用利用が禁止されています。
>
>GitHub Pages は、オンライン ビジネス、eコマース サイト、主に商取引の円滑化またはサービスとしての商用ソフトウェア (SaaS) の提供のどちらかを目的とする、その他の Web サイトを運営するための無料の Web ホスティング サービスとしての使用を意図したものではなく、またそのような使用を許可するものでもありません。
>参考 : <https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages#prohibited-uses>

### 開発者側でのヘッダー付与が不可(静的ホストしかできない)

開発者側でのヘッダー付与が不可だと思われます。
<https://stackoverflow.com/questions/26416727/cross-origin-resource-sharing-on-github-pages>

よって、ヘッダーをカスタマイズしたい場合には向かないと考えられます。

しかし、CloudflareのようなCDN（コンテンツデリバリーネットワーク）サービスを使用することで、プロキシを介してカスタムヘッダーを追加することが可能なようです。Cloudflareは、GitHub Pagesに対するリクエストを中継する際に、必要なヘッダーを付与できます。

やり方はありますが、ちょっと手間かかりそうですね。
:::message
自分はsqlite.wasmを利用したかったのですが、このヘッダー付与が難しそうだったのでGithub Pagesの利用は断念しました。

> Warning
For this to work, you need to set the following headers on your server:
`Cross-Origin-Opener-Policy: same-origin`
`Cross-Origin-Embedder-Policy: require-corp
参考 : <https://github.com/sqlite/sqlite-wasm>

:::

**.htaccessをサポートしてない（たぶん）**
.htaccessの設定をいじることでカスタムヘッダーを利用できると思ったのですが、Github Pagesはその辺りをサポートしていないっぽいです。
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
- アナリティクス利用可能
- 高パフォーマンス

商用利用が可能なホスティングサービスであり、cloudflareの他サービスとの連携もできるのでセキュリティとパフォーマンスの2つを兼ねることが可能です。

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
### アナリティクス利用可能

(アナリティクスの部分は、詳細にみれて無料であるsentryやdatadogにしてもいいかも)
無料でアナリティクス機能を利用できる

> Cloudflare Web Analytics は、DNS を変更したり Cloudflare のプロキシを使用したりすることなく、Web サイトのプライバシーを第一に考えた分析を無料で提供します。Cloudflare Web Analytics は、サイト訪問者が体験する Web ページのパフォーマンスを理解するのに役立ちます。
>参考 : <https://developers.cloudflare.com/pages/how-to/web-analytics/>

### 高パフォーマンス

Cloudflareは世界中にCDNエッジサーバーを配置しているため、パフォーマンスを高めることができます。

> ![cloudflareエッジサーバー](https://storage.googleapis.com/zenn-user-upload/afe467c879a1-20241102.png)
> 参考 : <https://www.cloudflare.com/ja-jp/network/>

### 参考

<https://www.cloudflare.com/application-services/products/cdn/>
<https://developers.cloudflare.com/pages/how-to/web-analytics/>
<https://community.cloudflare.com/t/is-cloudflare-pages-workers-free-plan-free-for-commercial-use/291741>
<https://www.cloudflare.com/ja-jp/network/>

## Netlify

**特徴**

- 商用利用可

調べると日本だと応答速度が遅いらしいという情報が検索で引っかかりました。
しかし、現在ではエッジサーバーはTokyoにある感じがするのでこの問題も解消されたのだと思っています。
> Netlify UI を通じて、リージョンを次のいずれかのリージョンに変更できます。
> ap-northeast-1 - アジア太平洋 (東京)
> 参考 : <https://docs.netlify.com/functions/optional-configuration/?fn-language=ts#region>

現状日本でNext.jsを商用利用したい&無料でホストする場合、Cloudflare Pagesがライバル候補になりそうです。

### 参考

<https://qiita.com/benjuwan/items/4a2f175b648791412203>

## Cloud Run

### 特徴

- 簡単デプロイ
- 底コスト
- オートスケーリング
- 他GCPサービスとの連携
- コンテナ構築が任意となっている

### 簡単デプロイ

類似サービスはAWSのECS on Fargateです。
ECS on Fargateはインフラを構築するのに学習コストがかかるほか、サーバー代も割とでかいです。
しかし、ECS on Fargateと異なり、デプロイのしやすさと費用の観点でCloud RunをNext.jsをホストできるサーバーの候補に入れさせていただきました。
料金はかかりますが、月数十円に抑えられるレベルです。

### 底コスト

必要な時に必要な分だけインスタンスを稼働するような仕組みなので、ECS on Fargateのように常にインスタンスを稼働させる必要がなく費用を抑えることができます。
> ゼロおよび最小インスタンスへのスケーリング
> 参考 : <https://cloud.google.com/run/docs/overview/what-is-cloud-run?hl=ja#scale-to-zero>

### オートスケーリング

インスタンスの数を自動で調整することができ、リクエストが突然増えても処理することが可能です。
> ゼロおよび最小インスタンスへのスケーリング
>
>
> Cloud Run は、すべての受信リクエストを処理するため、また、[CPU 割り当て](https://cloud.google.com/run/docs/configuring/cpu-allocation?hl=ja)が `always on` に設定されている場合はリクエスト以外の CPU 使用率の増加に対応するため、[インスタンスを自動的に追加または削除](https://cloud.google.com/run/docs/about-instance-autoscaling?hl=ja)します。サービスに対する受信リクエストがない場合は、最後に残ったインスタンスまで削除されます。この動作は一般にゼロにスケーリングと呼ばれています。
>
> 参考 : <https://cloud.google.com/run/docs/overview/what-is-cloud-run?hl=ja#scale-to-zero>
>

### 他GCPサービスとの連携

> Google では、Google Cloud 上の他のサービスと連携できるように Cloud Run を構築しているため、さまざまな機能を備えたアプリケーションを構築できます。
>
>
> つまり、Cloud Run を使用すると、Cloud Run サービスの運用、構成、スケーリングに必要な時間がほとんどなくなるため、デベロッパーはコードの作成に時間を費やすことができます。クラスタの作成やインフラストラクチャの管理をすることなく Cloud Run で生産性を向上できます。
> 参考 : <https://cloud.google.com/run/docs/overview/what-is-cloud-run?hl=ja>
>

### コンテナ構築が任意となっている

> お好みの言語、フレームワーク、ライブラリを使用してコードを記述し、それをコンテナとしてパッケージ化して「gcloud run deploy」を実行すれば、本番環境での稼働に必要なものがすべて揃った状態でアプリがデプロイされます。コンテナの構築は完全に任意です。Go、Node.js、Python、Java、.NET Core、Ruby を使用している場合は、使用している言語のベスト プラクティスに従って、コンテナをビルドする[ソースベースのデプロイ](https://cloud.google.com/run/docs/deploying-source-code) オプションを使用できます。
参考 : <https://cloud.google.com/run?hl=ja>
>

### 参考

<https://cloud.google.com/run?hl=ja>
<https://cloud.google.com/run/docs/overview/what-is-cloud-run?hl=ja>
<https://envader.plus/article/413>

## Amplify

### 特徴

追加予定

- node.jsのバージョン
- AWSは他のサービスと連携できない

<https://docs.aws.amazon.com/ja_jp/amplify/latest/userguide/ssr-supported-features.html>

## 類似の記事

<https://zenn.dev/knagano/scraps/d772707b4909b0>
<https://qiita.com/benjuwan/items/4a2f175b648791412203#netlify>
<https://zenn.dev/catnose99/scraps/6780379210136f>
