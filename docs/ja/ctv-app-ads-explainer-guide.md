---
title: "ctv app-ads explainer guide"
description: "CTV/OTT環境における複数事業者間の広告在庫共有を、ads.txt／app-ads.txtの拡張（inventorypartnerdomain）で正しく検証・運用するためのガイドです。"
---
Released March 2021

フィードバックや質問は openRTB@iabtechlab.com または support@iabtechlab.com までメールでお送りください。このドキュメントは [https://iabtechlab.com/ads-txt/](https://iabtechlab.com/ads-txt/) でオンライン利用可能です。

# このドキュメントについて

| 項目 | 内容 |
|------|------|
| 翻訳 | Advertisers and Publishers Transparency Initiative (APTI) |
| 原著者 | IAB Technology Laboratory (IAB Tech Lab) |
| 原文 | [ads.txt & app-ads.txt: Guidance for Inventory Sharing](https://iabtechlab.com/wp-content/uploads/2021/03/ctv-app-ads-explainer-guide.pdf) |
| ライセンス | 原文に明示なし |

※この翻訳は、IAB Tech Lab による公式なものではありません。翻訳の正確性については翻訳者が責任を負います。

# Background（背景）

コネクテッド TV（CTV）市場では、複雑な収益化関係が頻繁に発生するため、現在設計されている ads.txt および app-ads.txt は、広範な採用には不十分です。（*これらの関係は CTV 環境や OTT コンテンツ配信に固有のものではありませんが、CTV/OTT コンテキストでの発生頻度がはるかに高いため、この問題の解決が特に必要になっています。*）これらのガイドラインと仕様の拡張は、複数のエンティティが広告枠に対する所有権を持つ可能性があるサイトやアプリをよりシームレスにサポートすることを目的としています。これは一般に**「インベントリ共有（Inventory Sharing）」**と呼ばれます。OTT では、これらの状況は、コンテンツ配信（MVPD や vMVPD）などの関係や、さまざまな配信契約（TV Everywhere）の結果として発生することがよくあります。最終的に、ほぼすべての関係は、「アプリ/サイトの所有者以外のビジネスエンティティが、アプリ/サイト内の広告枠の一部に対する所有権と、そのインベントリを販売する権利を持っている」というケースに単純化できます。

そのような状況の簡単な例として、vMVPD アプリなどのコンテンツ配信業者があります。これらのコンテンツ配信契約では、あるエンティティ（コンテンツプロデューサー/プログラマー A）が、コンテンツ配信業者 B にコンテンツを再放送する権利を与えます。契約の一環として、A と B の両方が、ストリーミングされたコンテンツに配信される広告インベントリの一部の所有権を持ちます（インベントリは「共有」されます）。「所有権」という言葉を使用することで、アプリ内で A と B の両方が正当に広告リクエストを発信し、それがプログラマティックエコシステムに伝播される可能性があることを意味しています。

現在の ads.txt および app-ads.txt 標準では、この関係を宣言するには、vMVPD アプリが app-ads.txt ファイルでプログラマー A を承認し、さらにプログラマーの承認されたセラーとリセラーの情報も含める必要があります。これは、app-ads.txt ファイルの生成と維持のコストを増加させ、承認されたセラーの数が増えるにつれて、標準のセキュリティ上の利点を徐々に低下させます。

私たちが CTV/OTT 向けの「Ads.txt & App-ads.txt for Inventory Sharing」ガイドラインを通じて定義し検証しようとしているのは、まさにこれらのシナリオです。

## Scope（範囲）

### In Scope（対象範囲内）

**ビジネス関係:** このソリューションは、**インベントリ共有**関係をカバーします。ここでは、異なるエンティティ（アプリ/サイトの所有者、コンテンツ所有者）が、特定のアプリ/サイト上のコンテンツ内の広告枠を販売する権利を持つ場合があります。

**潜在的な悪用ベクトル:** このソリューションは、アプリ/サイト上のインベントリに対するパブリッシャーの所有権（および販売権）の基本的な不当表示に対処することを目的としており、次の質問に答えます。

*「パブリッシャー A は、アプリ/サイト B 上の一部のインベントリに対する所有権（および販売権）を持っていますか？」*

### Out of Scope（対象範囲外）

**ビジネス関係:** このソリューションは、**レベニューシェア（収益分配）**シナリオをカバーしません。このシナリオでは、あるエンティティがコンテンツ所有者（例：YouTube、DailyMotion）によって提供されたコンテンツに関連付けられた広告インベントリを所有および販売します。所有エンティティは、広告販売から生じた収益をコンテンツ所有者と共有する場合がありますが、最終的には広告インベントリを所有/販売しているエンティティは 1 つだけです。

**潜在的な悪用ベクトル:** このソリューションは、特定のコンテンツ/番組内の排他性やインベントリ所有権など、コンテンツ権の所有権やメディア権管理の追加の側面には対処しません。次の質問に答えようとはしていません。

*「パブリッシャー A は、この特定のテレビ番組またはプログラミング内のインベントリを販売する権利を持っていますか？」または*

*「アプリ/サイト C は、特定のテレビ番組またはプログラミングを配信/ストリーミングする独占的権利を持っていますか？」*

これらの概念は、特にコネクテッド TV や OTT ストリーミングの分野でますます重要になっていますが、開発中の新しいソリューションが必要になります。

# Updates to Ads.txt & App-Ads.txt Standard（Ads.txt および App-Ads.txt 標準の更新）

ads.txt および app-ads.txt の以前のバージョンでは、これらのシナリオをサポートするには、アプリ/サイトの所有者/開発者が、インベントリ所有権の何らかのシェアを交渉したすべてのパートナー（およびそのリセラー）のパブリッシャー ID を使用して ads.txt/app-ads.txt ファイルを維持する必要がありました。これにより、多くの ads.txt/app-ads.txt ファイルを維持することが法外に困難になりました。この方法に移行することは、パブリッシャーがパートナーの ads.txt/app-ads.txt ファイル内のすべてのエントリを自社のインベントリを販売する権限があると認め、そのファイルの変更（知識の有無にかかわらず）のリスクを負うことを意味することに注意してください。

代わりに、ads.txt および app-ads.txt の仕様が更新され、（アプリ/サイト開発者のものとは別の）ビッドリクエストのパブリッシャー ID を検証できる別のドメインを指定する機能が含まれるようになりました。これらのドメインは、OpenRTB 仕様の site および app オブジェクトを通じて渡されます。

- *app.inventorypartnerdomain または*
- *site.inventorypartnerdomain*

これらのドメインを検証するために、[(app)ads.txt spec](https://iabtechlab.com/ads-txt/) には、ads.txt および app-ads.txt ファイル（ads.txt で定義）に次の追加宣言が含まれており、アプリ/サイトの所有者が入力することを目的としています。

| VARIABLE | VALUE | DESCRIPTION |
|---|---|---|
| inventorypartnerdomain | サイト/アプリ上の広告インベントリの一部に対する所有権を持つ（サイト/アプリ所有者の）パートナーのドメインへのポインタ。パートナーの ads.txt または app-ads.txt ファイルはここでホストされます。 | サイトまたはアプリに別のパートナーが所有する広告インベントリが含まれている場合、アプリまたはサイトは、このディレクティブを使用してそれらのパートナーのすべてのドメインをリストするべきです。 |

app-ads.txt の新しいバージョンでインベントリを検証するためにこれらの値がどのように連携するかについては、このドキュメントの後半にある[ユースケースの例（Example Use Cases）](#example-use-cases)を参照してください。

# Example Use Cases（ユースケースの例）

#### 定義:

- **Programmer A（プログラマー A）:** コンテンツ所有者またはコンテンツ開発者 - 例：ESPN、CBS、NBC、Crackle、Tastemade、Sky (UK)、TF1 (FR)、RTL (DE and NL)、SBS (AU)、Channel 9 (AU)、Nippon TV (JP) など。
- **(v)MVPD:** (virtual) Multichannel Video Programming Distributor / コンテンツ配信業者（収益化パートナー、ユーザー向けコンテンツの所有権を常に持っているとは限らない） - Sling TV、Pluto TV、YouTube TV、The Roku Channel、Fubo、Comcast、Sky (UK)、Virgin Media (UK)、Orange Télécom (FR) および Bouygues Télécom (FR)、Foxtel (AU)

## CASE A: Programmer Owned App（プログラマー所有アプリ）

**ビジネスシナリオ:** すべてのインベントリは、プログラマー A が所有するアプリで、選択した SSP を介してプログラマー A によって生成および販売されています。これは OTT インベントリの最も直接的な例であり、現在の app-ads.txt 承認モデルと変わりません。

**App:** Programmer A App (app bundle ID: 12345)

**Developer URL domain for the app:** devsite.programmerA.com

**Seller/Publisher:** Programmer A (publisher ID: abcde)

**Content Producer**: Programmer A

#### OpenRTB Declaration:

```json
{
  "app": {
    "bundle": "12345",
    "storeurl": "https://ctvappstore.com/details/12345/programmerA",
    "publisher": {
      "id": "abcde"
    }
  }
}
```

**Programmer A app-ads.txt file** (devsite.programmerA.com/app-ads.txt)**:**

```
ssp.com, abcde, DIRECT, *
```

*\*注: 「Certification Authority ID」フィールドも ads.txt および app-ads.txt ファイルに含まれる場合がありますが、これらの例ではオプションであるため省略されています。*

## CASE B: Content Channel on vMVPD app（vMVPD アプリ上のコンテンツチャンネル）

このケースでは、vMVPD アプリ内に表示されるライセンスコンテンツに対して実行される広告の承認が、ビッドリクエストおよび app-ads.txt & ads.txt ファイルに表示される可能性がある 2 つの異なる方法を示します。これらは、ビジネスシナリオ B.1 および B.2 として提示されます。

### Business Scenario B.1

vMVPD B は広告枠を販売する権利を持っており、広告は vMVPD B アプリ内のプログラマー A のコンテンツに配信されます。コンテンツの所有権に関する情報（つまり、コンテンツはプログラマー A が所有していること）は「ブラインド（blinded）」化されており、ビッドリクエストでは宣言されません。これはケース A（特定のコンテンツ宣言なしでアプリ上のインベントリを販売するアプリ所有者）と同様であり、現在の app-ads.txt 承認モデルと変わりません。

**App:** vMVPD B App (app bundle ID: 67890)

**Developer URL domain for the app:** devsite.vMVPDB.com

**Seller/Publisher:** vMVPD B (publisher ID: vwxyz)

**Content Producer:** Programmer A

#### OpenRTB Declaration: (by vMVPD B)

```json
{
  "app": {
    "bundle": "67890",
    "storeurl": "https://ctvappstore.com/details/67890/vmvpdB",
    "publisher": {
      "id": "vwxyz"
    }
  }
}
```

**vMVPD B app-ads.txt file** (devsite.vMVPDB.com/app-ads.txt)**:**

```
ssp.com, vwxyz, DIRECT
```

### Business Scenario B.2

プログラマー A は広告枠を販売する権利を持っており、広告は vMVPD B アプリ内のプログラマー A のコンテンツに配信されます。

**App:** vMVPD B App (app bundle ID: 67890)

**Developer URL domain for the app:** devsite.vMVPDB.com **Seller/Publisher:** Programmer A (publisher ID: abcde) **Content Producer:** Programmer A

#### OpenRTB Declaration: (by Programmer A)

```json
{
  "app": {
    "bundle": "67890",
    "storeurl": "https://ctvappstore.com/details/67890/vmvpdB",
    "inventorypartnerdomain": "programmerA.com",
    "publisher": {
      "id": "abcde"
    }
  }
}
```

**vMVPD B app-ads.txt file** (devsite.vMVPDB.com/app-ads.txt)**:**

```
ssp.com, vwxyz, DIRECT inventorypartnerdomain=programmerA.com
```

**Programmer A ads.txt file** (programmerA.com/ads.txt)**:**

```
ssp.com, abcde, DIRECT
```

## CASE C: Programmer Owned App using MVPD sign-in (TV Everywhere)（MVPD サインインを使用するプログラマー所有アプリ）

**App:** Programmer A App (app bundle ID: 12345)

**Developer URL domain for the app:** devsite.programmerA.com

**Seller/Publisher:** vMVPD B (publisher ID: vwxyz)

**Content Producer:** Programmer A

**ビジネスシナリオ:** ユーザーが vMVPD B のログイン認証情報を使用してプログラマー A のアプリにログインするため、vMVPD B はプログラマー A のアプリ内の広告枠を販売する権利を持っています。これはケース B: ビジネスシナリオ 2 の逆であることに注意してください。

```json
{
  "app": {
    "bundle": "12345",
    "storeurl": "https://ctvappstore.com/details/12345/programmerA",
    "inventorypartnerdomain": "vmvpdB.com",
    "publisher": {
      "id": "vwxyz"
    }
  }
}
```

**Programmer A app-ads.txt file** (devsite.programmerA.com/app-ads.txt)**:**

```
ssp.com, abcde, DIRECT
inventorypartnerdomain=vmvpdB.com
```

**vMVPD B ads.txt file** (vMVPDB.com/ads.txt)**:**

```
ssp.com, vwxyz, DIRECT
```

# Use Case Implementation Logic（ユースケースの実装ロジック）

| **Scenario** | **Do this..** | **Possible outcomes** |
|---|---|---|
| ビッドリクエストが app* であり、`$.app.inventorypartnerdomain` がない場合（ビジネスユース[ケース A](#case-a-programmer-owned-app-using-direct-publisher-sign-in)、[ケース B.1](#case-b-content-channel-on-vmvpd-app) に対応） | `$.app.bundle` のアプリストアレコードから取得した開発者ドメインで **app-ads.txt** の検索を試みる | *有効な app-ads.txt レコードが見つからない（ストアレコードが見つからない、ストアレコードにドメインがない、ドメインに app-ads.txt ファイルがない、Web サーバーがエラーを返すなど）* -> **参加していないインベントリ** *有効な app-ads.txt ファイルが見つかり、ビッドリクエストのパブリッシャー ID + 広告システムがファイルに見つからない* -> **承認されていないインベントリ** *有効な app-ads.txt ファイルが見つかり、ビッドリクエストのパブリッシャー ID + 広告システムがファイルに見つかる* -> **承認されたインベントリ** |
| ビッドリクエストが app* であり、`$.app.inventorypartnerdomain` がある場合（ビジネスユース[ケース B.2](#case-b-content-channel-on-vmvpd-app)、[ケース C](#case-c-programmer-owned-app-using-mvpd-sign-in-tv-everywhere) に対応） | `$.app.bundle` のアプリストアレコードから取得した開発者ドメインで **app-ads.txt** の検索を試みる **ビッドリクエスト**の `$.app.inventorypartnerdomain` フィールドのドメインで **ads.txt** の検索を試みる | *有効な app-ads.txt レコードが見つからない（ストアレコードが見つからない、ストアレコードにドメインがない、ドメインに app-ads.txt ファイルがない、Web サーバーがエラーを返すなど）* -> **結論が出ない: 承認を決定できない** |
| | | **IF:** *有効な app-ads.txt ファイルが見つかり、ビッドリクエストのパブリッシャー ID + 広告システムが app-ads.txt ファイルに見つかる* -> **承認されたインベントリ** **ELSE:** *有効な app-ads.txt ファイルが見つかり &* ***app-ads.txt ファイル*** *に、***ビッドリクエスト***からの* `$.app.inventorypartnerdomain` *のドメインと一致する inventorypartnerdomain ディレクティブが含まれていない* -> **承認されていないインベントリ** ***App-ads.txt ファイル*** *に、***ビッドリクエスト***からの* `$.app.inventorypartnerdomain` *のドメインと一致する inventorypartnerdomain ディレクティブが含まれているが、inventorypartnerdomain の ads.txt ファイルに有効な ads.txt レコードが見つからない（ドメインに ads.txt ファイルがない、Web サーバーがエラーを返すなど）* -> **結論が出ない: 承認を決定できない** ***App-ads.txt ファイル*** *に、***ビッドリクエスト***からの* `$.app.inventorypartnerdomain` *のドメインと一致する inventorypartnerdomain ディレクティブが含まれているが、ビッドリクエストのパブリッシャー ID + 広告システムが inventorypartnerdomain の ads.txt ファイルに見つからない* -> **承認されていないインベントリ** ***App-ads.txt ファイル*** *に、***ビッドリクエスト***からの* `$.app.inventorypartnerdomain` *のドメインと一致する inventorypartnerdomain ディレクティブが含まれており、ビッドリクエストのパブリッシャー ID + 広告システムが inventorypartnerdomain の ads.txt ファイルに見つかる* -> **承認されたインベントリ** |

**_\*注:_** *ビッドリクエストがアプリではなくサイトの場合、同じロジックが適用されますが、`$.site.inventorypartnerdomain` を探してください。*

# Implementation Guidelines for CTV/OTT（CTV/OTT の実装ガイドライン）

## CTV App Store Guidance（CTV アプリストアガイダンス）

#### Required（必須）:

1. app-ads.txt 情報がアドテクプラットフォーム全体で検証可能であることを確認するには、アプリストアの Web サイトを Web 上で公開することが重要です。
2. CTV アプリストアは、ストアで割り当てられた ID がストアから公開アクセス可能であることを確認することにより、[OTT/CTV Store Assigned App Identification Guidelines](https://iabtechlab.com/wp-content/uploads/2020/08/IAB-Tech-Lab-OTT-store-assigned-App-Identification-Guidelines-2020.pdf)（OTT/CTV ストア割り当てアプリ識別ガイドライン）をサポートしなければなりません（REQUIRED）。
3. CTV アプリストアは、[app-ads.txt standard](https://iabtechlab.com/wp-content/uploads/2019/03/app-ads.txt-v1.0-final-.pdf)（app-ads.txt 標準）に従い、HTML ページにメタタグを追加して、開発者の Web サイト URL、バンドル ID、ストア ID を公開しなければなりません（REQUIRED）。IAB Tech Lab の [demystifying app-ads.txt](https://iabtechlab.com/blog/demystifying-app-ads-txt/) ガイダンスでも、パブリッシャーの Web サイト URL、バンドル ID、ストア ID を公開する他の方法を定義しています。

## Publisher Guidance（パブリッシャーガイダンス）

#### Required（必須）:

1. パブリッシャーが CTV インベントリに app-ads.txt を採用する前に、[OTT/CTV Store Assigned App Identification Guidelines](https://iabtechlab.com/wp-content/uploads/2020/08/IAB-Tech-Lab-OTT-store-assigned-App-Identification-Guidelines-2020.pdf)（OTT/CTV ストア割り当てアプリ識別ガイドライン）を採用する必要があります。これらのガイドラインに従い、パブリッシャーは以下を行う必要があります（REQUIRED）。
   1. OpenRTB 2.5 の `app.bundle` フィールドまたは OpenRTB 3.0/AdCOM 1.0 の `app.storeid` フィールドで CTV アプリストア割り当て ID を渡す。
   2. OpenRTB 2.5 および OpenRTB 3.0/AdCOM 1.0 の `app.storeurl` フィールドで発信元アプリのストア URL を渡す。
2. **アプリ所有者**は、[app-ads.txt standard](https://iabtechlab.com/wp-content/uploads/2019/03/app-ads.txt-v1.0-final-.pdf)（app-ads.txt 標準）に従い、開発者の Web サイトで app-ads.txt ファイルを公開するべきです（SHOULD）。パブリッシャーがすでにモバイルアプリインベントリ用に app-ads.txt を公開しており、CTV アプリ用に異なる承認済みセラー ID がある場合、CTV アプリインベントリ専用の新しいドメインで CTV 固有の app-ads.txt ファイルを公開するべきです（SHOULD）。
3. さらに、**アプリ所有者**は、app-ads.txt ファイル内で、*inventorypartnerdomain* ディレクティブを使用して、**アプリ所有者**のアプリ内のインベントリを所有する**インベントリパートナー**のドメインを宣言するべきです（SHOULD）。これは、**インベントリパートナー**が ads.txt または app-ads.txt ファイルをホストするドメインであるべきです。

*\*注: アプリ所有者が inventorypartnerdomain ディレクティブを活用するのではなく、app-ads.txt ファイル内にインベントリパートナーのセラーおよびリセラー ID を直接リストすることを希望する場合、これもサポートされます。*

#### Guidance for app publishers passing additional information in bundle fields（バンドルフィールドで追加情報を渡すアプリパブリッシャー向けのガイダンス）

多くの CTV アプリパブリッシャーが、この移行の一環として「失われる」可能性のある追加情報をバンドル ID で渡していることが確認されています。以下は、この情報がより適切に渡される場所に関するガイダンスです。

1. **アプリ内のチャンネルまたはネットワーク:** `content.producer.name`
2. **VOD 対 ライブストリーム:** `content.livestream` で渡す
3. **デバイスのメーカー/モデル:** `device.make` & `device.model` で渡す
4. **アプリストア:** `app.storeurl` で渡す - *（注：これは app-ads.txt 標準ですでに必須です）*

参照: [OTT/CTV User Agent Guidelines](https://iabtechlab.com/wp-content/uploads/2019/12/OTT_CTV_User_Agent_Preliminary_Guidelines_IABTechLab_2019-12.pdf)

## SSP/Exchange Guidance（SSP/エクスチェンジガイダンス）

#### Required（必須）:

1. SSP/エクスチェンジは、インベントリパートナーが存在する場合に、パートナーの ads.txt ファイルへのポインタのためのインベントリパートナーのドメイン渡しをサポートするために、サイトおよびアプリオブジェクトの *app.inventorypartnerdomain* & *site.inventorypartnerdomain* フィールドを実装しなければなりません（REQUIRED）。
2. SSP/エクスチェンジは、[OTT/CTV Store Assigned App Identification Guidelines](https://iabtechlab.com/wp-content/uploads/2019/12/OTT_Store_Assigned_App_Identification_Guidelines_IABTechLab_2019-12.pdf)\* に従って CTV アプリ ID を提供するパブリッシャーをサポートするべきであり（SHOULD）、適切な既存または拡張 OpenRTB フィールドを介して（[Publisher Guidance](#publisher-guidance) セクションに記載されているように）追加のコンテキストおよび環境シグナルを渡すのを支援するべきです（SHOULD）。

*\*ガイドラインに従わないと、DSP が app-ads.txt 情報を検証できなくなります。*

## DSP Guidance（DSP ガイダンス）

#### Required（必須）:

1. DSP は、CTV アプリストアからの標準化されたガイダンスに従って（またはそれらのガイドラインに準拠したサービスを使用して）、app-ads.txt クローラーを実装するべきです（SHOULD）。
