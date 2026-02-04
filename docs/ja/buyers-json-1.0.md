---
title: "buyers.json 1.0"
description: "広告在庫を購入している買い手（広告主・代理店等）の正体を公開情報として宣言し、デジタル広告の需要側サプライチェーンの透明性と不正対策を強化します。"
---
Released June 2021

フィードバックや質問は support@iabtechlab.com までメールでお送りください。このドキュメントは [https://iabtechlab.com/buyers-json-demand-chain](https://iabtechlab.com/buyers-json-demand-chain) でオンライン利用可能です。

© IAB Technology Laboratory

# このドキュメントについて

| 項目 | 内容 |
|------|------|
| 翻訳 | Advertisers and Publishers Transparency Initiative (APTI) |
| 原著者 | IAB Technology Laboratory (IAB Tech Lab) |
| 原文 | [buyers.json v1.0](https://iabtechlab.com/wp-content/uploads/2021/03/buyers-json-1-0.pdf) |
| ライセンス | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) |

※この翻訳は、IAB Tech Lab による公式なものではありません。翻訳の正確性については翻訳者が責任を負います。

# About IAB Tech Lab（IAB Tech Lab について）

IAB Technology Laboratory は、グローバルな業界技術標準とソリューションを作成し、企業の導入を支援する非営利の研究開発コンソーシアムです。Tech Lab の目標は、デジタル広告およびマーケティングのサプライチェーンに関連する摩擦を減らしながら、業界の安全な成長に貢献することです。

IAB Tech Lab は、技術標準の開発を主導し、IAB 標準の迅速かつ費用対効果の高い実装を支援するコードライブラリを作成・維持し、企業が自社の技術ソリューションと IAB 標準との互換性を評価するためのテストプラットフォームを確立しています。IAB 標準は 18 年間にわたり、デジタル広告サプライチェーンにおける相互運用性と収益性の高い成長の基盤となってきました。IAB Technology Lab の詳細については、[https://iabtechlab.com](https://iabtechlab.com/) をご覧ください。

### License

**buyers.json** by the IAB Tech Lab’s Programmatic Standards Working Group is licensed under a Creative Commons Attribution 3.0 License. To view a copy of this license, visit creativecommons.org/licenses/by/3.0/ or write to Creative Commons, 171 Second Street, Suite 300, San Francisco, CA 94105, USA.

![CC by 3.0](https://i.creativecommons.org/l/by/3.0/88x31.png)

### Disclaimer

THE STANDARDS, THE SPECIFICATIONS, THE MEASUREMENT GUIDELINES, AND ANY OTHER MATERIALS OR SERVICES PROVIDED TO OR USED BY YOU HEREUNDER (THE “PRODUCTS AND SERVICES”) ARE PROVIDED “AS IS” AND “AS AVAILABLE,” AND IAB TECHNOLOGY LABORATORY, INC. (“TECH LAB”) MAKES NO WARRANTY WITH RESPECT TO THE SAME AND HEREBY DISCLAIMS ANY AND ALL EXPRESS, IMPLIED, OR STATUTORY WARRANTIES, INCLUDING, WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AVAILABILITY, ERROR-FREE OR UNINTERRUPTED OPERATION, AND ANY WARRANTIES ARISING

FROM A COURSE OF DEALING, COURSE OF PERFORMANCE, OR USAGE OF TRADE. TO THE EXTENT THAT TECH LAB MAY NOT AS A MATTER OF APPLICABLE LAW DISCLAIM ANY IMPLIED WARRANTY, THE SCOPE AND DURATION OF SUCH WARRANTY WILL BE THE MINIMUM PERMITTED UNDER SUCH LAW. THE PRODUCTS AND SERVICES DO NOT CONSTITUTE BUSINESS OR LEGAL ADVICE. TECH LAB DOES NOT WARRANT THAT THE PRODUCTS AND SERVICES PROVIDED TO OR USED BY YOU HEREUNDER SHALL CAUSE YOU AND/OR YOUR PRODUCTS OR SERVICES TO BE IN COMPLIANCE WITH ANY APPLICABLE LAWS, REGULATIONS, OR SELF-REGULATORY FRAMEWORKS, AND YOU ARE SOLELY RESPONSIBLE FOR COMPLIANCE WITH THE SAME, INCLUDING, BUT NOT LIMITED TO, DATA PROTECTION LAWS, SUCH AS THE PERSONAL INFORMATION PROTECTION AND ELECTRONIC DOCUMENTS ACT (CANADA), THE DATA PROTECTION DIRECTIVE (EU), THE E-PRIVACY DIRECTIVE (EU), THE GENERAL DATA PROTECTION REGULATION (EU), AND THE E-PRIVACY REGULATION (EU) AS AND WHEN THEY BECOME EFFECTIVE.

**Special thanks to** John Clyman, VP Engineering, Marketplace Quality & Security, Magnite for his leadership.

### Other Significant Contributors Include:

Paul Bannister, Chief Strategy Officer, Cafe Media; Per Bjorke, Sr. Product manager, Ad Traffic Quality, Google; Eric Bozinny, Sr. Director, Marketplace Quality, Pubmatic; Julien Delhommeau, Sr. Solutions Consultant, Xandr; Emma Fenlon, Sr. Manager, Exchange Quality, Verizon Media; Rahul Gupta, VP Client Solutions, Pulsepoint; Aaron Herrmann, Product Manager, Ads Integrity, Google; Curtis Light, Staff Software Engineer, Google; John Murphy, Chief Strategy Officer, Confiant; Alexandre Nderagakura, Technical Director, IAB Europe ; Angie Pennington, Sales & Operations Strategy Lead, Verizon Media; Amit Shetty, VP Programmatic & Partnerships, IAB Tech Lab, Lindsay Superczynski-Matthies, Sr P&E Optimization Specialist, Exchange Quality, Verizon Media; Maddy Want, Director of Product, Index Exchange.

### IAB Tech Lab Lead:

Amit Shetty, VP Programmatic & Partnerships, IAB Tech Lab

# 1 Abstract（概要）

デジタル広告エコシステムからマルバタイジングやその他の広告品質の問題を排除するための広範な取り組みの一環として、buyers.json は、セラーが自社のインベントリを購入しているのが誰であるかを識別できるようにします。このシステムの主な推進要因は、セラーがあらゆるデマンドソースを通じて、あらゆる形態のバイヤーを識別する必要があることです。これは、パブリッシャーが自社のインベントリに対する支出をより適切に監視し、多くの形態のマルバタイジングを解決し、最終的にパブリッシャーとそのオーディエンスを保護するのに役立つことを目的としています。

最大の効果を得るために、buyers.json は OpenRTB DemandChain オブジェクトと併用し、インプレッションの購入に関与するバイヤーエンティティの完全なチェーンへの包括的な視点を提供するべきです。

# 2 Introduction（はじめに）

バイヤーの身元に関する透明性の欠如は、マルバタイジングを排除する上での主な障害の 1 つです。マルバタイザーは、最も脆弱な侵入口を悪用し、DSP から DSP へと頻繁に移動することで、デジタル広告エコシステムの不透明で高度に断片化された性質を利用します。ある DSP で正体が判明するとすぐに、マルバタイザーはキャンペーンをシームレスに新しい DSP に移行します。パブリッシャーや SSP は、バイヤーの身元を把握していないことが多く、そのため、すべてのアクセスポイントですでに判明している悪質なエンティティを一斉にブロックすることができません。最終的な効果は、モグラ叩きゲームに例えられ、同じエンティティが異なる DSP を介して何度も現れます。

buyers.json は、広告システムやその他の支払い者とパブリッシャーの間の仲介者が、自分たちが代表するバイヤーを公表するためのメカニズムです。この情報を武器に、パブリッシャーと SSP は、マルバタイジング攻撃の発生源をより簡単に特定し、複数のデマンドソースにまたがる問題のあるバイヤーを特定し、自社とユーザーを保護するための適切な措置を講じることができます。

buyers.json は、ads.txt、Sellers.json、SupplyChain オブジェクトなど、業界で成功しているセルサイドの透明性への取り組みによって定められた道をたどります。Sellers.json がセルサイドエンティティの身元の透明性を高めたのと同様に、buyers.json はバイサイドに対して同じことを行います。

このドキュメントでは、広告システムとその顧客が利用する命令をエンコードするためのフォーマットについて説明します。

buyers.json は、OpenRTB DemandChain オブジェクトと併用するように設計されています。これら 2 つの仕様を合わせることで、マルウェアやその他の問題のあるデマンドに対抗するために使用できる透明性が大幅に向上しますが、あらゆる潜在的な形態の悪用を解決できるわけではありません。エージェンシーの身元のなりすましを防ぐには、追加の透明性の取り組みが必要になる場合があります。検討すべき取り組みの 1 つは、信頼できない仲介者によるデマンドの操作を防ぐための暗号技術（ads.cert など）の使用ですが、そのような取り組みはこの仕様の範囲外です。

# 3 Specification（仕様）

## 3.1 Access Method（アクセス方法）

DSP およびバイヤーとコンテンツパブリッシャーの間のその他の仲介者は、buyers.json ファイルをルートドメインに掲載するべきです。このドキュメントの目的において、「ルートドメイン」は「パブリックサフィックス」プラス名前に含まれる 1 つの文字列として定義されます。クローラーは、ルートドメインを導出するためにパブリックサフィックスリストを組み込むべきです。

buyers.json ファイルを掲載する一部のエンティティは複数のドメインを持っている場合があり、そのうちの 1 つが企業ドメインで、もう 1 つが別の広告配信ドメインである可能性があります。DemandChain データを buyers.json データにリンクするには、buyers.json ファイルは、DemandChainNode オブジェクトの "asi"（Advertising System Identifier / 広告システム識別子）フィールドに存在する任意のドメインで利用可能であるべきです。これは、おそらく正規のファイルにリダイレクトすることによって実現されます。buyers.json のコンテンツは、サーバーホスト上の標準的な相対パス `“/buyers.json”` のルートドメインから HTTPS 経由でアクセス可能でなければならず、HTTP リクエストヘッダーには `“Content-Type: application/json”` が含まれている必要があります。さらに、`"Content-Type: application/json; charset=utf-8"` を使用すると、UTF8 サポートが明示的に示されます。

便宜上、このリソースを「buyers.json ファイル」と呼びます。「ファイル」という言葉を使用していますが、リソースがファイルシステム由来である必要はありません。サーバーレスポンスが Success（HTTP 2xx ステータスコード）を示す場合、広告システムはコンテンツを読み取り、解析し、意図されたとおりに宣言を使用しなければなりません。サーバーレスポンスが HTTP リダイレクト（301、302、307 ステータスコード）を示す場合、広告システムはリダイレクトに従い、パブリックサフィックスプラス 1 文字列として定義される元のルートドメインから 1 回以内のリダイレクトであれば、そのデータをリダイレクト元の正当な情報として利用するべきです。元のルートドメインから外れるリダイレクトが 1 回だけであれば、複数のリダイレクトも有効です。HTTP 4xx および 5xx レスポンスの動作は未定義であり、実装に委ねられます。

## 3.2 File Format（ファイル形式）

ファイル内のすべてのデータは、JSON（JavaScript Object Notation）を使用してシリアル化されます。親 JSON オブジェクトとすべての子オブジェクトが buyers.json ファイルに書き込まれます。

## 3.3 Expiration（有効期限）

buyers.json を利用するシステムは、ファイルをキャッシュし、そのコンテンツを使用する前にキャッシュされたコピーが新しいことを定期的に確認するべきです。

標準的な HTTP キャッシュ制御メカニズムは、オリジンサーバーとロボットの両方が `“/buyers.json”` ファイルのキャッシュに影響を与えるために使用できます。具体的には、コンシューマーとレプリケーターは、オリジンサーバーによって設定された HTTP Expires ヘッダーに注意するべきです。最大有効期限は 7 日間が推奨されます。Cache-Control ディレクティブが存在しない場合、利用システムはデフォルトで有効期限を 7 日間とするべきです。

## 3.4 Implementation（実装）

バイヤーとパブリッシャーの間のすべての仲介者は、次の場所で buyers.json ファイルを公開するべきです。

```
https://{root_domain}/buyers.json
```

## 3.5 Object Specifications（オブジェクト仕様）

### Object: Parent

Parent オブジェクトは、buyers.json ファイルのトップレベルオブジェクトです。これは、buyers.json ファイル内のすべてのプロパティのコンテナです。

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| Buyers | object array; required | 広告システムによって表されるすべての Buyers オブジェクトのリスト。すべてのバイヤーは、機密（confidential）であっても含めなければなりません。 |
| Identifiers | object array; optional | この広告システムに関連付けられた Identifier オブジェクトの配列。例としては、TAG-ID、Dun & Bradstreet ビジネス識別子、または利用する広告システムが必要とする可能性のある任意のカスタム識別子などがあります。注: TAG には、buyers.json および DemandChain オブジェクトの使用に関する要件を Certified Against Malware プログラムに含める計画があり、これによりバイサイドの透明性イニシアチブの全体的な目標が支援されるため、IAB Tech Lab は TAG-ID の使用を推奨します。 |
| Name | string; optional | この広告システムが他の広告システムで識別されることを望む名前。 |
| contact_email | string; optional | このファイルに関する質問や問い合わせのために広告システムに連絡するための電子メールアドレス。 |
| contact_address | string; optional | 広告システムの会社の住所。 |
| version | string; required | この仕様のバージョン。現在、唯一の有効な値は文字列 "1.0" です（数値は無効）。 |
| last_updated | string; recommended | このファイルが最後に変更された日時。ISO 8601 形式の UTC（Zulu）時間。例: "2020-12-01T00:01:02Z"。取得システムでの不要な重複を防ぐために、実際のファイルコンテンツが変更されていない場合は、このタイムスタンプを更新しないべきです。 |
| ext | object; optional | このオブジェクトへの広告システム固有の拡張のためのプレースホルダー。 |

### Object: Buyers

このオブジェクトは、`buyer_id` に代わってインベントリの支払いを行う法的エンティティを識別します。ほとんどの場合、`buyer_id` は単一の法的エンティティのみを表すべきです。エンティティがマネージドサービスデスクまたはさまざまなバイヤーにサービスを提供する同様の業務である場合、そのエンティティは独自の buyers.json ファイルを掲載し、独自の DemandChain ノードによって表されなければなりません。つまり、複数の法的エンティティからのデマンドを集約する個々の `buyer_id` は、それ自体を仲介者と見なし、これらの透明性の取り組みにも参加するべきです。より詳細な例については、実装ガイドの「マネージドサービスデスクを持つ DSP（DSP with Managed Service Desk）」のセクションを参照してください。

購入エンティティは、広告システム内に複数の `buyer_id` を持つ場合があります。

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| buyer_id | String; required | バイヤーエンティティの一意の識別子。これは、OpenRTB レスポンスに `bidresponse.seatbid[].seat` プロパティが存在する場合、そのプロパティに含まれる ID と同じであるべきです。これは、DemandChain オブジェクト内の `DemandChainNode.bsid` に含まれる値ともなるべきです。 |
| is_confidential | Integer; optional, default: 0 | バイヤーの身元が機密であるかどうかを示します。0 = 機密ではない、1 = 機密である。 |
| buyer_type | string; required | アカウントのタイプの説明。`ADVERTISER`、`INTERMEDIARY`、または `BOTH` のいずれか。`"ADVERTISER"` の値は、このアカウントがインベントリを購入した広告主によって管理されていることを示します。`"INTERMEDIARY"` の値は、広告主に代わって作業するエンティティ（エージェンシーやリセラーなど）によってこのアカウントが管理されていることを示します。`"BOTH"` の値は、ビジネスのコンテキストに応じて広告主または仲介者のいずれかとして機能するエンティティによってこのアカウントが管理されていることを示します。このフィールドは、データを解釈する際に大文字と小文字を区別しないものとして扱われるべきです。 |
| name | string; required when is_confidential=0 | 指定された `buyer_id` で取引されるインベントリの支払いを行う会社（法的エンティティ）の名前。`is_confidential` が 1 に設定されている場合にのみ省略可能です。 |
| domain | string; required if buyer has a web presence and is_confidential=0 | 指定された `buyer_id` で取引されるインベントリの支払いを行う会社（法的エンティティ）のビジネスドメイン名。これはルートドメインのみでなければなりません。URL としてフォーマットしないでください。正: *example.com.* 誤: [*https://example.com/.*](https://example.com/) |
| comment | string; optional | このシートに関する役立つ説明。単一のプラットフォーム上に複数のバイヤー ID を持つバイヤーは、`comment` フィールドを使用して、この特定の `buyer_id` が何を表しているかを説明できます。 |
| created_on | string; recommended | バイヤーのシートの作成日。バイヤーがどれくらいの期間アクティブであるかを推定するのに役立ちます（マルバタイジングバイヤーは寿命が短い傾向があります）。日付の値は、ISO 8601 標準形式で表されるべきです。例: 2020-10-06。 |
| ext | object; optional | このオブジェクトへの広告システム固有の拡張のためのプレースホルダー。 |

## 3.6 Enumerated List Specification（列挙リスト仕様）

Identifier Names

以下のリストは、識別子リストで使用されるべき標準識別子を定義しています。

| **Name** | **Description** |
| --- | --- |
| TAG-ID | Trustworthy Accountability Group ID |
| DUNS | Dun & Bradstreet DUNS Number |

# 4 Sample File Contents（サンプルファイル内容）

```json
{
  "contact_email": "adquality@advertisingsystem.example",
  "contact_address": "Advertising System Inc., 101 Main Street, New York, NY 10101",
  "version": "1.0",
  "identifiers": [
    {
      "name": "TAG-ID",
      "value": "29da45e9wbh0bd5g"
    }
  ],
  "buyers": [
    {
      "buyer_id": "1234",
      "name": "Advertiser, Inc",
      "domain": "advertisingdomain.example",
      "buyer_type": "ADVERTISER",
      "created_on": "2020-10-01"
    },
    {
      "buyer_id": "5678",
      "name": "Intermediate Enterprises",
      "domain": "platformdomain.example",
      "buyer_type": "INTERMEDIARY",
      "created_on": "2020-09-21"
    },
    {
      "buyer_id": "1000023",
      "name": "Agency Group",
      "domain": "agencydomain.example",
      "buyer_type": "INTERMEDIARY",
      "comment": "Main seat for Agency Group",
      "created_on": "2020-09-01"
    },
    {
      "buyer_id": "212402",
      "is_confidential": 1,
      "buyer_type": "INTERMEDIARY",
      "created_on": "2020-10-01"
    }
  ]
}
```
