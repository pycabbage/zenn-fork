---
title: "【技術選定】　(個人開発者向け)　Next.jsをホストする代表的なサーバーを比較した"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Next.js","サーバー","Vercel","個人開発","技術選定"]
published: false
---
## 前提

VercelはNext.jsに最適化されたサーバーなので、迷ったらVercelを使いたいです。

公式ドキュメントを見ても見つけられなかったので、ここら辺の明確な根拠はありません。
しかし、**VercelとNext.jsは開発元が同じ**なので、Next.jsにホストするのに最適なインフラストラクチャが構築されていると考えられます。
何よりもNext.jsで破壊的な変更がこの先起こらないとも限りません。その時にいち早く対応するのは開発元が同じであるVercelなのは必然かなと思います。
よって、安定とパフォーマンスを選ぶならVercelが良いと考えています。

当然このあたりはサービスの要件によるとは思います。
Vercelを使っていた方もこの記事を見て、「CloudRunの方がいいんじゃないか？」「いいや、cloud Pagesだね」などなど、自分の最適を見つけていただければ嬉しいです。

**本記事ではフリープランで利用することを想定しています(CloudRun除く)。**

比較するホスティングサービス

- Github Pages (商用不可)
- Cloudflare Pages (商用可)
- Vercel (商用不可)
- Netlify (商用可) ?
- Amplify
- Cloud Run

:::message
有料にするくらいユーザーからのトラフィックがあるなら、Vercelの有料プランはどのみち必要になるかもしれないのでそこも考慮する必要があるかもしれない。
:::

## 知っておきたい用語

**.htaccess**

Webサーバーの動作をディレクトリ単位で制御することができるので、Github Pagesでカスタムヘッダーを付与することが可能かもしれないと思い、今回調査した。

**httpヘッダー**

CORSなどのヘッダーを付与し、セキュリティを高めることができる

REST fullに基づいたWeb APIで、httpヘッダーが利用される。カスタムヘッダーとして柔軟にヘッダーを活用してサーバー側にデータを送信することが可能になる。

慣習的にカスタムヘッダーはx-prefixを付与する

<https://apidog.com/jp/blog/how-to-check-http-headers/>

## **Github Pages**

**特徴**

- 商用利用不可
- 開発者側でのヘッダー付与が不可(静的ホストしかできない)
- 全てをgithubで統合できるので効率的に開発できる
- サーバーサイド言語のデプロイはできない
- Jeykyllという静的サイトジェネレーターがサーバー

### 商用利用不可

開発者側でのヘッダー付与が不可だと思われる。
<https://stackoverflow.com/questions/26416727/cross-origin-resource-sharing-on-github-pages>

### 開発者側でのヘッダー付与が不可(静的ホストしかできない)

ヘッダーをカスタマイズしたい場合には向かないと考えられます。

