---
title: "supply chain object"
description: "OpenRTB SupplyChain object specification"
---
# OpenRTB SupplyChain object


## Abstract（概要）

オープンなデジタル広告エコシステムにおける無効なトラフィック、アドフラウド、偽造インベントリから利益を得る能力を排除するための広範な取り組みの一環として、SupplyChain オブジェクトは、バイヤーが特定のビッドリクエストを販売または再販しているすべての当事者を確認できるようにします。この拡張オブジェクトは OpenRTB 2.5 で使用できます。OpenRTB 2.6 および 3.0 では、source オブジェクトに正式に追加されました。


## Introduction（はじめに）

ads.txt は、パブリッシャーやアプリ制作者がプログラマティックマーケットプレイスを通じて特定のインプレッションセットを販売する権限を持つ者を定義することにおいて、非常に成功しています。しかし、ads.txt はそれらのインプレッションの取引に関与するすべての当事者を明らかにしたり、認可したりする試みは行っていません。この情報は、サプライチェーンの透明性、すべての仲介者がバイヤーが取引したいエンティティであることの確認、インベントリが可能な限り直接的に購入されることの確認など、さまざまな理由からバイヤーにとって重要です。実装はバイヤーに対して可能な限り透明であるべきです。バイヤーがどのインベントリの販売にも誰が参加しているかを容易に理解できるようにするべきです。


## Implementation（実装）

SupplyChain オブジェクトは、主にノードのセットで構成されており、各ノードはインベントリの取引に参加する特定のエンティティを表します。最初から最後までのノードのチェーン全体が、インベントリに対する直接的な支払いフローに関与するすべてのエンティティを表します。将来のバージョンの仕様には、取引には関与しているが支払いには関与していないエンティティも含まれる可能性があります。


## ノードの定義

ノードには 2 つの必須プロパティが含まれます。広告システム識別子（asi）とセラー ID（sid）です。広告システム識別子は、広告システムのドメイン名です。セラー ID は、インベントリのセラー（広告システムがこのインベントリに対して支払う相手）を識別するために使用されます。広告システム識別子とセラー ID の両方は、ads.txt ファイルで提供されるものと同じ値であるべきです。セラー ID が複数のエンティティを表すことは無効です。すべてのセラー ID は、そのセラー ID で取引されたインベントリに対して支払いを受ける単一のエンティティにのみマッピングされなければなりません。販売エンティティが広告システム内で複数のセラー ID を持つことは有効です。


## OpenRTB オブジェクト: SupplyChain

このオブジェクトは、サプライチェーン内のリンクと、サプライチェーンが完全かどうかの指標の両方を表します。

SupplyChain オブジェクトは、OpenRTB 2.6 以降では BidRequest.Source.schain 属性に、OpenRTB 2.5 では BidRequest.Source.ext.schain 属性に含めるべきです。OpenRTB 2.4 以前の場合は、BidRequest.ext.schain 属性を使用するべきです。

SupplyChain オブジェクトには以下の属性が含まれます:


| Attribute | Type | Description |
|-----------|------|-------------|
| complete | integer; required | チェーンが、サイト、アプリ、またはその他のインベントリ媒体の所有者に至るまでの取引に関与するすべてのノードを含んでいるかどうかを示すフラグ。0 = いいえ、1 = はい。 |
| nodes | object array; required | チェーンの順序で並べられた SupplyChainNode オブジェクトの配列。完全なサプライチェーンでは、最初のノードは取引に関与する最初の広告システムとセラー ID（つまり、サイト、アプリ、またはその他の媒体の所有者）を表します。不完全なサプライチェーンでは、最初の既知のノードを表します。最後のノードは、このビッドリクエストを送信しているエンティティを表します。 |
| ver | string; required | 使用中のサプライチェーン仕様のバージョン。"major.minor" の形式です。例えば、仕様のバージョン 1.0 の場合は、文字列 "1.0" を使用します。 |
| ext | object; optional | このオブジェクトに対する広告システム固有の拡張のためのプレースホルダー。 |


## OpenRTB オブジェクト: SupplyChainNode

このオブジェクトは、ノードの配列として SupplyChain オブジェクトに関連付けられています。これらのノードは、ビッドリクエストのサプライチェーンに参加するエンティティの ID を定義します。SupplyChainNode オブジェクトには以下の属性が含まれます:


