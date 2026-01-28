---
title: "Sellers.json"
sidebarTitle: "sellers.json"
description: "Sellers.json 仕様 - バイヤーがデジタル広告の販売における直接のセラーまたは仲介者を発見できるようにする仕様"
---

Sellers.json

July 2019

# Abstract（概要）

オープンなデジタル広告エコシステムにおいて偽造インベントリから利益を得る能力を排除するための広範な取り組みの一環として、Sellers.json は、バイヤーがデジタル広告の販売において直接のセラーまたは仲介者であるエンティティが誰であるかを発見できるようにするメカニズムを提供します。

# About IAB Tech Lab（IAB Tech Lab について）

IAB Technology Laboratory は、グローバルな業界技術標準とソリューションを作成し、企業の導入を支援する非営利の研究開発コンソーシアムです。Tech Lab の目標は、デジタル広告およびマーケティングのサプライチェーンに関連する摩擦を減らしながら、業界の安全な成長に貢献することです。

IAB Tech Lab は、技術標準の開発を主導し、IAB 標準の迅速かつ費用対効果の高い実装を支援するコードライブラリを作成・維持し、企業が自社の技術ソリューションと IAB 標準との互換性を評価するためのテストプラットフォームを確立しています。IAB 標準は 18 年間にわたり、デジタル広告サプライチェーンにおける相互運用性と収益性の高い成長の基盤となってきました。IAB Technology Lab の詳細については、[https://iabtechlab.com](https://iabtechlab.com/) をご覧ください。

### License

Sellers.json by OpenRTB Working Group is licensed under a [Creative Commons Attribution 3.0](http://creativecommons.org/licenses/by/3.0/) [License](http://creativecommons.org/licenses/by/3.0/). To view a copy of this license, visi[t](http://creativecommons.org/licenses/by/3.0/) [creativecommons.org/licenses/by/3.0/](http://creativecommons.org/licenses/by/3.0/) or write to Creative Commons, 171 Second Street, Suite 300, San Francisco, CA 94105, USA.

![CC by 3.0](https://i.creativecommons.org/l/by/3.0/88x31.png)

### Disclaimer

THE STANDARDS, THE SPECIFICATIONS, THE MEASUREMENT GUIDELINES, AND ANY OTHER MATERIALS OR SERVICES PROVIDED TO OR USED BY YOU HEREUNDER (THE “PRODUCTS AND SERVICES”) ARE PROVIDED “AS IS” AND “AS AVAILABLE,” AND IAB TECHNOLOGY LABORATORY, INC. (“TECH LAB”) MAKES NO WARRANTY WITH RESPECT TO THE SAME AND HEREBY DISCLAIMS ANY AND ALL EXPRESS, IMPLIED, OR STATUTORY WARRANTIES, INCLUDING, WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AVAILABILITY, ERROR-FREE OR UNINTERRUPTED OPERATION, AND ANY WARRANTIES ARISING

FROM A COURSE OF DEALING, COURSE OF PERFORMANCE, OR USAGE OF TRADE. TO THE EXTENT THAT TECH LAB MAY NOT AS A MATTER OF APPLICABLE LAW DISCLAIM ANY IMPLIED WARRANTY, THE SCOPE AND DURATION OF SUCH WARRANTY WILL BE THE MINIMUM PERMITTED UNDER SUCH LAW. THE PRODUCTS AND SERVICES DO NOT CONSTITUTE BUSINESS OR LEGAL ADVICE. TECH LAB DOES NOT WARRANT THAT THE PRODUCTS AND SERVICES PROVIDED TO OR USED BY YOU HEREUNDER SHALL CAUSE YOU AND/OR YOUR PRODUCTS OR SERVICES TO BE IN COMPLIANCE WITH ANY APPLICABLE LAWS, REGULATIONS, OR SELF-REGULATORY FRAMEWORKS,

AND YOU ARE SOLELY RESPONSIBLE FOR COMPLIANCE WITH THE SAME, INCLUDING, BUT NOT LIMITED TO, DATA PROTECTION LAWS, SUCH AS THE PERSONAL INFORMATION PROTECTION AND ELECTRONIC DOCUMENTS ACT (CANADA), THE DATA PROTECTION DIRECTIVE (EU), THE E-PRIVACY DIRECTIVE (EU), THE GENERAL DATA PROTECTION REGULATION (EU), AND THE E-PRIVACY REGULATION (EU) AS AND WHEN THEY BECOME EFFECTIVE.

# Introduction（はじめに）

ads.txt は、パブリッシャーのコンテンツ配信者やアプリパブリッシャーが、ビッドリクエストを介して特定のインプレッションセット（パブリッシャーの広告インベントリ）を販売する権限を誰が持っているかを定義できるようにする上で、非常に成功しています。ただし、ads.txt は、広告プラットフォーム（パブリッシャーの SSP - サプライサイドプラットフォーム）内のパブリッシャーアカウント ID の身元を明らかにしようとはしません。

公開されアクセス可能な sellers.json ファイルにより、ビッドリクエストの最終セラーの身元を発見できるようになります（それらが ads.txt で承認されていると仮定して）。また、[SupplyChain](https://iabtechlab.com/sellers-json) オブジェクト内のすべてのノード（ビッドリクエストに参加したエンティティ）の身元を発見することも可能になります。現在、`Publisher.name` および `Publisher.domain` 属性を介して最終セラーを特定することは可能ですが、実際には、これらのプロパティはさまざまな販売システムによって一貫性なく入力されています。

Sellers.json は、この情報をすべてのビッドリクエストとともに提供するのではなく、「オフライン」で検索してキャッシュできるようにすることで、ビッドリクエストオブジェクトのサイズを小さくすることができます。Sellers.json はまた、ビッドリクエストの販売に参加したすべての仲介者の識別も可能にします。

# Audience（対象読者）

広告システムは、プログラマティック広告のセラーであれバイヤーであれ、取引のすべての当事者が十分に理解されている透明な市場から恩恵を受けます。このドキュメントは、セラーがプログラマティックインベントリの下流のセラーとバイヤーの両方に提供する情報を定義する役割を果たします。

# Change Log（変更履歴）

| **Version** | **Date** | **Changes** |
| --- | --- | --- |
| 1.0 | July 2019 | 初版 |

# SPECIFICATION（仕様）

このドキュメントは、広告システムが自らが代表するセラーとシステム内のそれらのセラーの識別子を公表するためのメカニズムを規定します。また、広告システムとその顧客が利用する命令をエンコードするためのフォーマットについても説明します。

## ACCESS METHOD（アクセス方法）

広告システムは、sellers.json ファイルをルートドメインおよび必要に応じてサブドメインに掲載するべきです。このドキュメントの目的において、「ルートドメイン」は「パブリックサフィックス」プラス名前に含まれる 1 つの文字列として定義されます。クローラーは、ルートドメインを導出するためにパブリックサフィックスリスト [16] を組み込むべきです。

宣言は、命令が適用されるウェブサイトから HTTP および/または HTTPS 経由で、サーバーホスト上の標準的な相対パス `“/sellers.json”` でアクセスできなければならず（MUST）、HTTP リクエストヘッダーには `“Content-Type: application/json”` が含まれている必要があります。さらに、`"Content-Type: application/json; charset=utf-8"` を使用して、UTF8 サポートを明示的に示すこともできます。

また、sellers.json ファイルをクロールする場合は、HTTP 経由の HTTPS 接続が推奨されます。いずれの場合も、同じ URL に対して HTTPS 接​​続と HTTP 接続の両方でデータを利用できる場合は、HTTPS からのデータが優先されるべきです。

便宜上、このリソースを「`“/sellers.json”` ファイル」と呼びます。「ファイル」という言葉を使用していますが、リソースがファイルシステム由来である必要はありません。

サーバーレスポンスが Success（HTTP 2xx ステータスコード）を示す場合、広告システムはコンテンツを読み取り、解析し、宣言を利用しなければなりません。

サーバーレスポンスが HTTP/HTTPS リダイレクト（301、302、307 ステータスコード）を示す場合、広告システムはリダイレクトに従い、リダイレクトが上記で定義された名前のパブリックサフィックスプラス 1 文字列として定義される元のルートドメインの範囲内にある場合に限り、そのデータをリダイレクト元の正当な情報として利用するべきです。各リダイレクト場所が元のルートドメイン内に留まる限り、複数のリダイレクトは有効です。たとえば、同じルートドメイン内での HTTP から HTTPS へのリダイレクトは有効です。

サードパーティの Web サーバーへの 1 ホップの権限委任を容易にするために、元のルートドメイン外の宛先への単一の HTTP リダイレクトのみが許可されます。サードパーティの場所がリダイレクトを返す場合、広告システムはレスポンスをエラーとして扱うべきです。将来のバージョンでは、サードパーティの Web サーバーへの他の権限委任に対処する可能性がありますが、現時点では、サードパーティの Web サーバーへのリダイレクトおよびその他のリダイレクトはエラーとして解釈され、無視されるべきです。

サーバーレスポンスがリソースが存在しないこと（HTTP ステータスコード 404）を示している場合、またはその他の HTTP エラーの場合は、最後に正常に取得されたデータセットが利用されるべきです。

## FILE FORMAT（ファイル形式）

ファイル内のすべてのデータは、JSON（JavaScript Object Notation）を使用してシリアル化されます。親 JSON オブジェクトとすべての子オブジェクトが sellers.json ファイルに書き込まれます。

## EXPIRATION（有効期限）

`“/sellers.json”` を利用するシステムは、ファイルをキャッシュするべきですが、そうする場合は、そのコンテンツを使用する前にキャッシュされたコピーが新しいことを定期的に確認しなければなりません。

標準的な HTTP キャッシュ制御メカニズムは、オリジンサーバーとロボットの両方が `“/sellers.json”` ファイルのキャッシュに影響を与えるために使用できます。具体的には、コンシューマーとレプリケーターは、オリジンサーバーによって設定された HTTP Expires ヘッダーに注意するべきです。

Cache-Control ディレクティブが存在しない場合、利用システムはデフォルトで有効期限を 7 日間とするべきです。

## Implementation（実装）

ads.txt ファイルに記載されているすべての広告システム、および SupplyChain オブジェクトノードから参照されているすべての広告システムは、以下の場所で Sellers.json ファイルを公開するべきです。

http://{advertising_system_domain}/sellers.json

## Object specifications（オブジェクト仕様）

### Object: Parent

Parent オブジェクトは、Sellers.json ファイルのトップレベルオブジェクトです。これは、sellers.json ファイル内のすべてのプロパティのコンテナです。

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| sellers | object array; required | 広告システムによって表されるすべての Seller オブジェクトのリスト。すべてのセラーは、機密（confidential）であっても含めなければなりません。 |
| identifiers | object array; optional | この広告システムに関連付けられた Identifier オブジェクトの配列。例としては、TAG-ID、Dun & Bradstreet ビジネス識別子、または利用する広告システムが必要とする可能性のある任意のカスタム識別子などがあります。 |
| contact_email | string; optional | このファイルに関する質問や問い合わせのために広告システムに連絡するための電子メールアドレス。 |
| contact_address | string; optional | 広告システムの会社の住所。 |
| version | string; required | この仕様のバージョン。現在、唯一の有効な値は 1.0 です。 |
| ext | object; optional | このオブジェクトへの広告システム固有の拡張のためのプレースホルダー。 |

### Sellers.json object: Identifier

識別子は任意の名前/値のペアであり、ビジネス識別子、認証識別子、または利用システムがセラーとより適切に相互運用するために必要なその他の識別子などの共通値を伝達するために使用されます。

標準識別子は、以下の[識別子名（Identifier Names）](#identifier-names)セクションにリストされています。

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| name | string; required | 識別子の説明 |
| value | string; required | 識別子の値 |

### Sellers.json object: Seller

`seller_id` に代わって販売されるインベントリの支払いを受ける販売法的エンティティの識別。

`seller_id` が複数のエンティティを表すことは無効です。すべての `seller_id` は、その `seller_id` で取引されたインベントリに対して支払いを受ける単一のエンティティにのみマップされなければなりません。販売エンティティが広告システム内に複数の `seller_id` を持つことは有効です。

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| seller_id | string; required | これは、ads.txt ファイルおよび SupplyChain.nodes 配列の `sid` プロパティに表示されるのと同じ ID です。ほとんどの場合、OpenRTB リクエストの `Publisher.Id` プロパティにも表示されます。 |
| is_confidential | integer; optional, default 0 | セラーの身元が機密であるかどうかを示します。0 = 機密ではない、1 = 機密である。 |
| seller_type | string; required | アカウントのタイプの列挙（`PUBLISHER`、`INTERMEDIARY`、または `BOTH`）。`"PUBLISHER"` の値は、このアカウントを通じて販売されるインベントリが、指定されたエンティティが所有するサイト、アプリ、またはその他のメディア上にあり、広告システムがそれらに直接支払いを行うことを示します。`"INTERMEDIARY"` の値は、このアカウントを通じて販売されるインベントリが、指定されたエンティティによって所有されていないか、広告システムが直接支払いを行わないことを示します。`"BOTH"` は、両方のタイプのインベントリがこのセラーによって取引されることを示します。このフィールドは、データを解釈する際に大文字と小文字を区別しないものとして扱われるべきであることに注意してください。 |
| is_passthrough | integer; optional, default 0 | パススルーセラーは、上流のサプライヤーからインベントリのコンシューマーへのインベントリの仲介者です。上流のサプライヤーとコンシューマーは、上流のサプライヤーがコンシューマーのプラットフォーム内でアカウントを管理できるように、相互にビジネス関係を確立していなければなりません。**値 1** は以下を示します。 * このセラーには、下流/利用側の広告システムとのアカウント制御関係があります。 * このセラーが SupplyChain の最後のリンクである場合、購買システムは、セラーのインベントリを取引するために、このセラーとのアカウント制御関係を確立している必要があります。 * これが SupplyChain の最後のリンクではない場合、このセラーは、アカウント制御関係を持つ 2 つのエンティティの間に存在するべきです。 **値 0** は以下を示します。 * 下流/利用側の広告システムには、このセラーとのアカウント制御関係がありません。 |
| name | string; required when is_confidential=0 | 指定された `seller_id` で取引されるインベントリの支払いを受ける会社（法的エンティティ）の名前。`is_confidential` が 1 に設定されている場合にのみ省略可能です。 |
| domain | string; required if seller has a web presence and is_confidential=0 | 指定された `seller_id` で取引されるインベントリの支払いを受ける会社（法的エンティティ）のビジネスドメイン名。`seller_type` プロパティが `INTERMEDIARY` または `BOTH` に設定されている場合、これはセラーの sellers.json ファイルのルートドメイン名であるべきです。`is_confidential` が 1 に設定されている場合、またはセラーが Web プレゼンスを持っていない場合は省略可能です。 |
| comment | string; optional | このインベントリに関する役立つ説明。複数のセラー ID を持つセラーが、このセラー ID が何を表しているかを説明するのに役立ちます。 |
| ext | object; optional | このオブジェクトへの広告システム固有の拡張のためのプレースホルダー。 |

sellers.json および SupplyChain のドメインには、OpenRTB の Site オブジェクトの `domain` や ads.txt に使用されるドメイン定義と同様に、完全な URL ではなく**ルートドメイン**のみが入力されることに注意してください。このドキュメントの目的において、「ルートドメイン」は「パブリックサフィックス」プラス名前に含まれる 1 つの文字列として定義されます。実装者は、ルートドメインを導出するためにパブリックサフィックスリスト [16] を組み込むべきです。

## Enumerated List Specification（列挙リスト仕様）

### Identifier Names

以下のリストは、識別子リストで使用されるべき標準識別子を定義しています。

| **Name** | **Description** |
| --- | --- |
| TAG-ID | Trustworthy Accountability Group ID |
| DUNS | Dun & Bradstreet DUNS Number |

# Sample File Contents（サンプルファイル内容）

```json
{
  "contact_email": "adops@advertisingsystem.com",
  "contact_address": "Advertising System Inc., 101 Main Street, New York, NY 10101",
  "version": "1.0",
  "identifiers": [
    {
      "name": "TAG-ID",
      "value": "28cb65e5bbc0bd5f"
    }
  ],
  "sellers": [
    {
      "seller_id": "1942009976",
      "name": "Publisher1",
      "domain": "publisher1.com",
      "seller_type": "PUBLISHER"
    },
    {
      "seller_id": "1397382429",
      "name": "Exchange1",
      "domain": "exchange1.com",
      "seller_type": "INTERMEDIARY"
    },
    {
      "seller_id": "20000000",
      "name": "Seller And Intermediary, Inc",
      "domain": "sellerandintermediary.com",
      "seller_type": "PUBLISHER",
      "comment": "NorthAmerica O&O inventory"
    },
    {
      "seller_id": "20000001",
      "name": "Seller And Intermediary, Inc",
      "domain": "sellerandintermediary.com",
      "seller_type": "PUBLISHER",
      "comment": "APAC O&O inventory"
    },
    {
      "seller_id": "20000002",
      "name": "Seller And Intermediary, Inc",
      "domain": "sellerandintermediary.com",
      "seller_type": "INTERMEDIARY",
      "comment": "Non O&O inventory"
    },
    {
      "seller_id": "101010101",
      "name": "Hybrid Seller",
      "domain": "hybridseller.com",
      "seller_type": "BOTH",
      "comment": "Sells both O&O and other sellers' inventory"
    },
    {
      "seller_id": "00000001",
      "seller_type": "INTERMEDIARY",
      "is_confidential": 1
    },
    {
      "seller_id": "EB_0001",
      "name": "Passthrough Publisher",
      "domain": "passthroughpublisher.com",
      "seller_type": "PUBLISHER",
      "is_passthrough": 1,
      "comment": "direct buyer/seller of this inventory must establish an account relationship with Passthrough Publisher"
    }
  ]
}
```
