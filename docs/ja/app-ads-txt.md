---
title: "app-ads.txt 1.0"
description: "モバイルアプリ向けのads.txt仕様。アプリ内広告における認定販売者の関係を明確にし、アプリ広告の透明性を確保します。"
---
Final specification version 1.0 March 2019

# About ads.txt and app-ads.txt (ads.txt と app-ads.txt について)

ads.txt 仕様は 2017 年春に開発され、デスクトップおよびモバイルウェブインベントリをカバーしています。このドキュメントでは、モバイルアプリストア、コネクテッドテレビアプリストア、およびその他同様の配信チャネルを通じて配布されるソフトウェアアプリケーションの要件を満たすための、元の ads.txt 標準の拡張について説明します。Authorized Sellers for Apps (app-ads.txt) は、OpenRTB ワーキンググループの支援を受けて開発された、ピアレビュー済みの標準規格です。本ドキュメントおよび補足の ads.txt 仕様は、[https://iabtechlab.com/ads-txt](https://iabtechlab.com/ads-txt) で入手可能です。

この仕様は、モバイルアプリにおける ads.txt 機能の必要性に対応しています。この仕様は、将来的にアプリが ads.cert やその他のウェブベースのリソースを実装できるようにする可能性も持っています。

# About the IAB Technology Lab (IAB Technology Lab について)

IAB Technology Laboratory (Tech Lab) は、効果的で持続可能なグローバルデジタルメディアエコシステムの成長を促進するための標準、ソフトウェア、およびサービスを作成・提供する、非営利の研究開発コンソーシアムです。デジタルパブリッシャー、アドテクノロジー企業、マーケター、代理店、およびインタラクティブマーケティング分野に関心を持つその他の企業で構成される IAB Tech Lab は、透明で安全かつ効果的なサプライチェーン、よりシンプルで一貫性のある測定、そして消費者にとってより良い広告体験を通じて、ブランドとメディアの成長を可能にすることを目指しており、特にモバイルおよびテレビ/デジタルビデオチャネルの活性化に注力しています。IAB Tech Lab のポートフォリオには、消費者、パブリッシャー、広告主、およびサードパーティプラットフォームのデジタル体験を向上させるために設計された DigiTrust リアルタイム標準化 ID サービスが含まれます。理事会メンバーには、AppNexus、ExtremeReach、Google、GroupM、Hearst Digital Media、Integral Ad Science、Index Exchange、LinkedIn、MediaMath、Microsoft、Moat、Pandora、PubMatic、Rakuten、Quantcast、Telaria、The Trade Desk、Yahoo! Japan が含まれます。

2014 年に設立された IAB Tech Lab は、ニューヨーク市に本社を置き、サンフランシスコにオフィス、シアトルとロンドンに代表部を構えています。

IAB Tech Lab の詳細については、[www.iabtechlab.com](http://www.iabtechlab.com/) をご覧ください。

### Authors:

Curtis Light, Staff Software Engineer, Google Curt Larson, Chief Product Officer, Sharethrough

### Other Significant Contributions Include:

Duke Dukellis, Director, Product Management, Google; Ian Trider, Director, RTB Platform Operations, Centro; Jan Winkler, Executive Director, AdSpirit; Jim Butler, Chief Technology Officer, Global Supply Platforms, Verizon Media Group / Oath; Jud Spencer, Principal Lead

Software Engineer, The Trade Desk; Madeleine Gordon, Technical Writer, Google; Neal Richter, CTO, Rakuten Marketing, and IAB Tech Lab OpenRTB Co-Chair; Per Bjorke, Senior Product Manager, Google; Sam Tingleff, Chief Technology Officer, IAB Tech Lab; Sergio Serra, Senior Product Manager, InMobi

### IAB Tech Lab Contact:

Jennifer Derke, Director of Product, Programmatic & Data, IAB Tech Lab openRTB@iabtechlab.com

#### Contributors and Technical Governance (貢献者および技術ガバナンス)

[OpenRTB Working Group](https://iabtechlab.com/working-groups/openrtb-working-group/) メンバーは ads.txt イニシアチブへの貢献を提供しています。OpenRTB ワーキンググループの参加者は、IAB Tech Lab のメンバーでなければなりません。プロジェクトの技術ガバナンスとコードコミットは、IAB Tech Lab OpenRTB Commit Group によって提供されます。

### License (ライセンス)

OpenRTB Specification the IAB Tech Lab is licensed under a Creative Commons Attribution 3.0 License. To view a copy of this license, visit [https://creativecommons.org/licenses/by/3.0/](https://creativecommons.org/licenses/by/3.0/) or write to Creative Commons, 171 Second Street, Suite 300, San Francisco, CA 94105, USA.

![CC by 3.0](https://i.creativecommons.org/l/by/3.0/88x31.png)

### Disclaimer (免責事項)

THE STANDARDS, THE SPECIFICATIONS, THE MEASUREMENT GUIDELINES, AND ANY OTHER MATERIALS OR SERVICES PROVIDED TO OR USED BY YOU HEREUNDER (THE “PRODUCTS AND SERVICES”) ARE PROVIDED “AS IS” AND “AS AVAILABLE,” AND IAB TECHNOLOGY LABORATORY, INC. (“TECH LAB”) MAKES NO WARRANTY WITH RESPECT TO THE SAME AND HEREBY DISCLAIMS ANY AND ALL EXPRESS, IMPLIED, OR STATUTORY WARRANTIES, INCLUDING, WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AVAILABILITY, ERROR-FREE OR UNINTERRUPTED OPERATION, AND ANY WARRANTIES ARISING

FROM A COURSE OF DEALING, COURSE OF PERFORMANCE, OR USAGE OF TRADE. TO THE EXTENT THAT TECH LAB MAY NOT AS A MATTER OF APPLICABLE LAW DISCLAIM ANY IMPLIED WARRANTY, THE SCOPE AND DURATION OF SUCH WARRANTY WILL BE THE MINIMUM PERMITTED UNDER SUCH LAW. THE PRODUCTS AND SERVICES DO NOT CONSTITUTE BUSINESS OR LEGAL ADVICE. TECH LAB DOES NOT WARRANT THAT THE PRODUCTS AND SERVICES PROVIDED TO OR USED BY YOU HEREUNDER SHALL CAUSE YOU AND/OR YOUR PRODUCTS OR SERVICES TO BE IN COMPLIANCE WITH ANY APPLICABLE LAWS, REGULATIONS, OR SELF-REGULATORY FRAMEWORKS, AND YOU ARE SOLELY RESPONSIBLE FOR COMPLIANCE WITH THE SAME, INCLUDING, BUT NOT LIMITED TO, DATA PROTECTION LAWS, SUCH AS THE PERSONAL

INFORMATION PROTECTION AND ELECTRONIC DOCUMENTS ACT (CANADA), THE DATA PROTECTION DIRECTIVE (EU), THE E-PRIVACY DIRECTIVE (EU), THE GENERAL DATA PROTECTION REGULATION (EU), AND THE E-PRIVACY REGULATION (EU) AS AND WHEN THEY BECOME EFFECTIVE.

# Abstract (概要)

Authorized Sellers for Apps (app-ads.txt) は、本来ウェブ広告インベントリを保護するために設計された [Authorized Digital Sellers](https://iabtechlab.com/ads-txt/) [(ads.txt) 標準](https://iabtechlab.com/ads-txt/) の拡張です。これは、オンラインアプリストアを通じて配信されるアプリをサポートするように互換性を拡張し、アプリストアのリスティングをアプリ開発者のウェブサイトにリンクさせます。

これを実現するために、アプリストアのリストページからアプリ開発者のウェブサイト URL を取得するための標準プロトコルを概説します。これは、ストア側の実装負担を最小限に抑えるように設計されています。開発者のウェブサイト上の app-ads.txt ファイルで承認を公開するアプリ開発者は、この構成を、開発者が独自に管理するオンラインリソースに集約します。開発ドメインを使用することで、ユニバーサルな名前空間が作成され、承認されていない開発者のなりすましの特定とブロックに役立つ可能性があります。

このアプリと開発者ドメインのリンクを提供することを除けば、参加者は、ドメインと承認されたセラーの強制処理を、ウェブインベントリ向けの ads.txt で使用されているものとほぼ同一であると見なすべきです（サブドメインの処理に関する例外を除く）。

# Definitions (定義)

**Authorized seller verifier (承認されたセラーの検証者)**: バイヤーやセラーの広告プラットフォームなど、一部の広告インベントリの承認されたセラーのステータスを確認するエンティティ。

**App metadata (アプリのメタデータ)**: アプリストアで入手可能なアプリに関する情報。これには、アプリアイコン、名前、説明、スクリーンショット、およびウェブサイトを含む開発者情報などが含まれます。通常、アプリストアはストアのウェブサイト内にこの情報を提供するページを提供します。

**bundle_id**: アプリに固有であり、配布されたアプリストアやインベントリが取引されるエクスチェンジに関係なく独立していることを意図した、プラットフォーム固有のアプリケーション識別子。Android では、これはバンドルまたはパッケージ名であるべきです（例：`com.foo.mygame`）。iOS では、同様のパターンに従います（例：`com.apple.mobilenotes`）。なお、OpenRTB 2.5 および AdCOM 1.0 の App オブジェクトでは、`bundle_id` は「bundle」という名前になっています。

**store_id**: 特定のストア内でのアプリの場所を特定するために使用される、在庫管理単位 (SKU) またはその他の識別子を表すアプリストア固有の識別子。たとえば、`B00BN3YZM2` のような Amazon Stock Identification Number (ASIN)、あるいは `1110145109` のような iTunes の数値ストア ID がこれにあたります。（なお、`store_id` は OpenRTB 2.5 以下の App オブジェクトの「bundle」フィールドで渡される場合もあります。AdCOM 1.0 では、App オブジェクトの「storeid」フィールドにあります。）

**storeurl**: OpenRTB ビッドリクエストの App オブジェクトで提供されるインストール済みアプリのアプリストア URL であり、IQG 2.1 コンプライアンスに必要です。たとえば、ビッドリクエストには、Google Play にリストされている Android アプリの場合は https://play.google.com/store/apps/details?id=com.google.android.deskclock、Apple iTunes ストアにリストされている iOS アプリの場合は https://itunes.apple.com/us/app/id1110145109、Roku Channel Store にリストされているコネクテッド TV アプリの場合は https://channelstore.roku.com/details/151908/the-roku-channel の `storeurl` がリストされる場合があります。

*bundle_id、store_id、および storeurl の関係に関する注記: Amazon や Apple iTunes アプリストアの場合、storeurl に store_id が含まれますが（例:* [*https://www.amazon.com/Amazon-App-Tester/dp/B00BN3YZM2）、*](https://www.amazon.com/Amazon-App-Tester/dp/B00BN3YZM2%29) *これはすべてのアプリストアに当てはまるわけではありません。たとえば、Google Play アプリストアの storeurl には store_id ではなく bundle_id が含まれています。実装者は store URL を不透明な値として扱うべきであり、この仕様を使用する目的で URL パラメータの内容から構造を解釈することは推奨されません。*

# Introduction (はじめに)

このドキュメントを読む前に、[https://iabtechlab.com/ads-txt/](https://iabtechlab.com/ads-txt/) にある主要な ads.txt 仕様に精通することをお勧めします。このドキュメントは ads.txt 仕様で概説されている詳細に大きく依存しているためです。

Authorized Sellers for Apps (app-ads.txt) 仕様は、以下のプロセスを詳述します：

* アプリ開発者は、アプリのストアメタデータでウェブサイト URL を提供し、そのウェブサイト上でアプリの広告インベントリの承認されたセラーをリストした app-ads.txt ファイルを公開します。
* アドネットワーク/セルサイドプラットフォームは、承認されたセラーステータスの強制を容易にするために、ビッドリクエストでストアリストの URL を提供します。
* アプリストアは、クロールおよび構造化データとしての解析を可能にするために、アプリのストアリストページ上の標準 HTML `<meta>` タグでアプリのメタデータを公開します。
* 承認されたセラーの検証者は、アプリストアをクロールして開発者ウェブサイト情報を見つけ、開発者ウェブサイトをクロールして app-ads.txt ファイルを取得・解釈し、インベントリに対する承認ステータスを強制します。

[Resource Description Framework in attributes](https://en.wikipedia.org/wiki/RDFa) (RDFa) W3C 勧告および [Open Graph protocol](http://ogp.me/) がこの仕様に影響を与えました。

# Solution specification (ソリューション仕様)

以下は、アプリ開発者、アドネットワーク/セルサイドプラットフォーム、バイサイドプラットフォーム、およびアプリストアに対する要件を規定します。

## App developers (アプリ開発者)

アプリ開発者は、アプリに app-ads.txt を採用するために以下の手順に従わなければなりません（MUST）。

### Provide developer website URL in app store listings (アプリストアリストで開発者ウェブサイト URL を提供する)

この仕様は、アプリを配布しているすべてのアプリストア内のアプリのストアリストメタデータ内に、開発者ウェブサイト URL が存在することに依存しています。多くのアプリストアは現在、開発者の連絡先情報としてストア内に表示するために、開発者のウェブサイト URL を収集しています。

ウェブサイトを公開し、その URL を提供することは、アプリの広告インベントリが承認されたセラースキームに参加するために必須（REQUIRED）です。

このウェブサイト URL を使用して、関心のあるクローラーはパスを導出し、対応するドメイン上の app-ads.txt ファイルのクロールを試みます。検証者が公開された開発者 URL から `/app-ads.txt` パスの場所を導出する方法の詳細な説明については、[Translate developer URL to an app-ads.txt path](#translate-developer-url-to-an-app-adstxt-path) セクションを参照してください。また、開発者ウェブサイト URL が app-ads.txt URL に変換される例や、ファイルの検索においてサブドメインが検索される順序については、[Appendix B](#appendix-b-developer-url-to-app-adstxt-file-url-test-cases) を参照してください。

### Publish an app-ads.txt file (app-ads.txt ファイルを公開する)

ウェブ向けの ads.txt ファイルの適切な形式と内容に関する完全な詳細については、[https://iabtechlab.com/ads-txt/](https://iabtechlab.com/ads-txt/) にある主要な ads.txt 標準を参照してください。ads.txt 仕様と同じガイドラインを使用しますが、app-ads.txt ファイルでは `subdomain` ディレクティブは使用されず、遭遇した場合は無視されるべきである（SHOULD）という例外があります。

ファイル名は `ads.txt` ではなく `app-ads.txt` です。これにより、アプリとウェブの構成が別々に管理され、互いに競合が生じないようになります。アプリがウェブとは異なる導入モデルを持っているという性質上、この柔軟性により、1 つの統合ファイルにエントリをまとめる場合と比較して、採用と保守が容易になると予想されます。

### Changing the developer website URL for an app (アプリの開発者ウェブサイト URL の変更)

アプリストアへの負担を軽減するため、この仕様では、クローラーに対してストアウェブサイトのクロール頻度を制限するよう求めています。開発者は、開発者 URL ドメインへの変更が、関心のある承認されたセラーの検証者によって認識されるまでに時間がかかる場合があることを予想するべきです（SHOULD）。ドメインを変更する場合、可能であれば、古いドメインからファイルを削除したり、古い場所から必要なエントリを削除したりする前に、関連するエントリを含む app-ads.txt ファイルを古いドメインと新しいドメインの両方で長期間ホストすることをお勧めします（RECOMMENDED）。

### Optionally indicating that there are no authorized sellers (オプションで承認されたセラーがいないことを示す)

一部の開発者は、app-ads.txt ファイルによって許可される承認されたセラーをアプリに持たせないことを選択する場合があります。検証者が空の app-ads.txt ファイルを適切に読み取り解釈できるように、[ads.txt 仕様のガイダンス](http://iabtechlab.com/ads-txt)（承認された広告システムレコードを含まないファイルの要件を記述している）に従ってください。

## Ad networks/sell-side platforms (aka “bid request issuers”) (アドネットワーク/セルサイドプラットフォーム（別名「ビッドリクエスト発行者」）)

RTB ビッドリクエストを発行するアドネットワークおよびセルサイドプラットフォーム（SSP）は、インベントリがこの仕様に従って承認されたものとして扱われるために、以下のようにアプリの配信チャネルを示さなければなりません（MUST）。

### Include the storeurl parameter within bid requests (ビッドリクエスト内に storeurl パラメータを含める)

TAG Inventory Quality Guidelines は、アドネットワーク、アドエクスチェンジ、およびセルサイドプラットフォームに対し、インプレッションを提供しているアプリに対応する個々のストアリストを示すストア URL を提供することを要求しています。現在この値を提供していないサプライサイドプラットフォームまたはエクスチェンジは、app-ads.txt 要件に準拠するために提供しなければなりません（MUST）。独自インベントリの承認されたセラーチェックを実行するアドネットワークは、検証プロセス内でアプリストア URL を利用しなければなりません（MUST）。

## App stores (アプリストア)

アプリストアは、app-ads.txt 標準を促進するために、以下の機能をサポートするよう求められます。

### Publish structured app information (構造化されたアプリ情報を公開する)

承認されたセラーの検証者を支援するために、アプリストアに対し、個々のアプリのストアリストページとともに 3 つの HTML `<meta>` タグを公開することを要求します：

* アプリ開発者のウェブサイト URL（現在は多くの場合、ストアリストページ上のユーザーがクリック可能なリンクとして提供されています）
* アプリの `bundle_id`
* アプリの `store_id`

アプリストアのアプリメタデータから `bundle_id` および/または `store_id` を取得する目的は、それがビッドリクエスト内の `bundle_id` および/または `store_id` と一致するかどうかをクロスチェックすることです。アプリストアは、そのリストに対して `developer_url` が提供されたかどうかに関係なく、すべてのアプリリストに対して `bundle_id` および `store_id` の meta タグを常に公開することが求められます（REQUESTED）。これにより、アプリストアはそのストアリスト URL が特定のバンドル ID/ストア ID に対して正当なものであることを表明でき、承認されたセラーの検証者が、特定のアプリが app-ads.txt に参加していないことを確認するのに役立ちます。

アプリストアは、HTML ドキュメントの冒頭にある `<head>` HTML タグ内にこれらのタグを挿入し、適切な値を content 属性に含めることで、以下のように HTML meta タグをフォーマットしなければなりません（MUST）：

```
<meta name="appstore:developer_url" content="https://www.path.to/page" />
<meta name="appstore:bundle_id" content="com.example.myapp" />
<meta name="appstore:store_id" content="SKU12345" />
```

このソリューションは、[Open Graph プロトコル](http://ogp.me/)や [Twitter マークアップタグ](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/overview/markup.html)に似ており、フィールドの目的を示すために `appstore:` プレフィックスが使用されています。これらの名前は [WHATWG Wiki MetaExtensions](https://wiki.whatwg.org/wiki/MetaExtensions) ページに登録されています。Twitter の仕様と同様に、プレフィックスに対して正式なコンパクト名前空間 ([CURIE](https://en.wikipedia.org/wiki/CURIE)) を定義することは要求しません。アプリストアは、[`<meta>` タグに関する W3C 標準](https://www.w3.org/TR/html5/document-metadata.html#the-meta-element)および周辺ドキュメントに従って有効な HTML を生成するものと想定されています。ページが参加していると認識されるためには、アプリストアは `developer_url` meta タグに加えて、ストアに適用可能な `bundle_id` および/または `store_id` meta タグを含めなければなりません（MUST）。アプリに URL が提供されていない場合は、`developer_url` meta タグの content 属性に空の値を使用してください。

## Authorized seller verifiers (承認されたセラーの検証者)

情報提供、レポート、または強制の理由で承認されたセラーステータスを確認したいエンティティは、以下の手順に従うべきです（SHOULD）。これらの手順は、セルサイドプラットフォームからエクスチェンジ、バイサイドプラットフォームに至るまで、エコシステムのすべての関係者に適用されます。

### Identify app store listing URLs for apps offering inventory (インベントリを提供するアプリのアプリストアリスト URL を特定する)

承認されたセラーの検証者は、検証したいインベントリに適したアプリストアリスト URL を決定するべきです（SHOULD）。OpenRTB の場合、以前に確認されたビッドリクエストから `storeurl` フィールドを読み取ります。非 OpenRTB インベントリの場合、独自のソリューションに適した方法を使用してください。

### Crawl app listing pages in app stores (アプリストア内のアプリリストページをクロールする)

対象の `storeurl` 値で指定された HTML ページをクロールします。値を抽出するために適切な HTML 解析ソリューションを使用して、上記の [App Stores](#app-stores) セクションで説明されている HTML `<meta>` タグから `developer_url`、`store_id`、および `bundle_id` プロパティを取得します。

一意のアプリストア URL が毎週 1 回以下の頻度でクロールされるようにクロールを制限し、ストアの robots.txt ファイルの制約を尊重してください（MUST）。検証者は、ストアの全インベントリをクロールするのではなく、検証者が積極的に広告インプレッションの機会を受け取っているアプリのリストのみをクロールするべきです（SHOULD）。最初の app-ads.txt 採用期間を除けば、開発者がアプリ開発者 URL を頻繁に変更することは予想されず、多くの URL は変更されるとしても稀でしょう。

リソースの効率化と開発者の利便性のため、アプリストアまたはサードパーティの集約サービスは、これらの URL を取得するためのバルク転送ソリューションを提供する API/ファイル形式を提供する場合があります。これらの代替的な独自ソリューションは歓迎されますが、このサービスを提供するファーストパーティまたはサードパーティのソリューションは、標準のアプリストア URL の場所で表示されるのと同じ開発者 URL、バンドル ID、およびストア ID データを表面化させなければなりません（MUST）。

### Translate developer URL to an app-ads.txt path (開発者 URL を app-ads.txt パスへ変換する)

以下の手順に従って、開発者 URL を app-ads.txt ファイルを見つけるためのクロール先パスに変換します。

1. URL のホスト名部分を抽出します。
2. 標準の [public suffix](https://publicsuffix.org/list/) の前にあるホスト名から、最初の（存在する場合は 2 番目の）名前以外をすべて削除します。例：
    1. `example.com` は単に `example.com` のまま
    2. `subdomain.example.com` は `subdomain.example.com` のまま
    3. `another.subdomain.example.com` は `subdomain.example.com` になる
    4. `another.subdomain.example.co.uk` は `subdomain.example.co.uk` になる
3. ホスト名に残っている `www.` または `m.` プレフィックスをすべて削除します。
4. そのパスに `/app-ads.txt` を追加します。
5. クローラーは、最初に URL の HTTPS バージョンの取得を試み、SSL が利用できない場合は HTTP バージョンにフォールバックするべきです（SHOULD）。

ドメインを正規化する際は、標準のパブリックサフィックスの適切な処理を確実に行うようにしてください。[publicsuffix.org ウェブサイト](https://publicsuffix.org/learn/)には、ドメイン解析を支援するために使用を検討できるさまざまな言語のソフトウェアライブラリへのリンクが含まれていますが、実装者はライブラリで使用されるサフィックスリストが最新であることを確認するべきです（SHOULD）。適切な解析シナリオの例をカバーしている付録のテストケースを参照してください。検証者は、上記のドメイン正規化ルールに従ってサブドメインで見つかった app-ads.txt ファイルを使用しなければならず（MUST）、そのサブドメインでファイルが見つからない場合にのみ、そのサブドメインの親で見つかった app-ads.txt ファイルをデフォルトとして使用します。

### Crawl and interpret app-ads.txt file (app-ads.txt ファイルをクロールし解釈する)

app-ads.txt ファイルの構造と内容はウェブファイル用の ads.txt と同じであり、[確立された ads.txt 標準](https://iabtechlab.com/ads-txt/)に従うべきです（SHOULD）。ウェブ強制ソリューション向けにすでに ads.txt を実装しているプラットフォームは、このインフラストラクチャをわずかな変更で app-ads.txt に再利用できるはずです。

### Requirements for implementing advertising systems (広告システム実装の要件)

承認ステータスを確認するために使用されるアカウント識別子を見つけるための OpenRTB `publisher.id` フィールドの利用に関して、元の ads.txt 仕様のガイドラインに従ってください。その後、上記の手順に従って app-ads.txt ファイルを見つけ、クロールし、解釈します。承認されたセラーのステータスを検証するセラーおよびバイヤーシステムは、一般にウェブベースのインベントリと同じアプローチに従いますが、上記で説明した app-ads.txt ファイルを見つける方法は例外です。

### Authoritative and canonical representation in app stores (アプリストアにおける正当かつ正規の表現)

アプリストアには、同じ正規ソフトウェアバンドルを指す複数の有効な `storeurl` 値が存在する場合があります。たとえば、Apple App Store 内の Angry Birds アプリには、URL に国コードパラメータが含まれている場合があります：

```
<https://itunes.apple.com/fi/app/ab-classic/id343200656?mt=8> <https://itunes.apple.com/us/app/ab-classic/id343200656?mt=8> <https://itunes.apple.com/nl/app/ab-classic/id343200656?mt=8>
```

さらに、言語コード、分析追跡、およびその他のバリアントを表す複数の有効なクエリ文字列パラメータバリアントが URL 内に含まれている場合があります。

承認されたセラーの検証者は、正規のバンドル ID/ストア ID の値を見つけるためにアプリストア URL を使用するべきです（SHOULD）。承認されたセラーの検証者は、広告配信および検証のためにインデックス付けされる識別子として、以下で説明する `appstore:bundle_id` または `appstore:store_id` パラメータ内で返される正規のバンドル/ストア ID 値を使用するべきです（SHOULD）。同じアプリを識別できるストア URL のバリアントは無制限になる可能性があるため、ルックアップキーとして完全なストア URL を使用してアプリや開発者 URL のインデックスを作成しようとしないことを強く推奨します（STRONGLY RECOMMEND AGAINST）。ほとんどの実装者は、ストアのドメイン + バンドル ID またはストア ID のタプルから開発者ドメインにマップするインデックスを作成すると予想されます。例：

```
itunes.apple.com:343200656 => rovio.com
```

### Reporting (レポート)

透明性のために、承認されたセラーの検証者は、app-ads.txt ファイルを見つけるために使用されたドメインと、対応する開発者ウェブサイトを見つけるために使用されたアプリストアードメインをクライアントに報告するべきです（SHOULD）。

# Implementer notes (実装者向けノート)

サプライサイドプラットフォームは、正しい app-ads.txt ファイルに適切なエントリを追加する正しい方法を開発者に指示するヘルプセンターリソースを提供するべきです（SHOULD）。

あらゆるタイプのウェブクローラーを実装するには、時間のかかるエンジニアリング投資が必要になる場合があります。承認されたセラーの検証者は、関連するアプリストアリストおよび/または app-ads.txt ファイルデータを事前に集約する Software-as-a-Service ソリューションへのサブスクリプションを検討し、自社構築と購入のトレードオフを評価できます。多くの参加者はすでに、app-ads.txt 検証での使用に適した開発者 URL メタデータを現在公開しているアプリ分析データソース/API を購読していると予想されます。これらのサービスには、実装手法を評価し、表面化させている開発者 URL がこの仕様で説明されている標準化された HTML `<meta>` タグにある URL と一致することを顧客に自己証明することを推奨します（ENCOURAGE）。

アプリにリストされている開発者のウェブサイトは頻繁に変更されるべきではないため、クローラーが変更を特定しようとしてアプリストアを頻繁にクロールする必要があるとは予想されません。アプリの app-ads.txt ファイルをホストしているドメインを変更する開発者 URL の変更はすべて、ストアリストの更新と古い app-ads.txt ファイルの削除の間に十分な遅延を許容するべきです（SHOULD）。

非カバレッジのリスク（ファイルが削除された場合）や利用できないインベントリ（エントリが残りのファイルから削除された場合）を回避するために、廃止された app-ads.txt ファイルを長期間（可能であれば 30 日間推奨）そのままにしておくことを検討してください。

# Limitations and constraints (制限と制約)

app-ads.txt および ads.txt 標準は、承認されていないプラットフォームクライアントがサプライサイドプラットフォームやアドエクスチェンジを不適切に使用して、販売許可のない広告インベントリを提供することを防ぐのに役立ちます。これらのツールは、悪質な広告プラットフォームが、アドエクスチェンジでインプレッションを提供する前にパブリッシャー ID を変更することで、未承認のパブリッシャー ID を承認済みのものとして偽ることを阻止することはできません。参加者はこの制限を認識しておく必要があります。開発者は、信頼できるプラットフォームとパブリッシャー ID のみを app-ads.txt ファイルに導入するべきです（SHOULD）。バイヤーは、承認されたインベントリであっても、無効なトラフィックについてスクリーニングおよび監視する必要があることを認識しておく必要があります。

個々のアプリ間で承認されたセラーを分割したいアプリ開発者は、別々の開発者ドメイン/サブドメインを使用しなければなりません（MUST）。なぜなら、標準には、リンクされたドメイン上の個​​々の app-ads.txt ファイル内で、個々のセラーがアプリのサブセットに対してのみ承認されていることを示す規定がないためです。私たちは一般的に、app-ads.txt を使用してきめ細かい制御を行おうとしないことをお勧めします。

# Appendix A: Developer URL canonicalization test cases (付録 A: 開発者 URL 正規化のテストケース)

これらの入力例と期待される出力は、望ましい開発者 URL から正規化されたドメインへの変換を示しています。

### Test handling of a typical .com domain (.com ドメインの典型的な処理のテスト)

`https://www.example.com/test` -> `example.com`

`https://m.example.com/test` -> `example.com`

`https://example.com/test` -> `example.com`

`https://subdomain.example.com/test` -> `subdomain.example.com`

`https://another.subdomain.example.com/test` -> `subdomain.example.com`

`https://subdomain.www.example.com/test` -> `example.com`

### Test handing of two-level public suffix (2 レベルパブリックサフィックスの処理のテスト)

`https://www.example.co.uk/test` -> `example.co.uk`

`https://m.example.co.uk/test` -> `example.co.uk`

`https://example.co.uk/test` -> `example.co.uk`

`https://subdomain.example.co.uk/test` -> `subdomain.example.co.uk`

`https://another.subdomain.example.co.uk/test` -> `subdomain.example.co.uk`

`https://subdomain.www.example.co.uk/test` -> `example.co.uk`

### Test handling of a newer country public suffix registerable namespace (新しい国別パブリックサフィックス登録可能名前空間の処理のテスト)

`https://www.example.uk/test` -> `example.uk`

`https://m.example.uk/test` -> `example.uk`

`https://example.uk/test` -> `example.uk`

`https://subdomain.example.uk/test` -> `subdomain.example.uk`

`https://another.subdomain.example.uk/test` -> `subdomain.example.uk`

`https://subdomain.www.example.uk/test` -> `example.uk`

# Appendix B: Developer URL to app-ads.txt file URL test cases (付録 B: 開発者 URL から app-ads.txt ファイル URL への変換テストケース)

これらの入力例と期待される出力は、開発者 URL から app-ads.txt パスへの適切な変換を示しています。

### Test baseline developer URL (ベースライン開発者 URL のテスト)

このテストは、サブドメインのないベースライン URL の正規化を示しています。

* Developer URL (開発者 URL): https://example.com/test
* Verifier will crawl (検証者のクロール先): https://example.com/app-ads.txt

### Test developer URL with ignored [www.](http://www/) subdomain (無視される www. サブドメインを含む開発者 URL のテスト)

このテストは、一般的な「www」サブドメインの正規化を示しています。

* Developer URL (開発者 URL): https://www.example.com/test
* Verifier will crawl (検証者のクロール先): https://example.com/app-ads.txt
* Confirm that crawler DOES NOT crawl (クローラーがクロールしないことを確認): https://www.example.com/app-ads.txt

### Test “m.” developer URL with ignored m. subdomain (無視される m. サブドメインを含む「m.」開発者 URL のテスト)

このテストは、一般的な「m」サブドメインの正規化を示しています。

* Developer URL (開発者 URL): https://m.example.com/test
* Verifier will crawl (検証者のクロール先): https://example.com/app-ads.txt
* Confirm that crawler DOES NOT crawl (クローラーがクロールしないことを確認): https://m.example.com/app-ads.txt

### Test developer URL with subdomain (サブドメインを含む開発者 URL のテスト)

このテストは、app-ads.txt ファイルを見つけるためにサブドメインがどのように使用されるかを示しています。

* Developer URL (開発者 URL): https://subdomain.example.com/test
* Verifier will first crawl (検証者の最初のクロール先): https://subdomain.example.com/app-ads.txt
* If no file found, verifier will then crawl (ファイルが見つからない場合の検証者の次のクロール先): https://example.com/app-ads.txt

### Test developer URL with multiple subdomains (複数のサブドメインを含む開発者 URL のテスト)

このテストは、app-ads.txt ファイルを見つけるために最初のサブドメインのみがどのように使用されるかを示しています。

* Developer URL (開発者 URL): https://another.subdomain.example.com/test
* Verifier will first crawl (検証者の最初のクロール先): https://subdomain.example.com/app-ads.txt
* If no file found, verifier will then crawl (ファイルが見つからない場合の検証者の次のクロール先): https://example.com/app-ads.txt

### Test developer URL with subdomain on a multipart public suffix (マルチパートパブリックサフィックス上のサブドメインを含む開発者 URL のテスト)

このテストは、マルチパートパブリックサフィックスを持つ URL の app-ads.txt ファイルを見つけるために、最初のサブドメインのみがどのように使用されるかを示しています。

* Developer URL (開発者 URL): https://another.subdomain.example.co.uk/test
* Verifier will first crawl (検証者の最初のクロール先): https://subdomain.example.co.uk/app-ads.txt
* If no file found, verifier will then crawl (ファイルが見つからない場合の検証者の次のクロール先): https://example.co.uk/app-ads.txt