| Attribute | Type | Description |
|-----------|------|-------------|
| asi | String; required | ビッダーが接続する SSP、エクスチェンジ、ヘッダーラッパーなどのシステムの正規ドメイン名。これは、委任されたシステムの明確な所有権を確立するために WHOIS および逆 IP ルックアップを容易にするため、親会社ドメインと異なる場合はシステムの運用ドメインである可能性があります。これは、ads.txt ファイルが存在する場合、セラーを識別するために使用される値と同じであるべきです。 |
| sid | string; required | 広告システム内のセラーまたはリセラーアカウントに関連付けられた識別子。これは、SSP/エクスチェンジが指定するフィールドでトランザクション（つまり OpenRTB ビッドリクエスト）で使用される値と同じでなければなりません。通常、OpenRTB では publisher.id です。OpenDirect では通常、パブリッシャーの組織 ID です。64 文字以内に制限するべきです。 |
| rid | String; optional | このセラーによって発行されたリクエストの OpenRTB RequestId。 |
| name | String; optional | 指定された seller_id で取引されるインベントリに対して支払いを受ける会社（法人）の名前。この値はオプションであり、広告システムの sellers.json ファイルに存在する場合は含めるべきではありません。 |
| domain | string; optional | このノードで表されるエンティティのビジネスドメイン名。この値はオプションであり、広告システムの sellers.json ファイルに存在する場合は含めるべきではありません。 |
| hp | integer; required | このノードがインベントリの支払いフローに関与するかどうかを示します。1 に設定すると、asi フィールドの広告システムが sid フィールドのセラーに支払い、そのセラーはチェーン内の前のノードに支払う責任を負います。0 に設定すると、このノードはインベントリの支払いフローに関与しません。SupplyChain のバージョン 1.0 では、このプロパティは常に 1 であるべきです。将来のバージョンの仕様で支払い処理を行わないノードが導入されることが予想されるため、明示的に含めることが必要です。実装者は、このフィールドをサポートし、下流の広告システムに送信されるビッドリクエストで SupplyChain オブジェクトを構築する際にこれを伝播するようにするべきです。 |
| ext | object; optional | このオブジェクトに対する広告システム固有の拡張のためのプレースホルダー。 |

asi および domain フィールドには、広告システムまたはセラーの正規ドメインのみを入力する必要があり、これらは照合のために OpenRTB Site.domain、sellers.json、ads.txt で使用されるドメインと同じであるべきです。完全な URL（またはスキーマ、つまり http:// や https://）は使用しないでください。このドキュメントの目的上、「ルートドメイン」は「パブリックサフィックス」に名前の 1 つの文字列を加えたものとして定義されます。実装者はルートドメインを導出するために Public Suffix リスト [16] を組み込むべきです。

有効な例:
example.com
example.co.uk

無効な例:
http://example.com
https://example.com/about-us.html


## 実装の詳細

リセラーが、自身のノードをチェーンに挿入せずに、前のセラーから SupplyChain オブジェクトをそのインベントリに対するリクエストにコピーすることは無効です。リセラーがチェーンに自身を挿入しない場合、そのビッドリクエストには SupplyChain オブジェクトを含めるべきではありません。

セラーが以前 SupplyChain オブジェクトを含んでいなかったインベントリを再販している場合、自身で SupplyChain オブジェクトを作成し、"complete" 属性を 0 に設定し、自身のノードを "nodes" 配列に挿入するべきです。

セラーが SupplyChain オブジェクトを持つインベントリを再販している場合、リセラーは既存のオブジェクトをコピーし、"complete" の元の値を保持し、自身のノードを "nodes" 配列の末尾に追加するべきです。

これがこのインベントリの最初のビッドリクエストである場合、SupplyChain オブジェクトは "complete" 属性を 1 に設定し、自身の情報のみを "nodes" 配列の唯一のノードとして作成するべきです。


## Examples（例）:

## 有効で完全な SupplyChain オブジェクト

### 最初のビッドリクエストの例（BidRequest1, seller = "directseller.com"）:


```
"bidrequest" : {
  "id": "BidRequest1",
  "app": {
    "publisher": {
      "id": "00001"
    }
  }
  "source": {
    "ext": {
      "schain": {
        "ver":"1.0",
        "complete": 1,
        "nodes": [
          {
            "asi":"directseller.com",
            "sid":"00001",
            "rid":"BidRequest1",
            "hp":1
          }
        ]
      }
    }
  }
}
```

### BidRequest1 の再販の例（BidRequest2, seller = "reseller.com"）:

```
"bidrequest" : {
  "id": "BidRequest2",
  "app": {
    "publisher": {
      "id": "aaaaa"
    }
  }
  "source": {
    "ext": {
      "schain": {
        "ver":"1.0",
        "complete": 1,
        "nodes": [
          {
            "asi":"directseller.com",
            "sid":"00001"
            "rid":"BidRequest1",
            "hp":1
          },
          {
            "asi":"reseller.com",
            "sid":"aaaaa",
            "rid":"BidRequest2",
            "hp":1
          }
        ]
      }
    }
  }
}

```

