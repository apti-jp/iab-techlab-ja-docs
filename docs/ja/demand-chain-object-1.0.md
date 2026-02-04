---
title: "demand chain object 1.0"
description: "広告クリエイティブの購入に関与するすべての買い手側事業者を可視化し、買い手サイドの透明性を高めます。"
---
Released March 2021

フィードバックや質問は openMedia@iabtechlab.com または support@iabtechlab.com までメールでお送りください。このドキュメントは [https://iabtechlab.com/buyers-json-demand-chain](https://iabtechlab.com/buyers-json-demand-chain) でオンライン利用可能です。

© IAB Technology Laboratory

# このドキュメントについて

| 項目 | 内容 |
|------|------|
| 翻訳 | Advertisers and Publishers Transparency Initiative (APTI) |
| 原著者 | IAB Technology Laboratory (IAB Tech Lab) |
| 原文 | [DemandChain Object v1.0](https://iabtechlab.com/wp-content/uploads/2021/06/DemandChainObject-1.0-June2021.pdf) |
| ライセンス | [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/) |

※この翻訳は、IAB Tech Lab による公式なものではありません。翻訳の正確性については翻訳者が責任を負います。

# About IAB Tech Lab（IAB Tech Lab について）

IAB Technology Laboratory は、グローバルな業界技術標準とソリューションを作成し、企業の導入を支援する非営利の研究開発コンソーシアムです。Tech Lab の目標は、デジタル広告およびマーケティングのサプライチェーンに関連する摩擦を減らしながら、業界の安全な成長に貢献することです。

IAB Tech Lab は、技術標準の開発を主導し、IAB 標準の迅速かつ費用対効果の高い実装を支援するコードライブラリを作成・維持し、企業が自社の技術ソリューションと IAB 標準との互換性を評価するためのテストプラットフォームを確立しています。IAB 標準は 18 年間にわたり、デジタル広告サプライチェーンにおける相互運用性と収益性の高い成長の基盤となってきました。IAB Technology Lab の詳細については、[https://iabtechlab.com](https://iabtechlab.com/) をご覧ください。

### License

Buyers.json by the IAB Tech Lab’s Programmatic Standards Working Group is licensed under a Creative Commons Attribution 3.0 License. To view a copy of this license, visit creativecommons.org/licenses/by/3.0/ or write to Creative Commons, 171 Second Street, Suite 300, San Francisco, CA 94105, USA.

![CC by 3.0](https://i.creativecommons.org/l/by/3.0/88x31.png)

### Disclaimer

THE STANDARDS, THE SPECIFICATIONS, THE MEASUREMENT GUIDELINES, AND ANY OTHER MATERIALS OR SERVICES PROVIDED TO OR USED BY YOU HEREUNDER (THE “PRODUCTS AND SERVICES”) ARE PROVIDED “AS IS” AND “AS AVAILABLE,” AND IAB TECHNOLOGY LABORATORY, INC. (“TECH LAB”) MAKES NO WARRANTY WITH RESPECT TO THE SAME AND HEREBY DISCLAIMS ANY AND ALL EXPRESS, IMPLIED, OR STATUTORY WARRANTIES, INCLUDING, WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AVAILABILITY, ERROR-FREE OR UNINTERRUPTED OPERATION, AND ANY WARRANTIES ARISING FROM A COURSE OF DEALING, COURSE OF PERFORMANCE, OR USAGE OF TRADE. TO THE EXTENT THAT TECH LAB MAY NOT AS A MATTER OF APPLICABLE LAW DISCLAIM ANY IMPLIED WARRANTY, THE SCOPE AND DURATION OF SUCH WARRANTY WILL BE THE MINIMUM PERMITTED UNDER SUCH LAW. THE PRODUCTS AND SERVICES DO NOT CONSTITUTE BUSINESS OR LEGAL ADVICE. TECH LAB DOES NOT WARRANT THAT THE PRODUCTS AND SERVICES PROVIDED TO OR USED BY YOU HEREUNDER SHALL CAUSE YOU AND/OR YOUR PRODUCTS OR SERVICES TO BE IN COMPLIANCE WITH ANY APPLICABLE LAWS, REGULATIONS, OR SELF-REGULATORY FRAMEWORKS, AND YOU ARE SOLELY RESPONSIBLE FOR COMPLIANCE WITH THE SAME, INCLUDING, BUT NOT LIMITED TO, DATA PROTECTION LAWS, SUCH AS THE PERSONAL INFORMATION PROTECTION AND ELECTRONIC DOCUMENTS ACT (CANADA), THE DATA PROTECTION DIRECTIVE (EU), THE E-PRIVACY DIRECTIVE (EU), THE GENERAL DATA PROTECTION REGULATION (EU), AND THE E-PRIVACY REGULATION (EU) AS AND WHEN THEY BECOME EFFECTIVE.

**Special thanks to** John Clyman, VP Engineering, Magnite for his leadership

### Other Significant Contributors Include:

Paul Bannister, Chief Strategy Officer, Cafe Media; Per Bjorke, Sr. Product manager, Ad Traffic Quality, Google; Eric Bozinny, Sr. Director, Marketplace Quality, Pubmatic; Julien Delhommeau, Sr. Solutions Consultant, Xandr; Emma Fenlon, Sr. Manager, Exchange Quality, Verizon Media; Rahul Gupta, VP Client Solutions, Pulsepoint; Aaron Herman, Product Manager, Ads Integrity, Google; Curtis Light, Staff Software Engineer, Google; John Murphy, Chief Strategy Officer, Confiant; Alexandre Nderagakura, Product Specialist - Programmatic, Smart ad server; Angie Pennington, Sales & Operations Strategy Lead, Verizon Media; Amit Shetty, VP Programmatic & Partnerships, IAB Tech Lab, Lindsay Superczynski-Matthies, Sr P&E Optimization Specialist, Exchange Quality, Verizon Media; Maddy Want, Director of Product, Index Exchange.

### IAB Tech Lab Lead:

Amit Shetty, VP Programmatic & Partnerships, IAB Tech Lab

# 1 Abstract（概要）

アドテクにおける透明性を促進し、特にパブリッシャーとエンドユーザーをマルバタイジングやその他の好ましくない広告から保護するための包括的な取り組みの一環として、DemandChain オブジェクトは、特定のビッドレスポンスに埋め込まれたクリエイティブの購入に関与するすべての当事者をセラーが確認できるようにします。この拡張オブジェクトは、OpenRTB 2.x または OpenRTB 3.0 で使用できます。

DemandChain は、buyers.json と連携して、セルサイドの透明性を高める SupplyChain および Sellers.json の仕様を補完するバイサイドの機能を提供します。

# 2 Introduction（はじめに）

ads.txt、そしてその後の SupplyChain と Sellers.json は、DSP やその他のバイヤーが、ビッドリクエストで提供されるインベントリを供給しているエンティティの完全なチェーンを特定できるようにする上で非常に成功しています。同様の透明性は、セルサイドがバイヤーを可視化するためにも不可欠です。これにより、悪意のあるアクターを特定してブロックし、クリエイティブの出所について情報に基づいた判断を下し、再販や同様の行為に対する制限を強制することができます。この実装は、セラーだけでなく、アンチマルウェアスキャンプロバイダーなどの信頼できるサードパーティに対しても、可能な限り透明であるべきです。これにより、それらの当事者（技術的な知識がそれほど高くない担当者を含む）が、自社のインベントリで配信されるあらゆるクリエイティブの配信に誰が関与しているかを簡単に理解できるようになるべきです。

エージェンシーの身元のなりすましを防ぐための追加の透明性の取り組みを検討することや、信頼できない仲介者によるデマンドの操作を防ぐための暗号技術を探求することには利点がありますが、これらはいずれもこの初期の取り組みの範囲外です。

# 3 Implementation（実装）

DemandChain（または dchain）オブジェクトは、主に一連のノードで構成され、各ノードはインプレッションの購入に参加する特定のエンティティを表します。最初から最後までのノードのチェーン全体は、インプレッションとその中で実行されるクリエイティブの支払いの直接的な流れに関与するすべてのエンティティを表します。仕様の将来のバージョンには、トランザクションには関与しているが支払いには関与していないエンティティも含まれる可能性があります。

具体的には、完全な dchain は、最終的な支払い者（通常はブランドまたはセルフサービス広告主）と、インプレッションが配信される最終的なパブリッシャーの間のすべての仲介者を指定します。このチェーンのすべての参加者がプログラマティックに統合されているわけではない可能性があり、この点については以下のノード定義で詳しく説明します。

# 4 Node Definition（ノード定義）

ノードには、2 つの推奨プロパティ、広告システム識別子（`asi`）とバイヤーシート ID（`bsid`）が含まれています。これらのプロパティは、プログラマティックな広告システムでは存在しなければなりません（MUST）。ただし、`asi` と `bsid` は「推奨（recommended）」としてマークされています。これは、支払いチェーン内の非プログラマティックな参加者を表す場合に、そしてその場合にのみ、省略される可能性があるためです。

`asi` は広告システムのドメイン名です。`bsid` は、インベントリのバイヤー、つまり広告システムにこのクリエイティブの配信料金を支払っているのが誰かを識別するために使用されます。`asi` で識別されるドメイン名は、buyers.json ファイルをホストするドメインと一致するべきであり、`bsid` はそのファイル内で `buyer_id` として表示される値であるべきです。

`bsid` は、複数のエンティティが広告システムに支払いを行っている場合でも、複数のエンティティを表すことはできません。すべての `bsid` は、そのインプレッションの支払いを行うビジネスとして表される単一のエンティティにのみマップされなければなりません。この `bsid` は、すべてのインベントリトランザクションで使用されなければなりません。ただし、購入エンティティは、広告システム内に複数のバイヤーシート ID を持つ場合があります。

# 5 OpenRTB Object: DemandChain（OpenRTB オブジェクト: DemandChain）

このオブジェクトは、デマンドチェーン内のリンクと、デマンドチェーンが完全であるかどうかを示すインジケーターの両方を表します。

DemandChain オブジェクトは、OpenRTB 2.5 以降では `BidResponse.seatbid.bid.ext.dchain` 属性に含めるべきです（SHOULD）。OpenRTB 2.4 以前では、`BidResponse.ext.dchain` 属性を使用するべきです。

DemandChain オブジェクトには、次の属性が含まれます。

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| complete | integer; required | チェーンに、クリエイティブの創始者および最終的な支払い元に遡るトランザクションに関与するすべてのノードが含まれているかどうかを示すフラグ。0 = いいえ、1 = はい。 |
| nodes | object array; required | チェーンの順序における DemandChainNode オブジェクトの配列。完全なデマンドチェーンでは、最初のノードはトランザクションに関与する最初の広告システムとバイヤー ID、つまりクリエイティブの創始者および最終的な支払い元を表します。不完全なデマンドチェーンでは、最初の既知のノードを表します。最後のノードは、このビッドレスポンスを送信しているエンティティを表します。 |
| ver | string; required | 使用中の DemandChain 仕様のバージョン。「メジャー.マイナー」の形式。たとえば、仕様のバージョン 1.0 の場合は、文字列 "1.0" を使用します（数値は無効）。 |
| ext | object; optional | このオブジェクトへの広告システム固有の拡張のためのプレースホルダー。 |

# 6 OpenRTB Object: DemandChainNode（OpenRTB オブジェクト: DemandChainNode）

このオブジェクトは、ノードの配列として DemandChain オブジェクトに関連付けられます。これらのノードは、ビッドリクエストのサプライチェーンに参加しているエンティティの身元を定義します。DemandChainNode オブジェクトには、次の属性が含まれます。

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| asi | string; recommended | ビッドレスポンスを生成している DSP またはその他のバイヤーシステムの正規ドメイン名。これは、buyers.json ファイルをホストしているのと同じ場所であるべきです。このフィールドは、プログラマティックデマンドチェーンに関与するすべての ASI にとって必須ですが、最初の DSP に到達する前の支払いフローに関与するバイサイドエンティティについては省略される場合があります。存在する場合は、完全な URL ではなく、ホスト名またはドメインでなければなりません。正: domain.com。誤: [https://domain.com.](https://domain.com/) |
| bsid | string; recommended | 広告システム内のバイヤーシートに関連付けられた識別子。これには、トランザクションで使用される値（つまり、OpenRTB ビッドレスポンスの `BidResponse.SeatBid.Seat`）と同じ値が含まれていなければならず（MUST）、buyers.json ファイルに `buyer_id` として表示される値でなければなりません。長さは 64 文字以内に制限されるべきです。このフィールドは、プログラマティックデマンドチェーンに関与するすべての ASI にとって必須ですが、`asi` 自体が省略されている場合、つまり最初の DSP に到達する前の支払いフローに関与するバイサイドエンティティについては省略される場合があります。 |
| rid | string; optional | このセラーによって発行されたリクエストの OpenRTB ビッドリクエストまたはオークション ID（つまり、`BidRequest.id`）。 |
| name | string; recommended | 指定された `bsid` に基づいて支払っている会社（法的エンティティ）の名前。この値は推奨されますが、広告システムの buyers.json ファイルに存在する場合は（そしてそこで機密とマークされていない場合は）、含めるべきではありません（SHOULD NOT）。`asi` が不在または null の場合は、含めなければなりません（MUST）。 |
| domain | string; recommended | このノードによって表されるエンティティのビジネスドメイン名。この値は推奨されますが、広告システムの buyers.json ファイルに存在する場合は（そしてそこで機密とマークされていない場合は）、含めるべきではありません（SHOULD NOT）。バイヤーが文字通り Web プレゼンスを持っていない場合を除き、`asi` が不在または null の場合は、含めなければなりません（MUST）。 |
| ext | object; optional | このオブジェクトへの広告システム固有の拡張のためのプレースホルダー。 |

上記のフィールドはいずれも必須（required）として指定されていませんが、(`asi`, `bsid`) フィールドと (`name`, `domain`) フィールドの間には包含的な OR 関係が暗示されています。デマンドチェーンのプログラマティックな参加者は、`"asi"` および `"bsid"` 値を含めなければなりません（MUST）。非プログラマティックな参加者（したがって `"asi"` 値を含めることができない参加者）は、バイヤーが文字通り Web プレゼンスを持っていない場合を除き、`"domain"` 値と同様に `"name"` 値によって表されなければなりません。

この仕様は、非プログラマティックな参加者の `"name"` および `"domain"` 値を buyers.json ファイルに関連付けることができず、異なる dchain 開始者によって常に一貫して表現されない可能性があることを認識しています。それにもかかわらず、不完全に正規化された情報であっても、深刻な広告品質違反を特定するのに役立つという点で、依然として方向性としては価値があります。

一部の当事者が、buyers.json に機密エントリを記載している場合、dchain ノードの `"name"` および `"domain"` フィールドを使用して、個々のビッドレスポンスのレベルでこれらのエンティティに関する情報を個人的に共有することもできる点に注意してください。

# 7 Implementation Details（実装詳細）

広告システムがこのインベントリのビッドリクエストを発信している場合、システム上のバイヤーの身元を示すノードを持つ DemandChain オブジェクトを作成するべきです。このバイヤーが最終的な支払い者である場合、DemandChain オブジェクトには 1 の `"complete"` 属性を含めるべきであり、これが `"nodes"` 配列内の唯一のノードであるべきです。

そのバイヤーが最終的な支払い者ではなく、広告システムがチェーン内の追加の支払い者を認識している場合、可能な限り多くの中間支払い者を含めるべきです。リストが完全であることがわかっている場合、DemandChain オブジェクトには 1 の `"complete"` 属性を含めるべきです。それ以外の場合、DemandChain オブジェクトに示されている支払い者以外にも支払い者がいることがわかっている場合は、`"complete"` 属性を 0 に設定しなければなりません。

リセラーが前のセラーからの DemandChain オブジェクトを、チェーンに自分のノードを挿入せずにそのインベントリのリクエストにコピーすることは無効です。リセラーが自分自身をチェーンに挿入しない場合、そのビッドリクエストには、受け取った変更されていない DemandChain オブジェクトを含めてはなりません（MUST NOT）。

広告システムが、以前に DemandChain オブジェクトを含んでいなかったビッドレスポンスを渡している場合、DemandChain オブジェクト自体を作成し、`"complete"` 属性を 0 の値でマークし、そのノードを `"nodes"` 配列に挿入するべきです。

広告システムが、DemandChain オブジェクトを持つビッドレスポンスを渡している場合、広告システムは既存のオブジェクトをコピーし、`"complete"` フラグの元の値を保持し、そのノードを `"nodes"` 配列の末尾に追加するべきです。

# 8 Validation & Enforcement Guidance（検証および強制のガイダンス）

集団的な参加に基づくソリューションとして、buyers.json と DemandChain には、各当事者がエントリを検証し、仕様への準拠を強制する方法についての共通の理解が必要です。

DemandChain オブジェクトにノードを追加する広告システムは、前のノードの構文形式をリアルタイムで検証するべきです。

*   前のノードが構文検証に合格した場合、広告システムは新しいノードを追加して続行できます。
*   前のノードが構文検証に失敗した場合、広告システムは独自のポリシーと好みに基づいて、それをどのように処理するかを選択できます。

壊れた構文は体系的な問題を示すことが多いため、エラーは少なくともログに記録して調査するべきです。広告システムは、ビッドレスポンス全体を破棄するなど、より厳格な措置を講じることも選択できます。広告システムが、構文的に無効な DemandChain オブジェクトを含むビッドレスポンスを処理する場合、その無効なオブジェクトを渡すべきではありませんが、代わりに complete を 0 に設定した新しい DemandChain オブジェクトを開始するべきです。

広告システムは、後でビジネスルールに対して非同期分析を行うために DemandChain ノードをログに記録することを選択することもできます（例：前の DemandChain ノードのバイヤー情報をバイヤーの buyers.json ファイルのリスト情報と照合して確認する、新しいシートの最初の出現を記録する、またはその他のより複雑な論理的観察など）。リアルタイムで実行する必要はありませんが、この情報をログに記録し、分析し、監視することは、サプライチェーン全体のデータ品質の向上につながるため、それが可能なシステムには期待されています。

# 9 Serializing and Exposing Creative Source Data（クリエイティブソースデータのシリアル化と公開）

クライアントに配信されるアドマークアップ内で、広告クリエイティブに関する限られたデータを公開すると便利です。これにより、パブリッシャーの広告運用担当者やサードパーティのアンチマルウェアベンダーなど、ビッドストリームデータにアクセスできない参加者が、問題のある広告を容易に特定できるようになります。

これは、OpenRTB 2.5 以降の `BidResponse.seatbid.bid.ext.dchain` 属性で dchain オブジェクトを渡す代わりではなく、追加として役立ちます。

したがって、DSP、または OpenRTB または同様のプログラマティックビッドレスポンスに表示されるアドマークアップを最初に生成するその他の当事者は、次のクリエイティブソースデータを予測可能な方法でアドマークアップにシリアル化することが推奨されます。

*   DSP ドメイン
*   バイヤーシート ID
*   クリエイティブ ID

バージョニングとプラットフォーム固有の拡張をサポートするために、これらの属性は次のようにカンマ区切りの文字列にシリアル化されるべきです。

ver,dsp\_domain,buyer\_seat\_id,creative\_id,ext

*   `ver` は、この DemandChain 仕様に準拠してシリアル化されたクリエイティブソースデータの場合、常に `1.0` であるべきです。
*   `dsp_domain` は、DSP の buyers.json ファイルが見つかるドメインであるべきです。
*   `buyer_seat_id` は、DSP のプラットフォーム上のバイヤーシート ID であるべきです。通常、これはビッドレスポンスの `BidResponse.SeatBid.Bid.seat` フィールドで使用される値であり、DSP の buyers.json ファイルに存在する `bsid` 値でもあります。
*   `creative_id` は、DSP がクリエイティブを識別するために使用する一意の識別子であり、通常はビッドレスポンスの `BidResponse.SeatBid.Bid.crid` 値です。
*   `ext` は、プラットフォーム固有の拡張を可能にするためのプレースホルダーです。存在する場合、このデータの形式は実装定義です。

値にカンマ、パーセント記号、またはその他の安全でない可能性のある文字が含まれる可能性のあるフィールドは、RFC 3986 に従って URL エンコードされなければなりません。値が存在しないか適用できないフィールドは、空の文字列で表されるべきです。末尾のカンマは、オプションで省略できます。

例:

```
1.0,mydsp.example,ac1f9e,89708971
```

この例は、mydsp.example のバイヤーシート（ac1f9e）とクリエイティブ ID（89708971）を表しています。

```
1.0,opaquedsp.example,,1472%2C20%25%20off%20300x250,
```

この例は、バイヤーシートが欠落しており（3 番目の値が空）、クリエイティブ ID（1472）と説明（%2C20%25%20off%20300x250、デコードすると 20% off 300x250）があり、拡張オブジェクトが空（後に何もないカンマが存在する）である opaquedsp.example を表しています。

## Embedding of Serialized Data in Ad Markup（アドマークアップへのシリアル化データの埋め込み）

クリエイティブソースデータの観察者による識別と解析を簡素化するために、シリアル化されたクリエイティブソースデータを、次のような標準化された識別子の一部としてアドマークアップで公開することが推奨されます。

```
data-ad-creative-source="*serialized_data*"
```

アドマークアップ内のこの識別子の場所は、クリエイティブの種類と実装の詳細によって異なります。HTML アドマークアップの場合、優先される場所は、最も外側の HTML タグの属性として表示されることです。

`serialized_data` は、二重引用符、バックスラッシュなどの特殊文字が含まれている場合に属性値に安全に埋め込むことができるように、HTML エスケープされるべきです。

最も外側の HTML タグは実装固有の詳細ですが、次のようになる場合があります。

```
<div name="adm" data-ad-creative-source="1.0,mydsp.example,ac1f9e,89708971">
...
</div>
```

または次のようになります。

```
<iframe name="adm" src="https://assets.mydsp.example/c/89708971" data-ad-creative-source="1.0,mydsp.example,ac1f9e,89708971">
...
</iframe>
```

あるいは、識別子は HTML コメントとして埋め込まれる場合があります。

```
<!-- data-ad-creative-source="1.0,mydsp.example,ac1f9e,89708971" -->
```

または JavaScript コメントとして：

```
// data-ad-creative-source="1.0,mydsp.example,ac1f9e,89708971"
```

これらの埋め込みはいずれも、単純な文字列一致または人間による検査による容易な識別を可能にします。

VAST クリエイティブなどに使用される XML アドマークアップの場合、推奨される埋め込みは、フォーマットに定義された標準拡張オブジェクト内に `data-ad-creative-source` 属性を含む `AdCreativeSource` タグを作成することです。`serialized_data` は、二重引用符、バックスラッシュなどの特殊文字が含まれている場合に属性値に安全に埋め込むことができるように、XML エスケープ（事実上 HTML エスケープと同じ）されるべきです。この埋め込みは、クリエイティブソースデータを埋め込む標準的かつ構造化された方法を提供すると同時に、使い慣れた方法で文字列一致を実行する機能を維持するという二重の目的を果たします。

たとえば、VAST の場合：

```
<Extensions>
  <Extension>
    <AdCreativeSource data-ad-creative-source="1.0,mydsp.example,ac1f9e,89708971">
  </Extension>
</Extensions>
```

# 10 Examples（例）

完全な DemandChain には、最終的な支払い者（通常はブランドまたはセルフサービス広告主）と最終的なパブリッシャーの間のすべての仲介者が含まれます。比較的単純なケースでは、これは次のように表される場合があります。

```
*Advertiser -> DSP -> SSP -> Publisher*
```

特に複雑なケースでは、次のようになる可能性があります。

```
*Brand -> Agency/Holdco -> DSP of record -> additional reselling DSP -> SSP/agg1 -> SSP/agg2 -> SDK provider -> Publisher*
```

これらの仲介者の一部、特に記録上の DSP（DSP of record）の前の仲介者は、プログラマティックに統合されていない場合があります。したがって、実際問題として、ビッドレスポンスを開始する最初の DSP は、可能な範囲で、dchain を開始し、DSP の下流にある非プログラマティックな支払い関係を識別するべきです。ビッドレスポンスを処理する各エンティティは、順番に dchain にリンクを追加しなければなりません。

例:

アプリ開発者が HypotheticalMobileMoney SDK を使用して SSP1 にビッドリクエストを送信し、SSP1 はそれをさまざまな DSP にファンアウトします。PopularDSP は、FamousBrand を代表する AOR（指定代理店）である RespectedAdAgency からの入札で応答します。

PopularDSP は最初に次のように応答します。

```json
"dchain": {
  "ver": "1.0",
  "complete": 1,
  "nodes": [
    {
      "asi": null,
      "name": "FamousBrand",
      "domain": "famousbrand.example"
    },
    {
      "asi": null,
      "name": "RespectedAdAgency",
      "domain": "respectedadagency.example"
    },
    {
      "asi": "populardsp.example",
      "bsid": "12345"
    }
  ]
}
```

dchain のコンシューマーは、populardsp.example にある PopularDSP の buyers.json ファイルを参照して、bsid 12345 が実際にエンティティ RespectedAdAgency にマップされていることを確認できます。

その後、SSP1 はビッドレスポンスを処理し、HypotheticalMobileMoney に渡す際にチェーンを拡張します。

```json
"dchain": {
  "ver": "1.0",
  "complete": 1,
  "nodes": [
    {
      "asi": null,
      "name": "FamousBrand",
      "domain": "famousbrand.example"
    },
    {
      "asi": null,
      "name": "RespectedAdAgency",
      "domain": "respectedadagency.example"
    },
    {
      "asi": "populardsp.example",
      "bsid": "12345"
    },
    {
      "asi": "ssp1.example",
      "bsid": "202049"
    }
  ]
}
```

dchain のコンシューマーは、populardsp.example（※原文ママ、文脈から ssp1.example の間違いの可能性が高いが翻訳では原文を尊重するか、注釈を入れるか。ここでは ssp1.example の buyers.json を見るのが正しいはず。原文: "consult the buyers.json file for SSP1 at populardsp.example"。これは原文の誤植の可能性が高い。SSP1 のドメインは `ssp1.example` となっている。ガイドラインは「原文の要件・定義・実装上の注意点を正確に伝え」るのが目的なので、明らかな誤植は修正して注記するか、そのまま訳して注記するか。ガイドには指示がないが、通常は誤植と思われる場合は訳注を入れるのが親切。しかし、URL/ドメインなどの technical details なので原文通りにしておくのが無難。）にある SSP1 の buyers.json ファイルを参照して、bsid 202049 が実際にエンティティ PopularDSP（populardsp.example）にマップされていることを確認できます。（SSP1 は SSP ですが、ビッドレスポンスが最終的なパブリッシャーに到達する前にそれに触れる最後の SSP であるとは限りません。）

セルフサービス指向の DSP を介したセルフサービス広告主の場合:

```json
"dchain": {
  "ver": "1.0",
  "complete": 1,
  "nodes": [
    {
      "asi": null,
      "name": "John's Groovy E-Commerce Business",
      "domain": "johnsgroovy.example"
    },
    {
      "asi": "selfservicedsp.example",
      "bsid": "af67ca81928ad90e"
    }
  ]
}
```

SSP1 が dchain のないビッドレスポンスを受信した場合、SSP1 は dchain を開始します。

```json
"dchain": {
  "ver": "1.0",
  "complete": 0,
  "nodes": [
    {
      "asi": "ssp1.example",
      "bsid": "123456789"
    }
  ]
}
```

DSP が、直接契約しているパートナー以外の関係を知らないか、共有できない場合:

```json
"dchain": {
  "ver": "1.0",
  "complete": 0,
  "nodes": [
    {
      "asi": null,
      "name": "An Agency",
      "domain": "anagency.example"
    },
    {
      "asi": "majordsp.example",
      "bsid": "12345"
    }
  ]
}
```
