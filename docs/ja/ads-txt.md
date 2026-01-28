---
title: "ads.txt"
description: "ads.txt 仕様 Version 1.1 - パブリッシャーが自社のインベントリの販売権限を持つ者を公に宣言できるようにする仕様"
---

ads.txt

Version 1.1

Released August 2022

ご意見やご質問は support@iabtechlab.com までメールでお寄せください。このドキュメントは [https://iabtechlab.com/ads.txt/](https://iabtechlab.com/ads.txt/) でオンライン公開されています。

© IAB Technology Laboratory

# About ads.txt (ads.txt について)

ads.txt 仕様は 2017 年春に開発されました。本ドキュメントは ads.txt 仕様バージョン 1.1 の最終版であり、Programmatic Supply Chain ワーキンググループの支援を受けて開発された、ピアレビュー済みの標準規格です。このドキュメントは [https://iabtechlab.com/ads-txt](https://iabtechlab.com/ads-txt) で入手可能です。

ads.txt 仕様は、パブリッシャーが自社のインベントリ（広告在庫）の販売権限を持つ者を公に宣言できるようにすることで、ads.txt ファイルを公開しているウェブサイトがホストするインベントリを保護することを目的としています。モバイルアプリストア、コネクテッドテレビアプリストア、およびその他同様の配信チャネルを通じて配布されるソフトウェアアプリケーションの要件を満たすには、同じく [https://iabtechlab.com/ads-txt](https://iabtechlab.com/ads-txt) で入手可能な app-ads.txt 仕様を参照してください。

# About IAB Tech Lab (IAB Tech Lab について)

IAB Technology Laboratory は、非営利の研究開発コンソーシアムであり、世界的な業界技術標準およびソリューションの作成と導入支援を担っています。Tech Lab の目標は、デジタル広告およびマーケティングのサプライチェーンに関連する摩擦を減らしつつ、業界の安全な成長に貢献することです。

IAB Tech Lab は技術標準の開発を主導し、IAB 標準の迅速かつコスト効率の高い実装を支援するためのコードライブラリを作成・維持し、企業が自社の技術ソリューションと IAB 標準との適合性を評価するためのテストプラットフォームを確立しています。IAB 標準は 18 年間にわたり、デジタル広告サプライチェーンにおける相互運用性と収益性の高い成長の基盤となってきました。IAB Technology Lab の詳細については、[https://iabtechlab.com](https://iabtechlab.com/) をご覧ください。

### License (ライセンス)

Ads.txt by Programmatic Supply Chain Working Group is licensed under a Creative Commons Attribution 3.0 License. To view a copy of this license, visit creativecommons.org/licenses/by/3.0/ or write to Creative Commons, 171 Second Street, Suite 300, San Francisco, CA 94105, USA.

### Disclaimer (免責事項)

THE STANDARDS, THE SPECIFICATIONS, THE MEASUREMENT GUIDELINES, AND ANY OTHER MATERIALS OR SERVICES PROVIDED TO OR USED BY YOU HEREUNDER (THE “PRODUCTS AND SERVICES”) ARE PROVIDED “AS IS” AND “AS AVAILABLE,” AND IAB TECHNOLOGY LABORATORY, INC. (“TECH LAB”) MAKES NO WARRANTY WITH RESPECT TO THE SAME AND HEREBY DISCLAIMS ANY AND ALL EXPRESS, IMPLIED, OR STATUTORY WARRANTIES, INCLUDING, WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AVAILABILITY, ERROR-FREE OR UNINTERRUPTED OPERATION, AND ANY WARRANTIES ARISING

FROM A COURSE OF DEALING, COURSE OF PERFORMANCE, OR USAGE OF TRADE. TO THE EXTENT THAT TECH LAB MAY NOT AS A MATTER OF APPLICABLE LAW DISCLAIM ANY IMPLIED WARRANTY, THE SCOPE AND DURATION OF SUCH WARRANTY WILL BE THE MINIMUM PERMITTED UNDER SUCH LAW. THE PRODUCTS AND SERVICES DO NOT CONSTITUTE BUSINESS OR LEGAL ADVICE. TECH LAB DOES NOT WARRANT THAT THE PRODUCTS AND SERVICES PROVIDED TO OR USED BY YOU HEREUNDER SHALL CAUSE YOU AND/OR YOUR PRODUCTS OR SERVICES TO BE IN COMPLIANCE WITH ANY APPLICABLE LAWS, REGULATIONS, OR SELF-REGULATORY FRAMEWORKS, AND YOU ARE SOLELY RESPONSIBLE FOR COMPLIANCE WITH THE SAME, INCLUDING, BUT NOT LIMITED TO, DATA PROTECTION LAWS, SUCH AS THE PERSONAL INFORMATION PROTECTION AND ELECTRONIC DOCUMENTS ACT (CANADA), THE DATA PROTECTION DIRECTIVE (EU), THE E-PRIVACY DIRECTIVE (EU), THE GENERAL DATA PROTECTION REGULATION (EU), AND THE E-PRIVACY REGULATION (EU) AS AND WHEN THEY BECOME EFFECTIVE.

### Significant Contributors to the 1.1 Release: (1.1リリースへの主な貢献者)

Justin Adler-Swanberg, Director Marketplace Quality, MediaMath; Paul Bannister, Chief Strategy Officer, CafeMedia; Per Bjorke, Group Product Manager, Google; Eric Bozinny, Sr Director Marketplace Quality, Pubmatic; Katie Chang, Sales Operations & Strategy Lead, Yahoo; Zack Dugow, Founder and CEO, Insticator; Emma Fenlon, Sr. Manager Exchange Quality, Yahoo; Jeremy Grant, Sr. Product Manager, Index Exchange; Chris Kane, Founder, Jounce Media; Curt Larson, Chief Product Officer, Sharethrough; Curtis Light, Staff Software Engineer, Google; Don Marti, VP Ecosystem Innovation, CafeMedia; Kristen Moegling, Sr.

Technical Solutions,Triplelift; Angie Pennington, Sales and Operations Strategy Lead, Yahoo; Neal Richter, Director, Advertising Science, Amazon DSP, Jud Spencer, Principal Lead Software Engineer, The Trade Desk; Brian Van Horne, Director of Engineering, Magnite; Jean-Luc Wasmer, VP Partnership Integrations, Triton Digital; Liam Whiteside, Head of Ad Technology, Global; Anna Wolk, Marketplace Quality, The Trade Desk;

### IAB Tech Lab Lead: (IAB Tech Lab リード)

Jill Wittkopp, Sr. Director Product, IAB Tech Lab

# 1 ABSTRACT (概要)

オープンなデジタル広告エコシステムにおいて偽造インベントリから利益を得る行為を排除するための広範な取り組みの一環として、コンテンツ所有者が自社のインベントリの販売権限を持つ者を宣言できるようにするメカニズムを提供します。

# 2 INTRODUCTION (はじめに)

簡潔にするため、読者はアドテクにおける不正の問題とその規模の大きさ [1],[2],[3] について、すでに精通しているものと仮定します。不正にはさまざまな形態がありますが、ここでは、リアルタイムビディング (RTB) プロセスにおいて、インベントリが誤ったラベルやアカウントを使用してバイヤーに提供される形態に焦点を当てます。一般的に、ウェブページのドメインやモバイルアプリの ID が偽造され、本来販売権限を持たないサイトやアプリであるかのように見せかけられます。

本ドキュメントでは、コンテンツ所有者が、自社のインベントリの販売権限を持つ広告システムおよびリセラーのセットを明示的に宣言できるようにする新しい標準規格を提案します。これにより、バイヤーは承認されたエンティティを経由した安全なサプライチェーンを通じて広告枠を購入できるようになります。

## 2.1 CHANGE LOG (変更履歴)

| **Version** | **Date** | **Changes** |
|---|---|---|
| 1.0 | June 27, 2017 | 初版 |
| 1.0.1 | August 30, 2017 | コミュニティからのフィードバックに基づく軽微な修正。3.1 の明確化、および 3.2、3.5、4.4、4.5、5.5 における contact 変数と subdomain 変数のサポート追加。 |
| 1.0.2 | March 4, 2019 | コミュニティからのフィードバックに基づく軽微な修正。空の ads.txt ファイルの意図を示すためにプレースホルダーレコードを使用するガイダンスを含む 3.2.1 および 4.7 を追加し、以前の方法を非推奨化。「About」セクションに ads.txt と app-ads.txt の区別を追加。 |
| 1.0.3 | December 2020 public comment March 2021 – final release | CTV や類似のユースケースを支援するために `inventorypartnerdomain` ディレクティブを追加（詳細は 4.6 および 5.7 を参照）。 |
| 1.1 | April 2022 public comment July 2022 final release | `managerdomain` および `ownerdomain` 変数を追加（詳細は 3.5.1、4.7、4.8、5.8、5.9 を参照）。 |

# 3. SPECIFICATION (仕様)

このメモは、パブリッシャーであるコンテンツ配信者が、承認された広告システムおよびそれらのシステム内での識別子を公に宣言するためのメカニズムを規定します。この仕様は、OpenRTB ビッドリクエスト内の `site.domain` や `app.bundle`、または他の取引方法における同等の情報と組み合わせて使用されることを想定しています。また、広告システムおよびその顧客が利用するための指示をエンコードする形式についても記述します。広告システムは、そのウェブサイト上にあると主張する広告を購入または販売する前に、これらの宣言を取得するべきです（SHOULD）。

この仕様は、特に robots.txt 標準 [5][6] に着想を得ています。重要な特性として、ファイルがコンテンツのウェブ配信システムに配置されるため、そのウェブサイトがファイルを作成したことが証明されます。リアルタイムの広告枠販売については IAB Tech Lab の OpenRTB [7] や Google の AdX API [8]、非リアルタイムの販売については IAB Tech Lab の OpenDirect [9] など、他のさまざまな広告 API 仕様を参照してください。

## 3.1 ACCESS METHOD (アクセス方法)

パブリッシャーは、ルートドメインおよび必要に応じてサブドメインに `/ads.txt` ファイルを投稿するべきです（SHOULD）。本ドキュメントの目的において、「ルートドメイン」は「パブリックサフィックス」に名前の文字列を 1 つ加えたものとして定義されます。クローラーは、ルートドメインを導出するために Public Suffix List [16] を組み込むべきです（SHOULD）。
宣言は、指示が適用されるウェブサイトから、サーバーホスト上の標準的な相対パス `/ads.txt` で、かつ HTTP リクエストヘッダーに `Content-Type: text/plain` を含める形で、HTTP および/または HTTPS 経由でアクセス可能でなければなりません（MUST）。さらに `Content-Type: text/plain; charset=utf-8` を使用して UTF8 サポートを示すことも推奨されます。

また、ads.txt ファイルをクロールする際には、HTTP よりも HTTPS 接続を優先することが推奨されます。同じ URL に対して HTTPS と HTTP の両方の接続でデータが利用可能な場合は、HTTPS からのデータを優先するべきです（SHOULD）。

便宜上、このリソースを `/ads.txt` ファイルと呼びますが、実際にはリソースがファイルシステム由来である必要はありません。

サーバーレスポンスが Success（HTTP 2xx ステータスコード）を示す場合、広告システムはコンテンツを読み取り、解析し、宣言を利用しなければなりません（MUST）。

サーバーレスポンスが HTTP/HTTPS リダイレクト（301、302、307 ステータスコード）を示す場合、リダイレクトが上記で定義された元のルートドメインの範囲内である場合に限り、広告システムはリダイレクトに従い、リダイレクト元の正当なデータとして利用するべきです（SHOULD）。元のルートドメイン内に留まる限り、複数のリダイレクトも有効です。たとえば、同じルートドメイン内での HTTP から HTTPS へのリダイレクトは有効です。

第三者のウェブサーバーサイトへの権限のワンホップ委任を促進するために、元のルートドメイン外の宛先への HTTP リダイレクトは 1 回だけ許可されます。第三者の場所がさらにリダイレクトを返す場合、広告システムはそのレスポンスをエラーとして扱うべきです（SHOULD）。将来のバージョンでは、第三者ウェブサーバーへの他の権限委任に対応する可能性があります。その他すべてのリダイレクトはエラーとして解釈して無視するべきです（SHOULD）。

サーバーレスポンスがリソースへのアクセス制限（HTTP 401）を示す場合、広告システムは認証キーまたは説明を求めてサイトに直接連絡するべきです（SHOULD）。

サーバーレスポンスがリソースが存在しないこと（HTTP ステータスコード 404）を示す場合、広告システムは、宣言が存在せず、いかなる広告システムもそのウェブサイトでの広告売買が無許可ではない（つまり制限がない）と見なすことができます。以前にクローラーがデータを発見した URL でその他の HTTP エラーが発生した場合、最後に正常に取得されたデータセットを利用するべきです（SHOULD）。

## 3.2 FILE FORMAT (ファイル形式)

データは、ここで説明するようにフォーマットされたプレーンテキストオブジェクトとしてエンコードされます。HTTP Content-type は `text/plain` であるべきです（SHOULD）。それ以外の Content-type はエラーとして扱い、コンテンツは無視するべきです（SHOULD）。この形式の構文の完全な説明は、以下のセクション 3.4 に記載されています。

論理的な形式は以下で構成されます：

- 改行で区切られた空ではないレコードのセット。レコードは以下の形式の行のセットで構成されます：

  `<FIELD #1>, <FIELD #2>, <FIELD #3>, <FIELD #4>`

  または

  `<VARIABLE>=<VALUE>`

- `#` 記号で始まる行はコメントと見なされ、無視されます。
- データ形式を含む行の構文はセクション 3.4 で定義されます。
- 変数形式を含む行の構文はセクション 3.5 で定義されます。

### 3.2.1 FILES WITHOUT AUTHORIZED ADVERTISING SYSTEM RECORDS (承認された広告システムレコードのないファイル)

一部のパブリッシャーは、空の ads.txt ファイルを公開することで、いかなる広告システムも承認しないことを選択し、そのウェブサイトでの広告売買が許可されている広告システムがないことを示す場合があります。利用システムが空のファイルを適切に読み取り解釈できるようにするため（ウェブサーバーが `/ads.txt` URL に対してエラーページを返す場合と区別するため）、上記の形式仕様に準拠した正しくフォーマットされた行が少なくとも 1 行含まれていなければなりません（MUST）。その他に承認された広告システムレコードを含まないファイルの場合、ファイルが ads.txt 仕様に準拠していることを示すために、以下の「プレースホルダー」レコードを使用してください：

```
placeholder.example.com, placeholder, DIRECT, placeholder
```

ドメイン `example.com` に特別な意味はありません。これは、行が適切にフォーマットされ、実際の広告システムドメインの代わりに恒久的に予約された代替ドメイン（[https://tools.ietf.org/html/rfc6761](https://tools.ietf.org/html/rfc6761)）で始まるようにするために使用されています。

以前のバージョンの ads.txt 仕様では、パブリッシャーは単に空の ads.txt ファイルを使用して、そのウェブサイトでの広告売買が承認されている広告システムがないことを示してもよいとされていました。この方法は曖昧さを生むため現在は非推奨となっており、利用システムは 2020 年 3 月 1 日以降、これを無視するべきです（SHOULD）。

### 3.2.2 THE DATA RECORD (データレコード)

以下は各フィールドの内容を定義します。必要に応じて IAB OpenRTB [7] および IAB OpenDirect [9] 仕様を参照します。

| **FIELD** | **NAME** | **DESCRIPTION** |
|---|---|---|
| Field #1 | Domain name of the advertising system | （必須）ビッターが接続する SSP、エクスチェンジ、ヘッダーラッパーなどのシステムの正規ドメイン名。これは親会社のドメインとは異なる場合があり、委任されたシステムの明確な所有権を確立するための WHOIS や逆引き IP ルックアップを容易にするために、システムの運用ドメインである場合があります。理想的には、SSP またはエクスチェンジは使用すべきドメイン名を詳述したドキュメントを公開します。 |
| Field #2 | Publisher's Account ID | （必須）Field #1 の広告システム内のセラーまたはリセラーアカウントに関連付けられた識別子。これには、SSP/エクスチェンジによって指定されたフィールド内のトランザクション（つまり OpenRTB ビッドリクエスト）で使用されるのと同じ値を含まなければなりません（MUST）。通常、OpenRTB ではこれは `publisher.id` です。OpenDirect の場合は通常、パブリッシャーの組織 ID です。 |
| Field #3 | Type of Account/ Relationship | （必須）アカウントタイプの列挙。値 `DIRECT` は、パブリッシャー（コンテンツ所有者）が Field #1 のシステム上の Field #2 に示されるアカウントを直接管理していることを示します。これは通常、パブリッシャーと広告システム間の直接的なビジネス契約を意味します。値 `RESELLER` は、パブリッシャーが Field #2 に示されるアカウントを管理する別のエンティティに対し、Field #1 のシステムを通じて広告枠を再販することを許可したことを示します。将来的に他のタイプが追加される可能性があります。なお、このフィールドはデータを解釈する際に大文字と小文字を区別しないものとして扱われるべきです（SHOULD）。 |
| Field #4 | Certification Authority ID | （オプション）認証局内で広告システムを一意に識別する ID（この ID は Field #1 にリストされたエンティティにマップされます）。現在の認証局としては Trustworthy Accountability Group（別名 TAG）があり、TAGID がここに含まれます [11]。認証 ID の宣言は sellers.json の _identifiers_ オブジェクトに取って代わられます。注：このフィールドは将来の ads.txt バージョンで非推奨となる可能性があります。 |

親会社が複数の異なる SSP/エクスチェンジを運営している場合、Field #1 のドメインは、ビッターがビッドリクエストを受け取っている RTB 接続のドメインを参照するべきであることに注意してください。

Field #4 の認証 ID は「広告システム」（例：SSP）に接続されており、sellers.json ファイル内で宣言することが推奨されます。

## 3.4 SYNTAX DEFINITION (構文定義)

### 3.4.1 COMMENTS (コメント)

コメントは文字 `#` で示されます。`#` を含む行は、データ利用者に対し、`#` 文字の後から行末までのデータを無視するよう通知するべきです（SHOULD）。

### 3.4.2 THE RECORD (レコード)

コア構文はカンマ区切り形式で、3 つの定義されたフィールドを持ち、1 行につき 1 レコードです。

利用システムは、一連の空白やタブを無視するべきです（SHOULD）。データが明らかに破損しているか形式が不正な場合、ファイルの内容は無視されるべきです（SHOULD）。フィールドはタブ、カンマ、空白を含まないべきです（SHOULD NOT）。含める場合は、URL エンコード [13] でエスケープするべきです（SHOULD）。

個々のレコードは行末マーカーで区切られます。利用システムは CR、CRLF などをレコード区切り文字として寛容に解釈するべきです（SHOULD）。

Field #1 で許可される識別子は、定義上、RFC 1123 [10]、RFC 1123 の関連正誤表、または包括的な RFC に従う有効な DNS ドメイン名であると見なされます。
Field #2 の識別子は文字列または整数です。参考として、OpenRTB の `publisher.id` [14] は文字列フィールドです。

### 3.4.3 EXTENSION FIELDS (拡張フィールド)

拡張フィールドは、各レコードに拡張データを追加する前に明確な最終区切りフィールド `;` を利用する限り、実装者とその利用者によって許可されます。

## 3.5 VARIABLE DECLARATION RECORDS (変数宣言レコード)

`<VARIABLE>=<VALUE>` のパターンを含む行はすべて変数宣言として解釈し、クローラーはそのデータをルートドメインに関連付けて保存するべきです（SHOULD）。

`<VARIABLE>` は内部に空白を持たない文字列識別子です。サポートされる唯一の区切り文字は等号 `=` です。`<VALUE>` は任意のデータを含むことができるオープンな文字列です。

宣言行は行末マーカーで終了します。利用システムは CR、CRLF などを行区切り文字として寛容に解釈するべきです（SHOULD）。

人間が読みやすくするために、変数はファイルの末尾に宣言することが推奨されますが、これは厳密な要件ではなく、クローラーがこれを前提とすべきではありません。

### 3.5.1 SUPPORTED VARIABLES (サポートされる変数)

以下の変数が正式にサポートされています。将来的に他の変数が追加される可能性があります。クローラーが同じ変数を持つ複数の行を見つけた場合、それらすべてを読み取り、ルートドメインに関連付けて保存するべきです（SHOULD）。

| **VARIABLE** | **VALUE** | **DESCRIPTION** |
|---|---|---|
| CONTACT | 連絡先情報 | （オプション）ファイルの所有者に関する人間が読める連絡先情報。ウェブサイトの広告運用チームの連絡先の場合があります。これには、メールアドレス、電話番号、お問い合わせフォームへのリンク、またはその他の適切な通信手段などが含まれます。 |
| SUBDOMAIN | サブドメインファイルへのポインタ | （オプション）ads.txt が存在するルートドメイン内のサブドメインへの機械可読なサブドメインポインタ。クローラーはデータを取得し、現在のドメインではなくサブドメインに関連付けるべきです（SHOULD）。この参照は、パブリックサフィックス切り捨てプロセスの対象外であるべきです。ルートドメインのみがクローラーをサブドメインに参照させるべきです。サブドメインは他のサブドメインを参照するべきではありません。 |
| INVENTORYPARTNERDOMAIN | アプリケーションのコンテンツ内で広告を収益化することを明示的に許可されたエンティティのドメインへのポインタ。パートナーの対応する ads.txt ファイルはこのドメインでホストされます。 | （関連する場合に推奨）サイトまたはアプリが別のパートナーによって所有されるインベントリを含む場合、アプリまたはサイトは、そのパートナー配下のすべての関係について個別の行を維持する従来の方法ではなく、このディレクティブを通じてそれらパートナーのすべてのドメインをリストできます。`INVENTORYPARTNERDOMAIN` 参照は ads.txt ファイルのみ（app-ads.txt ではない）をたどることが期待されます。この機能は広告システムとの調整が必要なため、詳細については実装者向けノートを参照してください。 |
| OWNERDOMAIN | ドメイン/サイト/アプリを所有する事業体のビジネスドメインを指定します（例：`example.com` は `example1.com`、`example2.com` などを所有）。 | （推奨）これは、参照される sellers.json ファイル内のこのパブリッシャーのエントリにおける `sellers.domain` と同じ値であるべきです（SHOULD）。`sellers.domain` と同様に、これは完全なホスト名や URL ではなく、Public Suffix List+1 であるべきです（SHOULD）。完全な OpenRTB SupplyChain オブジェクトの場合、発信元のパブリッシャーを表すノード（schain オブジェクトの最初にリストされるノード）は、`OWNERDOMAIN` と一致する `sellers.domain` を持つべきです（SHOULD）。この変数のインスタンスが複数含まれている場合、最初のもののみが使用されるべきです（SHOULD）。`OWNERDOMAIN` が ads.txt ファイルが見つかったドメインと同じであっても、このフィールドを含めることが推奨されます。また、バイヤーは、sellers.json で `BOTH` としてリストされているセラーに対し、所有または代表するすべての ads.txt ファイルに `OWNERDOMAIN` を正しくリストすることを義務付けることが推奨されます。 |
| MANAGERDOMAIN | パブリッシャーのインベントリの主要または独占的な収益化パートナーのビジネスドメインを指定します。 | （オプション、関連する場合のみ使用）サイトの所有者がグローバルまたは特定の国で収益化を管理していない場合、独占的な管理会社のドメインがこの変数に含まれます。ドメインの構文は `[PSL+1 ドメイン, 必須]`, `[ISO 3166-1 alpha-2 国コード, オプション, 空白=グローバル]` です。この変数は、パブリッシャーではないものの、このサイトの主要または独占的なプログラマティックセラーであるセラーに対してのみ使用されるべきです（SHOULD）。これは通常、パブリッシャーが特定の市場で自身のインベントリを販売していない場合にのみ適用されます。マネージャーによって収益化される広告機会において、`MANAGERDOMAIN` にリストされたドメインは、完全な SupplyChain オブジェクト内の発信元のパブリッシャーを表すノードのドメインでもあることが期待されます。`MANAGERDOMAIN` 値は複数存在できますが、国ごとに 1 つだけです。グローバル/デフォルトの `MANAGERDOMAIN` は、変数行に国「拡張」を持つべきではありません。デフォルトは、国拡張を含む他のエントリによってオーバーライドできます。国宣言の形式については例を参照してください。ユースケースと潜在的な SPO への影響の詳細については、実装ガイドを参照してください。 |

## 3.6 EXPIRATION (有効期限)

`/ads.txt` の利用システムはファイルをキャッシュするべきですが（SHOULD）、そうする場合、コンテンツを使用する前にキャッシュされたコピーが最新であることを定期的に確認しなければなりません（MUST）。

オリジンサーバーとロボットの両方が標準的な HTTP キャッシュ制御メカニズムを使用して、`/ads.txt` ファイルのキャッシュに影響を与えることができます。具体的には、利用者とレプリケーターは、オリジンサーバーによって設定された HTTP Expires ヘッダーに注意するべきです（SHOULD）。

キャッシュ制御ディレクティブが存在しない場合、利用システムはデフォルトで 7 日間の有効期限を設定するべきです（SHOULD）。

# 4. EXAMPLES (例)

上記で定義したように、3 つの必須フィールドがあります。一部の例には、オプションの認証局 ID フィールドが含まれています。

## 4.1 SINGLE SYSTEM DIRECT (単一システム DIRECT)

この例は、ウェブサイト所有者によって直接管理/運用されている承認されたシステムが 1 つだけあるウェブサイトです。

`http://example.com/ads.txt`

```
greenadexchange.com, XF7342, DIRECT, 5jyxf8k54
```

## 4.2 SINGLE SYSTEM RESELLER (単一システム RESELLER)

この例は、インベントリの再販（リセール）を行う別会社によって運営されている承認されたシステムが 1 つだけあるウェブサイトです。その広告システムは認証局に登録されていないため、オプションの 4 番目のフィールドは省略されています。

`http://example.com/ads.txt`

```
redssp.com, 57013, RESELLER
```

## 4.3 MULTIPLE SYSTEMS AND RESELLERS (複数システムおよびリセラー)

この例は、複数の承認されたシステムと複数のリセラーを持つウェブサイトです。承認された広告システムの一部は認証局に登録されており、ID が発行されています。

`http://example.com/ads.txt`

```
# ads.txt file for example.com:
greenadexchange.com, 12345, DIRECT, d75815a79
silverssp.com, 9675, RESELLER, f496211
blueadexchange.com, XF436, DIRECT
orangeexchange.com, 45678, RESELLER
silverssp.com, ABE679, RESELLER
```

## 4.4 CONTACT RECORDS (コンタクトレコード)

この例は、複数の承認されたシステムと複数のコンタクトレコードを持つウェブサイトです。

`http://example.com/ads.txt`

```
# ads.txt file for example.com:
greenadexchange.com, 12345, DIRECT, d75815a79
blueadexchange.com, XF436, DIRECT
contact=adops@example.com
contact=http://example.com/contact-us
```

## 4.5 SUBDOMAIN REFERRAL (サブドメイン参照)

この例は、異なる承認されたシステムのセットを持つサブドメインをクローラーに参照させるウェブサイトです。クローラーはサブドメインをデータの取得先となる別の URL として扱い、親ドメインではなくサブドメインに関連付けるべきです（SHOULD）。

`http://example.com/ads.txt`

```
# ads.txt file for example.com:
greenadexchange.com, 12345, DIRECT, d75815a79
blueadexchange.com, XF436, DIRECT
subdomain=divisionone.example.com
```

`http://divisionone.example.com/ads.txt`

```
# ads.txt file for divisionone.example.com:
silverssp.com, 5569, DIRECT, f496211
orangeexchange.com, AB345, RESELLER
```

## 4.6 INVENTORYPARTNERDOMAIN REFERRAL (INVENTORYPARTNERDOMAIN 参照)

この例は、異なる承認されたシステムのセットを持つ「インベントリパートナー」をクローラーに参照させるアプリ（またはウェブサイト）です。クローラーは、`inventorypartnerdomain` をドメインとして受け取り、そのパートナーの ads.txt ファイルからデータを取得して、アプリ（またはウェブサイト）の承認されたセラーリストに関連付けるための ads.txt URL を構築するべきです（SHOULD）。

より詳細な実装情報とシナリオについては、実装ガイドを参照してください：[https://iabtechlab.com/wp-content/uploads/2021/03/ctv-app-ads-explainer-guide.pdf](https://iabtechlab.com/wp-content/uploads/2021/03/ctv-app-ads-explainer-guide.pdf) 注 - 2 番目の ads.txt ファイル内の `inventorypartnerdomain` エントリは処理しないべきです（SHOULD NOT）（ワンホップのみ追跡）。

`http://devsite.vMVPDB.com/app-ads.txt`

```
# app-ads.txt file for vMVPD B:
ssp.com, vwxyz, DIRECT
inventorypartnerdomain=programmerA.com
```

`http://programmerA.com/ads.txt`

```
# ads.txt file for Programmer A
ssp.com, abcde, DIRECT
```

従来の ads.txt/app-ads.txt モデルから `inventorypartnerdomain` ディレクティブへ移行する場合、ファイルの変更は以下のようになります：

BEFORE

vMVPDB は、Programmer A の ads.txt ファイル上のすべてのセラーアカウントをリストして、それらのアカウントにインベントリの販売を許可しなければなりません：

`http://devsite.vMVPDB.com/app-ads.txt`

```
# app-ads.txt file for vMVPD B:
ssp.com, vwxyz, DIRECT
ssp.com, abcde, DIRECT
ssp.com, fghij, RESELLER
ssp.com, klmno, RESELLER
ssp.com, pqrst, RESELLER
```

`http://programmerA.com/ads.txt`

```
# ads.txt file for Programmer A:
ssp.com, abcde, DIRECT
ssp.com, fghij, RESELLER
ssp.com, klmno, RESELLER
ssp.com, pqrst, RESELLER
```

AFTER

vMVPDB は Programmer A のドメインを指すだけで、Programmer A の ads.txt（app-ads.txt ではない）上のすべてのセラーアカウントがインベントリを販売することを承認できます：

`http://devsite.vMVPDB.com/app-ads.txt`

```
# app-ads.txt file for vMVPD B:
ssp.com, vwxyz, DIRECT
inventorypartnerdomain=programmerA.com
```

## 4.7 OWNERDOMAIN usage (OWNERDOMAIN の使用)

`OWNERDOMAIN` 変数は、sellers.json ファイル内の `sellers.domain` を、ads.txt ファイルが見つかったドメインに接続するために使用されます。`OWNERDOMAIN` が ads.txt ファイルがホストされているドメインと異ならない場合でも、明確にするためにこの値をすべての ads.txt ファイルに含めることが推奨されます。

この変数が存在しない場合、`OWNERDOMAIN` は収益化されているドメインおよび ads.txt ファイルが見つかった場所と同じであると見なされるべきです（SHOULD）。

より詳細な実装情報とシナリオについては、実装ガイドを参照してください：[https://iabtechlab.com/wp-content/uploads/2022/04/Ads.txt-1.1-Implementation-Guide.pdf](https://iabtechlab.com/wp-content/uploads/2022/04/Ads.txt-1.1-Implementation-Guide.pdf)

この例では、"`MediaCompany.com`" は "`example.com`" のビジネスオーナーです。したがって、`example.com/ads.txt` ファイルにはビジネスオーナーを指定するエントリが含まれています。

`http://example.com/ads.txt`

```
OWNERDOMAIN=mediacompany.com

greenadexchange.com, XF7342, DIRECT, 5jyxf8k54
```

## 4.8 MANAGERDOMAIN usage (MANAGERDOMAIN の使用)

`MANAGERDOMAIN` 変数は、パブリッシャーと主要または独占的な収益化パートナーとの関係を表すために使用されるべきです（SHOULD）。これらの場合、`MANAGERDOMAIN` はパブリッシャーのインベントリを購入するための最も直接的なパスであるべきです（SHOULD）。

より詳細な実装情報とシナリオについては、実装ガイドを参照してください：[https://iabtechlab.com/wp-content/uploads/2022/04/Ads.txt-1.1-Implementation-Guide.pdf](https://iabtechlab.com/wp-content/uploads/2022/04/Ads.txt-1.1-Implementation-Guide.pdf)

`http://example.com/ads.txt`

```
OWNERDOMAIN=mediacompany.com
MANAGERDOMAIN=yellowmediamanager.com, FR
MANAGERDOMAIN=bluemediamanager.com, US

greenadexchange.com, XF7342, DIRECT, 5jyxf8k54
```

## 4.9 FILE WITHOUT AUTHORIZED ADVERTISING SYSTEMS (承認された広告システムのないファイル)

この例は、承認された広告システムを公開していないウェブサイトであり、正しくフォーマットされた ads.txt ファイル内でこの意図を反映しています。

`http://example.com/ads.txt`

```
placeholder.example.com, placeholder, DIRECT, placeholder
```

# 5. IMPLEMENTER’S NOTES (実装者向けノート)

## 5.1 VERSION (バージョン)

これは仕様のバージョン 1.1 であり、将来のバージョンについては、可能な限り下位互換性を持たせるようにあらゆる試みが行われます。

## 5.2 GUIDANCE BY PARTY (当事者別のガイダンス)

### 5.2.1 SSP/EXCHANGE (SSP/エクスチェンジ)

SSP およびエクスチェンジは、Field #1 で使用する正規ドメインを決定するべきです（SHOULD）。パブリッシャーおよび DSP 向けにドキュメントを公開するべきです（SHOULD）。パブリッシャー向けのドキュメントには、パブリッシャーが Field #2 の適切な ID を取得する方法を示すべきです（SHOULD）。DSP 向けのドキュメントには、DSP が ads.txt ファイルと照合するためにビッドリクエストのどのフィールドを使用すべきかを示すべきです（SHOULD）。

OpenRTB ビッドリクエストを作成するシステムは、セラーのアカウント ID を `Publisher.ID` フィールドに配置することが推奨されます。また、`Site.Domain` フィールドには、アカウント ID が公に投稿されている ads.txt ファイルをホストするドメインが入力されていることを確認してください。

理想的には、実装する SSP/エクスチェンジは、パブリッシャーが ads.txt ファイルに配置するための正確な行を生成するツールを提供するべきです（SHOULD）。SSP/エクスチェンジはまた、パブリッシャーのドメインをクロールし、ads.txt ファイルの欠如やファイル内の適切な宣言の欠如をパブリッシャーに通知する（例：パブリッシャーダッシュボードでの警告、電子メールなど）ことも検討するべきです（SHOULD）。

### 5.2.2 DSP (DSP)

DSP は、エクスチェンジが使用する正規ドメイン（Field #1）および ads.txt と照合すべきビッドリクエスト内の適切なフィールド（Field #2）について、SSP/エクスチェンジが提供するドキュメントを参照するべきです（SHOULD）。

### 5.2.3 PUBLISHERS (パブリッシャー)

パブリッシャーは、エクスチェンジが使用する正規ドメイン（Field #1）および Field #2 に配置すべき適切な ID について、SSP/エクスチェンジが提供するドキュメントを参照するべきです（SHOULD）。

## 5.3 INTEROPERABILITY (相互運用性)

実装者は、`/ads.txt` ファイルの解析における堅牢性に特に注意を払うべきです（SHOULD）。`/ads.txt` ファイルは自動化されたシステムまたは手動のプラットフォーム固有のテキストエディタで作成されることが予想されるため、データの利用者は、異なる改行規則（特に CRLF に加えて CR および LF）、およびさまざまな空白やフィールド区切り文字を持つファイルを受け入れる際に寛容であるべきです（SHOULD）。

## 5.4 SECURITY (セキュリティ)

`/ads.txt` 宣言は別の、おそらく認証されていない HTTP トランザクションで取得および適用されるため、あるサーバーが別のサーバーになりすましたり、`/ads.txt` へのリクエストを傍受して、利用システムに偽情報を提供する可能性があります。

これが懸念される場合、ウェブサイト所有者は `/ads.txt` ファイルに対する安全でない http リクエストを https リクエストにリダイレクトするべきです（SHOULD）。

## 5.5 SUBDOMAIN DIRECTIVES (サブドメインのディレクティブ)

クローラーを作成する場合、実装者は広告の重要なリクエストを発生させているルートドメインから `/ads.txt` をリクエストするべきです（SHOULD）。パブリッシャーは常にルートドメインに `/ads.txt` ファイルを投稿するべきです（SHOULD）。クローラーは、クローラーの URL リストを作成する際にサブドメインを取り除くべきです（SHOULD）。サブドメインの除去を実装する際には Public Suffix List [12][16] を利用するべきです（SHOULD）。

特定のサブドメインが異なる承認された広告システムを持つ場合、パブリッシャーはそのサブドメインにのみ ads.txt ファイルを投稿し、`subdomain=` 変数を使用してルートドメイン上の ads.txt でそれらのサブドメインをそれぞれ明示的に宣言するべきです（SHOULD）。クローラーは、ルートドメイン上の ads.txt で `subdomain=` 変数を使用してリストされているサブドメイン上の ads.txt ファイルのみをクロールするべきです（SHOULD）。

ルートドメイン上の ads.txt がサブドメインを宣言し、そのサブドメインに ads.txt が存在する場合、そのサブドメイン上の ads.txt にリストされている広告システムのみが、そのサブドメイン上のインベントリを販売することを承認されます。ルートドメイン上の ads.txt がサブドメインを宣言していない、またはサブドメインに ads.txt が存在しない場合、ルートドメインの ads.txt にリストされている広告システムのみが、そのサブドメイン上のインベントリを販売することを承認されます。

## 5.6 ADS.TXT CRAWLERS (ads.txt クローラー)

ads.txt データクローラーのリファレンス実装は github [15] にあります。

ads.txt 以外のパブリッシャーコンテンツをクロールし、パブリッシャーコンテンツ、広告、および関連するメタデータを読み取って表示したいクローラーは、robots.txt の指示によって禁止されていない場合、そうすることができます。

ads.txt ファイル仕様内の仕様バージョン番号または最終更新日の宣言は、指定された変数ではありません。実装者がコメントを使用してこれらの変数を含めることは歓迎されますが、ワーキンググループはこれらを仕様の公式変数にしたいとは考えていません。なぜなら、クローラーがこの情報を取得するためのより信頼性の高い方法があるためです。

最終更新日は、ads.txt ファイルがどれくらい最近更新されたかを判断するためにクローラーによって使用されます。この判断を行うには、以下の 2 つのデータポイントを使用することをお勧めします。

1. Last-Modified レスポンス HTTP ヘッダー
2. 最後の既知のファイルの内容と新しいファイルの内容のチェックサム比較により、ファイルが同じかどうかを判断する

上記の 2 つの方法を使用することで、クローラーはパブリッシャーに `lastupdateddate` のような別の変数を維持するよう要求することなく、ファイルの内容が変更されたかどうかを判断できるはずです。

仕様バージョンは、パブリッシャーが使用している ads.txt 仕様のバージョンを判断するためにクローラーによって使用されます。2017 年に ads.txt が作成されて以来、仕様に対する破壊的な変更はありません。各バージョンの拡張機能は、`CONTACT`、`SUBDOMAIN`、`INVENTORYPARTNERDOMAIN`、そして現在の `MANAGERDOMAIN` や `OWNERDOMAIN` などの新しい変数を含めることでした。パブリッシャーが使用している ads.txt のバージョンに基づいてクローラーが行う決定はありません。

代わりに、クローラーはファイル内でどの変数がサポートされているかに焦点を当て、新しい変数をすべてサポートしていることを確認するべきです（SHOULD）。

## 5.7 INVENTORYPARTNERDOMAIN DIRECTIVES (INVENTORYPARTNERDOMAIN ディレクティブ)

多くの場合、特にモバイルおよび CTV ビデオストリーミングアプリ（別名 OTT アプリ）では、他社からコンテンツをライセンス供与してキュレーションし、複数の配信アプリへのコンテンツの配信/再送信を許可することが一般的です。

これらの関係は `INVENTORYPARTNERDOMAIN` ディレクティブを通じて列挙されます。詳細については、「ads.txt for CTV explainer doc」（[https://iabtechlab.com/ads-txt](https://iabtechlab.com/ads-txt) でも入手可能）を参照してください。

クローラーは、発信元の app/ads.txt から 1 ホップ先のエントリを取得するべきです（SHOULD）（パートナーの ads.txt ファイル内の `inventorypartnerdomain` エントリは利用しないべきです（SHOULD NOT））。

このディレクティブは、ドメインがビッドレベルの承認のために OpenRTB 仕様を使用してビッドリクエストで渡される場合にのみ適用されます：

- `app.inventorypartnerdomain` または
- `site.inventorypartnerdomain`

## 5.8 OWNERDOMAIN DIRECTIVE (OWNERDOMAIN ディレクティブ)

多くのパブリッシャーやアプリ開発者は、複数のドメイン（サイト）やアプリを所有し、収益化しています。ドメイン/アプリの所有者を明確にするためです。例：

`ExamplePublisher.com` は `example1.com` と `example2.com` を所有しています。

より詳細な実装情報とシナリオについては、実装ガイドを参照してください：[https://iabtechlab.com/wp-content/uploads/2022/04/Ads.txt-1.1-Implementation-Guide.pdf](https://iabtechlab.com/wp-content/uploads/2022/04/Ads.txt-1.1-Implementation-Guide.pdf)

## 5.9 MANAGERDOMAIN DIRECTIVE (MANAGERDOMAIN ディレクティブ)

エコシステム内のさまざまな関係を明確にするために、仕様が更新され、パブリッシャーがドメイン/アプリを所有するビジネスエンティティを指定し、収益化を他社に委託している場合のマネージャー（例：セールスハウス）を宣言できるようになりました。

より詳細な実装情報とシナリオについては、実装ガイドを参照してください：[https://iabtechlab.com/wp-content/uploads/2022/04/Ads.txt-1.1-Implementation-Guide.pdf](https://iabtechlab.com/wp-content/uploads/2022/04/Ads.txt-1.1-Implementation-Guide.pdf)

# 6. SCOPE AND FUTURE DIRECTIONS (範囲と今後の方向性)

## 6.1 SCOPE (範囲)

この標準の初版の範囲は、偽造インベントリに関連するいくつかの不正シナリオに対処する目的で、ドメイン所有者の観点からウェブコンテンツの承認されたセラーを定義するメカニズムを定義することです。

## 6.2 OPEN ISSUES (未解決の課題)

仕様の将来のバージョンでの解決に向けて検討すべき未解決の課題は、`support@iabtechlab.com` への連絡を通じて注意喚起するべきです（SHOULD）。

## 6.3 FUTURE DIRECTIONS (今後の方向性)

今後の方向性としては、許可される広告フォーマットのカバー、シンジケーション、および第三者への権限委任などが含まれます。

# 7. ACKNOWLEDGEMENTS (謝辞)

著者は、ロボット排除標準 [5][6] のオリジナルの著者に感謝します。また、初期ドラフトへのコメントやイニシアチブのサポートに対して、IAB Tech Lab、TAG、および多数の企業内の多くの人々に感謝します。

# 8. REFERENCES (参考文献)

- [1] https://techcrunch.com/2016/01/06/the-8-2-billion-adtech-fraud-problem-that-everyone-is-ignoring/
- [2] http://adage.com/article/digital/ana-report-7-2-billion-lost-ad-fraud-2015/302201/
- [3] http://boingboing.net/2016/12/21/methbot-a-3m-5mday-video-a.html
- [4] https://www.emarketer.com/Article/Ad-Industrys-Focus-on-Fraud-Has-Intensified/1014430
- [5] http://www.robotstxt.org/norobots-rfc.txt
- [6] https://en.wikipedia.org/wiki/Robots_exclusion_standard
- [7] https://www.iab.com/guidelines/real-time-bidding-rtb-project/
- [8] https://developers.google.com/ad-exchange/rtb/downloads
- [9] https://www.iab.com/guidelines/iab-opendirect-specification/
- [10] https://tools.ietf.org/html/rfc1123
- [11] https://www.tagtoday.net/
- [12] https://publicsuffix.org/
- [13] https://www.w3schools.com/tags/ref_urlencode.asp
- [14] http://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-5-FINAL.pdf
- [15] https://github.com/InteractiveAdvertisingBureau/adstxtcrawler
- [16] https://publicsuffix.org/list/public_suffix_list.dat
- [17] ads.txt explainer doc.
- [18] https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2