## 有効で不完全な SupplyChain オブジェクト

### SupplyChain オブジェクトをサポートしていない広告システムからの最初のビッドリクエストの例（BidRequest3, seller = "directseller.com"）:

```
"bidrequest" : {
  "id": "BidRequest3",
  "app": {
    "publisher": {
      "id": "00001"
    }
  }
  "source": {
    "ext": {
    }
  }
}
```

### SupplyChain オブジェクトをサポートする広告システムによる BidRequest3 の再販の例（BidRequest4, seller = "reseller.com"）:


```
"bidrequest" : {
  "id": "BidRequest4",
  "app": {
    "publisher": {
      "id": "aaaaa"
    }
  }
  "source": {
    "ext": {
      "schain": {
        "ver":"1.0",
        "complete": 0,
        "nodes": [
          {
            "asi":"reseller.com",
            "sid":"aaaaa",
            "rid":"BidRequest4",
            "hp":1
          }
        ]
      }
    }
  }
}
```
## 非 OpenRTB リクエストのための SupplyChain
上記のドキュメントは OpenRTB プロトコルを介した取引のみのガイダンスを提供しているため、このセクションでは OpenRTB ではなくタグを介して SupplyChain 情報を通信する標準的な方法について説明します。この状況は、広告システムがアドサーバー、ビデオプレーヤー、SSAI ベンダーなどに挿入して広告システムへの広告リクエストを開始できるタグを提供する場合に最も一般的に発生します。

**シリアライゼーションの目標:**
* SupplyChain オブジェクトのすべてのプロパティをサポートする
* シリアライズされたデータの URL エンコーディングの必要性を最小限に抑える
* SupplyChain の将来の変更に対する前方互換性をサポートする

**使用シナリオ:**
この付録では、業界標準の「キーバリューペア」を介して受信できる SupplyChain データを含む適切に構造化された文字列を定義する方法論を概説します。

受信側の広告システムがタグベースのリクエストを処理し、別の広告システムへの送信 OpenRTB リクエストを形成している場合、以下の手順が指定されます。まず、以下に説明するように受信した SupplyChain データを解析し、受信したデータで SupplyChain オブジェクトを作成して入力するべきです。最後に、広告システムはオブジェクト内の配列に自身の情報を追加するべきです。

受信側の広告システムがタグベースのリクエストを処理し、別の広告システムへの送信タグベースリクエストを形成している場合、以下の手順が指定されます。受信した文字列の先行する情報を変更せずに、既存の文字列に自身のノードを追加するべきです。

受信側の広告システムが OpenRTB リクエストを処理し、別の広告システムへの送信タグベースリクエストを形成している場合、以下の手順が指定されます。受信した SupplyChain オブジェクト内のデータを解析し、以下に指定されたとおりにシリアライズするべきです。自身のための仕様準拠の文字列を形成し、それを先行する文字列に追加するべきです。

**タグまたは URL を介した広告システムへの SupplyChain の受信**
広告システムは、広告タグまたは VAST URL で文字列シリアライズされた SupplyChain を受け入れるためのパラメータをサポートするべきです。このパラメータは "schain" とすることが推奨されます。

例えば、アドサーバーは次のようなディスプレイ広告タグ形式を持つ場合があります:

```
<script src="https://ads.exchange1.com/srv?pid=194&sz=300x250&plid=2842181&schain=[SUPPLYCHAIN GOES HERE]"></script>
```

または次のような VAST URL 形式:

```
https://ads.exchange1.com/srv?pid=194&sz=v&plid=2842185&schain=[SUPPLYCHAIN GOES HERE]
```

**他のタグまたは URL への SupplyChain の送信**
広告システムは、SupplyChain オブジェクトを別の広告タグまたは VAST URL に渡す必要がある場合があります。これは、SupplyChain 情報が OpenRTB を介して広告システムに受信されたか、上記のように文字列シリアライズされた SupplyChain を介して受信されたかに関係なく発生する可能性があります。この目的のために、広告システムは文字列シリアライズされた SupplyChain を出力するためのマクロ（例えば $SCHAIN）をサポートすることが推奨されます。このマクロの出力は、広告システムのノードが追加された文字列シリアライズされた SupplyChain でなければなりません。

### OpenRTB SupplyChain オブジェクトの URL パラメータへのシリアライゼーション
推奨 URL パラメータ: schain

### シリアライゼーションの形式
シリアライゼーションは 2 つの項目で構成されます。SupplyChainObject プロパティと SupplyChainNode 配列です。これら 2 つの項目はバン（"!"）文字で区切られます。

