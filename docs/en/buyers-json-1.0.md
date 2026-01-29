---
title: "buyers.json 1.0"
description: "Declares the identity of buyers (advertisers, agencies, etc.) purchasing ad inventory as public information, enhancing transparency and fraud prevention in the digital advertising demand-side supply chain."
---
Released June 2021

Please email support@iabtechlab.com with feedback or questions. This document is available online at [https://iabtechlab.com/buyers-json-demand-chain](https://iabtechlab.com/buyers-json-demand-chain)

© IAB Technology Laboratory

# About IAB Tech Lab

The IAB Technology Laboratory is a nonprofit research and development consortium charged with producing and helping companies implement global industry technical standards and solutions. The goal of the Tech Lab is to reduce friction associated with the digital advertising and marketing supply chain while contributing to the safe growth of an industry.

The IAB Tech Lab spearheads the development of technical standards, creates and maintains a code library to assist in rapid, cost-effective implementation of IAB standards, and establishes a test platform for companies to evaluate the compatibility of their technology solutions with IAB standards, which for 18 years have been the foundation for interoperability and profitable growth in the digital advertising supply chain. Further details about the IAB Technology Lab can be found at [https://iabtechlab.com.](https://iabtechlab.com/)

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

#　 1 Abstract

As part of a broader effort to eliminate malvertising and other ad quality issues from the digital advertising ecosystem, buyers.json enables sellers to identify who is buying their inventory. The primary driver for this system is the need for sellers to identify buyers in all their forms across all demand sources. This aims to help publishers better monitor spend on their inventory, solve many forms of malvertising, and ultimately protects publishers and their audiences.

For best effect, buyers.json should be used in conjunction with the OpenRTB DemandChain object to provide a comprehensive view into the complete chain of buyer entities that are involved in purchasing an impression.

# 2 Introduction

Lack of transparency into buyer identity is one of the chief obstacles to eliminating malvertising. Malvertisers take advantage of the opaque and highly fragmented nature of the digital advertising ecosystem by exploiting the weakest entry points and jumping frequently from DSP to DSP. As soon as they are found out on one DSP, malvertisers seamlessly shift their campaigns to a new one. Publishers and SSPs often don’t have insight into the identities of buyers and therefore can’t block a known bad entity across all the access points at once. The end effect is likened to the whack-a-mole arcade game, where the same entity appears again and again across different DSPs.

buyers.json is a mechanism for advertising systems and other intermediaries between payor and publisher to publicly declare the buyers that they represent. Armed with this information, publishers and SSPs can more easily identify the sources of malvertising attacks, identify problematic buyers across multiple demand sources, and take appropriate action to protect themselves and their users.

buyers.json follows in the path set by the industry’s successful sell-side transparency efforts such as ads.txt, Sellers.json, and the SupplyChain Object. As Sellers.json boosted transparency into the identities of sell-side entities, buyers.json does the same for the buy side.

This document describes the format for encoding the instructions to be consumed by advertising systems and their customers.

buyers.json is designed to be used in conjunction with the OpenRTB DemandChain object. While these two specifications together provide for significant improvements in transparency that can be used to combat malware and other problematic demand, they cannot solve for every potential form of abuse. Additional transparency efforts may be needed to prevent spoofing of agency identity. One such effort to explore is the use of cryptographic techniques (like ads.cert) to prevent manipulation of demand by untrustworthy intermediaries, among others, but such efforts are beyond the scope of this specification.

# 3 Specification

## 3.1 Access Method

DSPs and other intermediaries between the buyer and the content publisher should post the buyers.json file on their root domain. For the purposes of this document the “root domain” is defined as the “public suffix” plus one string in the name. Crawlers should incorporate a Public Suffix list to derive the root domain.

Some entities who post buyers.json files may have multiple domains, one of which would be the corporate domain and the other a distinct ad-serving domain. To link DemandChain data to buyers.json data, the buyers.json file should be available on any domain that is present in the "asi" (advertising system identifier) field of a DemandChainNode object, perhaps by redirecting to the canonical file.The contents of buyers.json must be accessible via HTTPS from the root domain under a standard relative path on the server host: "/buyers.json" with the HTTP request header containing "Content-Type: application/json". Additionally, using "Content-Type: application/json; charset=utf-8" explicitly signals UTF8 support.

For convenience we refer to this resource as the "buyers.json file”. Despite the use of the word "file," the resource need not originate from a file system. If the server response indicates Success (HTTP 2xx Status Code), the advertising system must read the content, parse it, and use the declarations as intended. If the server response indicates an HTTP redirect (301, 302, 307 status codes), the advertising system should follow the redirect and consume the data as authoritative for the source of the redirect, if no more than a single redirect away from the original root domain defined as the public suffix plus one string. Multiple redirects are valid as long as only one redirect leads off the original root domain. The behavior for HTTP 4xx and 5xx responses is undefined and is left to the implementations to handle.

## 3.2 File Format

All data in the file is serialized using JSON (JavaScript Object Notation). The parent JSON object and all child objects are written to the buyers.json file.

## 3.3 Expiration

Systems that consume /buyers.json should cache the files and periodically verify that the cached copy is fresh before using its contents.

Standard HTTP cache-control mechanisms can be used by both origin server and robots to influence the caching of the /buyers.json file. Specifically, consumers and replicators should take note of the HTTP Expires header set by the origin server. A maximum expiry of 7 days is recommended. If no cache-control directives are present, consuming systems should default to an expiry of 7 days.

## 3.4 Implementation

All intermediaries between the buyer and publisher should publish a buyers.json file at the following location:

```
https://{root_domain}/buyers.json
```

## 3.5 Object Specifications

### Object: Parent

The Parent object is the top-level object of a buyers.json file. It is a container for all properties in a buyers.json file.

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| Buyers | object array; required | The list of all Buyers objects that are represented by the advertising system. All buyers must be included even if they are confidential. |
| Identifiers | object array; optional | Array of Identifier objects associated with this advertising system. Examples could be TAG-Ids, Dun & Bradstreet business identifiers, or any custom identifier that a consuming advertising system might need.  Note: The IAB Tech Lab recommends the use of TAG-Id, especially since TAG has plans to include requirements around the use of buyers.json & DemandChain Object in their Certified Against Malware program, which will help the overall goals of the buy-side transparency initiatives. |
| Name | string; optional | The name that this advertising system wants to be identified as in other advertising systems. |
| contact_email | string; optional | An email address to use to contact the advertising system for questions or inquiries about this file. |
| contact_address | string; optional | The business address of the advertising system. |
| version | string; required | The version of this spec, currently the only valid value is the string "1.0" (numeric values are invalid). |
| last_updated | string; recommended | The date and time this file was last changed, in ISO 8601 format, UTC (Zulu) time. Example: "2020-12-01T00:01:02Z". To prevent unnecessary duplication in retrieval systems, this timestamp should not be updated if actual file contents have not changed. |
| ext | object; optional | Placeholder for advertising-system specific extensions to this object. |

### Object: Buyers

This object identifies the legal entity that pays for inventory bought on behalf of buyer_id. In most cases, a buyer_id should represent only a single legal entity. In circumstances where the entity is a managed service desk or similar operation servicing a variety of buyers, that entity must post its own buyers.json file and be represented by its own DemandChain node. In other words, any individual buyer_id that aggregates demand from multiple legal entities should consider itself an intermediary and also participate in these transparency efforts. See the section "DSP with Managed Service Desk" in the Implementation Guide for more detailed examples.

A buying entity may have multiple buyer_ids within an advertising system.

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| buyer_id | String; required | A unique identifier for the buyer entity. This should be the same ID that appears in the bidresponse.seatbid[].seat property, if it is present, of an OpenRTB response. This should also be the value included in a DemandChainNode.bsid in a DemandChain Object. |
| is_confidential | Integer; optional, default: 0 | Indicates whether the identity of the buyer is confidential, where 0 = is not confidential and 1 = is confidential. |
| buyer_type | string; required | A description of the type of account, either ADVERTISER, INTERMEDIARY, or BOTH.  A value of "ADVERTISER" indicates that this account is controlled by the advertiser that purchased the inventory.  A value of “INTERMEDIARY" indicates that this account is controlled by an entity (such as an agency or reseller) working on behalf of the advertiser.  A value of “BOTH" indicates that this account is controlled by an entity that works as either an advertiser or intermediary depending on the business context.  This field should be treated as case insensitive when interpreting the data. |
| name | string; required when is_confidential=0 | The name of the company (the legal entity) that pays for inventory that is transacted under the given buyer_id. Can be omitted only when is_confidential is set to 1. |
| domain | string; required if buyer has a web presence and is_confidential=0 | The business domain name of the company (the legal entity) that pays for inventory that is transacted under the given buyer_id.  This must be a root domain only; do not format as a URL. Correct: *example.com.* Incorrect: [*https://example.com/.*](https://example.com/) |
| comment | string; optional | Any helpful description for this seat. Buyers that have multiple buyer ids on a single platform can make use of the comment field to describe what this specific buyer_id represents. |
| created\_on | string; recommended | Date of creation of the buyer's seat. Can be useful to estimate how long the buyer has been active (malvertising buyers tend to have short lifespan).  The date value should be represented in ISO 8601 standard format, e.g. 2020-10-06. |
| ext | object; optional | Placeholder for advertising-system specific extensions to this object. |

## 3.6 Enumerated List Specification

Identifier Names

The following list defines standard identifiers that should be used in the identifier list.

| **Name** | **Description** |
| --- | --- |
| TAG-ID | Trustworthy Accountability Group ID |
| DUNS | Dun & Bradstreet DUNS Number |

# 4 Sample File Contents

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