> Warning
For this to work, you need to set the following headers on your server:
`Cross-Origin-Opener-Policy: same-origin`
`Cross-Origin-Embedder-Policy: require-corp
参考 : <https://github.com/sqlite/sqlite-wasm>

**Cloudflare**のようなCDN（コンテンツデリバリーネットワーク）サービスを使用することで、プロキシを介してカスタムヘッダーを追加することが可能なようです。Cloudflareは、GitHub Pagesに対するリクエストを中継する際に、必要なヘッダーを付与できます。
やり方はあるが、ちょっと手間かかりそうです。

**.htaccessをサポートしてない（たぶん）**

.htaccessを利用することでカスタムヘッダーを利用できると思ったが、Github Pagesはその辺りをサポートしていないっぽいです。
公式ドキュメントでは触れられていないがそういった(古い)記事を見ます。

### サーバーサイド言語のデプロイはできない

Next.jsを静的ホストする場合に使えます。
> GitHub Pages は、PHP、Ruby、Python などのサーバーサイド言語はサポートしていません。

参考
 <https://docs.github.com/ja/pages/getting-started-with-github-pages/about-github-pages#static-site-generators>
>

参考

<https://github.com/orgs/community/discussions/23723>

## Cloudflare Pages

**特徴**

- 商用利用が可能
- cloudflareサービスを組み合わせて利用できる
- アナリティクス利用可能

商用利用が可能なホスティングサービス

### 商用利用が可能

公式も明確にfreeプランでも商用利用を許可している

>
>
>
> ![スクリーンショット 2024-10-20 13.36.15.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/a6013ad0-fe10-490f-aded-294bd615f82c/844f5520-0344-4750-b466-cebd7dd1360e/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2024-10-20_13.36.15.png)
>
> ![スクリーンショット 2024-10-20 13.34.57.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/a6013ad0-fe10-490f-aded-294bd615f82c/0118137c-69f6-4e7f-a5a0-4555f21a11fe/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2024-10-20_13.34.57.png)
>

### cloudflareサービスを組み合わせて利用できる

### アナリティクス利用可能

(アナリティクスの部分は、詳細にみれて無料であるsentryやdatadogにしてもいいかも)
無料でアナリティクス機能を利用できる

> Cloudflare Web Analytics は、DNS を変更したり Cloudflare のプロキシを使用したりすることなく、Web サイトのプライバシーを第一に考えた分析を無料で提供します。Cloudflare Web Analytics は、サイト訪問者が体験する Web ページのパフォーマンスを理解するのに役立ちます。
>
### 参考

<https://developers.cloudflare.com/pages/how-to/web-analytics/>
>

> 参考 : <https://community.cloudflare.com/t/is-cloudflare-pages-workers-free-plan-free-for-commercial-use/291741>
>

## Vercel

VercelはNext.jsと相性がいいのでパフォーマンスが高いと考えられます。

途中で商用利用したい場合には、cloudflare pagesへの移行も可能なので最初にVercelをホスト先にするのはありだと思います。

### アナリティクス

アナリティクスを提供しているが、1ヶ月という期間しか見れない。

freeプランは商用利用不可と記載されていますが、ホストしたWebサイトに**広告を貼ることは営利目的に当たらない**という話も見たのですがどうやらダメっぽいです

<https://vercel.com/docs/limits/fair-use-guidelines#commercial-usage>
<https://zenn.dev/link/comments/269bb2354e95ac>

アナリティクスのパフォーマンスも高い

> Vercel Web アナリティクスは**Google アナリティクスの 44 分の 1 のサイズな**ので、優れたサイト パフォーマンスを維持できます。
参考 : <https://vercel.com/blog/vercel-web-analytics-is-now-generally-available>
>

**ヘッダーのカスタマイズ**

httpヘッダーなどのカスタマイズが可能

<https://vercel.com/docs/functions/edge-middleware>

## Netlify

**特徴**

- 商用利用可
- 静的サイトのホスト用であって、サーバーサイド言語のデプロイは不可

日本だと応答速度が遅いらしい。

理由としては、日本にエッジサーバーがなく、シンガポールからの配信になるためレイテンシーが発生するというものです。しかし、情報源が古いのと、ここら辺のエッジサーバの情報が公式ドキュメントから見つけられなかったので詳細は不明。

エッジサーバーはTokyoにある。パフォーマンスは大丈夫そう?

関数だけ？

<https://docs.netlify.com/functions/optional-configuration/?fn-language=ts#region>

現状日本でNext.jsをホストする場合、Cloudflare Pagesが商用利用可能なサービスとしてライバル候補に上がる。商用利用したい&無料であれば、cloudflare pagesと比較になりそうです。

### 参考

<https://qiita.com/benjuwan/items/4a2f175b648791412203>

## Amplify

node.jsのバージョン

追加予定

AWSは他のサービスと連携できない

<https://docs.aws.amazon.com/ja_jp/amplify/latest/userguide/ssr-supported-features.html>

## Cloud Run

コンテナ構築が任意となっている

> お好みの言語、フレームワーク、ライブラリを使用してコードを記述し、それをコンテナとしてパッケージ化して「gcloud run deploy」を実行すれば、本番環境での稼働に必要なものがすべて揃った状態でアプリがデプロイされます。コンテナの構築は完全に任意です。Go、Node.js、Python、Java、.NET Core、Ruby を使用している場合は、使用している言語のベスト プラクティスに従って、コンテナをビルドする[ソースベースのデプロイ](https://cloud.google.com/run/docs/deploying-source-code) オプションを使用できます。
参考 : <https://cloud.google.com/run?hl=ja>
>

- 簡単にデプロイが可能
- オートスケーリング
- 他GCPサービスとの連携

### 簡単にデプロイが可能

類似サービスはAWSのECS on Fargateです。
ECS on Fargateはインフラを構築するのに学習コストがかかるほか、サーバー代も割とでかいです。
しかし、ECS on Fargateと異なり、デプロイのしやすさと費用の観点でCloud RunをNext.jsをホストできるサーバーの候補に入れさせていただきました。
料金はかかりますが、月数十円に抑えられるレベルです。

### オートスケーリング

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

### 参考

<https://cloud.google.com/run?hl=ja>
<https://cloud.google.com/run/docs/overview/what-is-cloud-run?hl=ja>
<https://envader.plus/article/413>

## 類似の記事

<https://zenn.dev/knagano/scraps/d772707b4909b0>
<https://qiita.com/benjuwan/items/4a2f175b648791412203#netlify>