```{SupplyChainObject}!{SupplyChainNode array}```

### SupplyChainObject プロパティ
SupplyChain オブジェクトには 2 つのプロパティがあります。version と complete です。これら 2 つの値はシリアライズされた値の先頭に含まれなければならず、カンマ（","）で区切られなければなりません。

```ver,complete```

### SupplyChainNode プロパティの配列
SupplyChainObject プロパティに続いて、SupplyChain 内のすべてのノードを含めなければなりません。SupplyChainNode オブジェクトのプロパティはカンマ（","）で区切られなければならず、複数のノードがある場合は、各ノードはバン（"!"）文字で区切られなければなりません。

プロパティの順序は以下のとおりです:

```asi,sid,hp,rid,name,domain,ext```

ext プロパティの内容はエクスチェンジ固有であり、このドキュメントではこのオブジェクトの値のシリアライゼーション方法を指定する試みは行いません。

オプションの SupplyChainNode プロパティ値は省略でき、末尾のセパレータはオプションで除外できます。

Example:
```exampleexchange.com,12345,1,,,```

or

```exampleexchange.com,12345,1```

プロパティの値に URL エンコーディングが必要な場合（RFC 3986 または Wikipedia の投稿を参照）、またはカンマやバン文字が含まれる場合は、URL エンコードするべきです。プロパティを区切るために使用されるカンマはエンコードしないでください。

Example:
```exampleexchange.com,123%2CB,1,,,```

これは、支払いを処理する exampleexchange.com 上の "123,B" という sid を表します。

### Examples（例）

### シングルホップ - チェーン完全

**SupplyChain**
```
"schain" : {
    "ver":"1.0",
    "complete":1,
    "nodes":[
        {
            "asi":"exchange1.com",
            "sid":"1234",
            "hp":1,
            "rid":"bid-request-1",
            "name":"publisher",
            "domain":"publisher.com"
        }
    ]
}
```

**Serialized Value**
```
1.0,1!exchange1.com,1234,1,bid-request-1,publisher,publisher.com
```

### シングルホップ - チェーン完全、オプションフィールド欠落

**SupplyChain**
```
"schain" : {
    "ver":"1.0",
    "complete":1,
    "nodes" : [
        {
            "asi":"exchange1.com",
            "sid":"1234",
            "hp":1
        }
    ]
}
```

**Serialized Value**
```1.0,1!exchange1.com,1234,1,,,```

### マルチホップ - すべてのプロパティが提供

**SupplyChain**
```
"schain" : {
    "ver": "1.0",
    "complete" : 1,
    "nodes" : [
        {
            "asi":"exchange1.com",
            "sid":"1234",
            "hp":1,
            "rid":"bid-request-1",
            "name":"publisher",
            "domain":"publisher.com"
        },
        {
            "asi":"exchange2.com",
            "sid":"abcd",
            "hp":1,
            "rid":"bid-request-2",
            "name":"intermediary",
            "domain":"intermediary.com"
        }
    ]
}
```
**Serialized Value**
```1.0,1!exchange1.com,1234,1,bid-request-1,publisher,publisher.com!exchange2.com,abcd,1,bid-request2,intermediary,intermediary.com```

### マルチホップ - チェーン完全、オプションフィールド欠落

**SupplyChain**
```
"schain" : {
    "ver":"1.0",
    "complete":1,
    "nodes":[
        {
            "asi":"exchange1.com",
            "sid":"1234",
            "hp":1
        },
        {
            "asi":"exchange2.com",
            "sid":"abcd",
            "hp":1
        }
    ]
}
```

**Serialized Value**
```1.0,1!exchange1.com,1234,1,,,!exchange2.com,abcd,1,,,```

### マルチホップ予想 - チェーン不完全

**SupplyChain**
```
"schain" : {
    "ver":"1.0",
    "complete" :0,
    "nodes":[
        {
            "asi":"exchange2.com",
            "sid":"abcd",
            "hp":1
        }
    ]
}
```

**Serialized Value**
```1.0,0!exchange2.com,abcd,1,,,```

### シングルホップ - チェーン完全、エンコードされた値

**SupplyChain**
```
"schain" : {
    "ver":"1.0",
    "complete":1,
    "nodes":[
        {
            "asi":"exchange1.com",
            "sid":"1234!abcd",
            "hp":1,
            "rid":"bid-request-1",
            "name":"publisher, Inc.",
            "domain":"publisher.com"
        }
    ]
}
```

**Serialized Value**
```1.0,1!exchange1.com,1234%21abcd,1,bid-request-1,publisher%2c%20Inc.,publisher.com```
