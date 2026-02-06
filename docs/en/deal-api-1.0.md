---
title: "Deal Sync API Specification"
sidebarTitle: "Deal Sync API"
description: "An API specification for synchronizing deal information between buy-side and sell-side platforms. It reduces manual entry, increases transparency in curated deals, and standardizes deal setup across systems."
---

Deal Sync API Specification

# About the IAB Tech Lab

The IAB Technology Laboratory is a nonprofit research and development consortium charged with producing and helping companies implement global industry technical standards and solutions. The goal of the Tech Lab is to reduce friction associated with the digital advertising and marketing supply chain while contributing to the safe growth of an industry. The IAB Tech Lab spearheads the development of technical standards, creates and maintains a code library to assist in rapid, cost-effective implementation of IAB standards, and establishes a test platform for companies to evaluate the compatibility of their technology solutions with IAB standards, which for 18 years have been the foundation for interoperability and profitable growth in the digital advertising supply chain. Further details about the IAB Technology Lab can be found at www.iabtechlab.com

### IAB Tech Lab Lead:

Hillary Slattery, Sr. Director of Product, IAB Tech Lab

### License

This specification is licensed under a Creative Commons Attribution 3.0 License. To view a copy of this license, visit creativecommons.org/licenses/by/3.0/ http://creativecommons.org/licenses/by/3.0/ or write to Creative Commons, 171 Second Street, Suite 300, San Francisco, CA 94105, USA.

### Disclaimer

THE STANDARDS, THE SPECIFICATIONS, THE MEASUREMENT GUIDELINES, AND ANY OTHER MATERIALS OR SERVICES PROVIDED TO OR USED BY YOU HEREUNDER (THE "PRODUCTS AND SERVICES") ARE PROVIDED "AS IS" AND "AS AVAILABLE," AND IAB TECHNOLOGY LABORATORY, INC. ("TECH LAB") MAKES NO WARRANTY WITH RESPECT TO THE SAME AND HEREBY DISCLAIMS ANY AND ALL EXPRESS, IMPLIED, OR STATUTORY WARRANTIES, INCLUDING, WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AVAILABILITY, ERROR-FREE OR UNINTERRUPTED OPERATION, AND ANY WARRANTIES ARISING FROM A COURSE OF DEALING, COURSE OF PERFORMANCE, OR USAGE OF TRADE. TO THE EXTENT THAT TECH LAB MAY NOT AS A MATTER OF APPLICABLE LAW DISCLAIM ANY IMPLIED WARRANTY, THE SCOPE AND DURATION OF SUCH WARRANTY WILL BE THE MINIMUM PERMITTED UNDER SUCH LAW. THE PRODUCTS AND SERVICES DO NOT CONSTITUTE BUSINESS OR LEGAL ADVICE. TECH LAB DOES NOT WARRANT THAT THE PRODUCTS AND SERVICES PROVIDED TO OR USED BY YOU HEREUNDER SHALL CAUSE YOU AND/OR YOUR PRODUCTS OR SERVICES TO BE IN COMPLIANCE WITH ANY APPLICABLE LAWS, REGULATIONS, OR SELF-REGULATORY FRAMEWORKS, AND YOU ARE SOLELY RESPONSIBLE FOR COMPLIANCE WITH THE SAME, INCLUDING, BUT NOT LIMITED TO, DATA PROTECTION LAWS, SUCH AS THE PERSONAL INFORMATION PROTECTION AND ELECTRONIC DOCUMENTS ACT (CANADA), THE DATA PROTECTION DIRECTIVE (EU), THE E-PRIVACY DIRECTIVE (EU), THE GENERAL DATA PROTECTION REGULATION (EU), AND THE E-PRIVACY REGULATION (EU) AS AND WHEN THEY BECOME EFFECTIVE.

# Introduction

This API has multiple implications including lowering manual entry by making the high-level terms of the deal clear so automated setups can be more easily executed. It also adds transparency into Curated deals that is not currently available in the bid stream.

## Goals

- Decrease manual entry of deal information across systems by providing a way for the terms of a deal to be input and sent to the system that will deliver the deal to review and accept.
- Describe what the selling system deal includes at a high level
- Know which parties were involved in curating and selling the package

## What it is

- API that provides subscribers with static information about a given Deal that outlines the tenents of the Deal.
- This MVP is a one-party design for the origin system to PUSH information about the deal into the receiving system(s) from the system where it was created (e.g. SSP → DSP). It also allows the same system to query the receiving system for the Deal status after initial deal send. Future versions will likely add support for bi-directional communications.
- Version 1.0 of this API does not support differential overrides, but 1.1 will. For the 1.0 version, periodic polling by the deal receiver can be used as a fallback. To ensure data integrity, deal receivers are encouraged to implement periodic polling as a fallback mechanism to handle any missed notifications.

## What it isn't

- This is a separate API that is **NOT** included in OpenRTB Request/Response
- Does not include real-time information contained in the bid request or determine whether or not a deal applies. Implementers are strongly encouraged to validate the conditions laid out in this deal with OpenRTB requests to ensure their expectations are being met.
- The MVP of this API does NOT support proposals, revisions, or negotiations. It is assumed those are known to implementers *a priori.* Future versions will likely contemplate this functionality.
- The MVP is not meant to support discoverability in deal marketplaces. Future versions may include that functionality.

## Considerations

- The values of these fields are meant to be an outline of business terms agreed to between buyers and sellers *a priori*. The information contained in this API should be used as a guide of what the terms that were agreed to, but they should never be used to bid without validating that information coming from the OpenRTB Bid Request is in line with the terms laid out in this API.
- Deal criteria provided via this channel are not guaranteed to be accurately reflected in bid requests containing the associated deal ID. It is the responsibility of the buyer to validate bid requests that contain the deal ID conform to the deal criteria. In other words, buyers should ALWAYS apply targeting matching the terms outlined in any deal on their side. For example, if a deal is struck for US only inventory, buyers should include that targeting in their DSP when trafficking the campaign.
- If bid requests continually do not match the expectations laid out in the API, a conversation should be had between the buyer and seller to continue negotiations offline.
- It is not possible to validate that the party selling the inventory has been authorized without including app bundle or site id that matches the publishers (app)ads.txt file. Deal IDs receiving requests without that information should be used rarely and closely monitored.

---

# Deal API Specification
An HTTP POST endpoint implemented by the receiving system to accept data pushed from the origin system. Configuration of push calls is out of scope for this specification and is the responsibility of the Origin system.

## Object: Deal

| Attribute | Type | Description |
|-----------|------|-------------|
| `id` | string; **required** | A unique identifier for the direct deal in origin's namespace. |
| `name` | string, recommended | Name of the deal as created in the origin system. Note: This name may be displayed to the buyer. The person inputting the deal into the `origin` system should consider that when setting up the deal. |
| `created` | string | UTC timestamp in seconds in ISO-8601 of when the deal was created in the Origin system |
| `sellerstatus` | int, default 0, recommended | Status of the deal in the sellers system where:  `0` = deal is active  `1` = deal is paused  `2` = deal is pending   `4` = deal is complete (ie. selling scomplete (ie. selling system shows deal has completed)   `4` = deal is archived (cannot be active again) |
| `origin` | string, **required** | The advertising system domain of the business entity that will receive bid responses for the deal, typically the SSP hosting the API. |
| `seller` | string, recommended | Canonical domain of the business entity who sold the deal. This may be the same as the origin or curator, but it also could be any intermediate seller.    [See Implementation Guidance for additional detail](#origin-curator-and-seller) |
| `desc` | string | Short description for the deal to help the receiver locate the deal once it has been sent. It is strongly recommended to keep this field to 250 characters or less. |
| `wseat` | string array, recommended | Allowed list of buyer seats (e.g., advertisers, agencies) allowed to bid on this impression.   IDs of seats and knowledge of the buyer's customers to which they refer must be coordinated between bidders and the exchange <i>a priori</i>.   At most, only one of `wseat` and `bseat` should be used in the same request. Omission of both implies no seat restrictions. |
| `bseat` | string array | Block list of buyer seats (e.g., advertisers, agencies) restricted from bidding on this impression. IDs of seats and knowledge of the buyer's customers to which they refer must be coordinated between bidders and the exchange <i>a priori</i>.   At most, only one of `wseat` and `bseat` should be used in the same request. Omission of both implies no seat restrictions.|
| `adtypes` | int array | The format of the ad creative(s) supported by the inventory in the deal:  `1` = Banner  `2` = Video  `3` = Audio  `4` = Native  If this is empty or missing, the deal is assumed to apply to all types of ad creative. |
| `auxdata` | int | Indicates if there is non-publisher data (i.e. a non-publisher data layer) applied in this package with an associated fee where:  `0` = undisclosed  `1` = yes, at start of deal and will not be modified  `2` = yes and subject to change after start of deal  `3` = no and will not be modified  `4` = no and subject to change after start of deal  [See implementation guidance for additional detail](#auxiliary-data) |
| `pubcount` | int | Indicates if there is more than one publishing company:  `0` = undisclosed  `1` = single publisher  `2` = multi-publisher [See implementation guidance for additional detail](#publisher-count) |
| `dinventory` | int | Indicates if the inventory for the deal is dynamic, meaning sites or applications included in the deal may update after the deal is live where:  `0` = undisclosed  `1` = inventory will NOT update once the deal goes live  `2` = inventory where this deal may run is updated dynamically.   [See implementation guidance for additional detail](#dynamic-inventory) |
| `terms` | object, **required** | Terms of the deal. See [Object: Terms](#object-terms) for additional detail |
| `inventory` | object | Information about the inventory included in the deal. This object should only be included when the deal is for a static set of sites or applications (`dinventory=1`).   See [Object: Inventory](#object-inventory) for additional detail |
| `curation` | object | Information about the curation package if applicable.   See [Object: Curation](#object-curation) for additional detail. |
| `ext` | object | Placeholder for deal-specific extensions |

## Object: Terms

| Attribute | Type | Description |
|-----------|------|-------------|
| `startdate` | string | UTC timestamp in seconds in ISO-8601 of when the deal starts |
| `enddate` | string | UTC timestamp in seconds in ISO-8601 of when the deal ends. Evergreen or always on deals should leave this field blank. |
| `countries` | string array | An array of country codes in which the deal is available, where country code is a string using ISO-3166-3. If this is empty or missing, the deal is assumed to apply to all countries. |
| `dealfloor` | float | Minimum bid for impressions for this deal expressed in CPM. Unless `pricetype` is Fixed, this should be used as guidance to buyers.    [See Implementation Guidance for additional detail](#price-and-floor-guidance) |
| `cur` | string; default "USD" | Bid currency using ISO-4217 alpha codes. |
| `guar` | int | Indicates that the deal is of type guaranteed and the bidder must bid on the deal, where 0 = not a guaranteed deal, 1 = guaranteed deal. |
| `pricetype` | int, default 2 | Deal Price Type where:  `0` = Dynamic (ie. auction type will be provided by `request.at` attribute in OpenRTB Bid Request)  `1` = First Price  `2` = Second Price Plus  `3` = Fixed Price Exchange-specific auction types can be defined using values 500 and greater. |
| `units` | int | Number of units (impressions) over the specified start and end date of the deal. If the deal is guaranteed, this number should be provided. If the deal is not guaranteed this may be omitted. |
| `totalcost` | float | The total cost over the specified start and end date of the deal. If the deal is guaranteed, this value should be provided. If the deal is not guaranteed this may be omitted.    [See Implementation Guidance for additional detail](#price-and-floor-guidance) |
| `ext` | object | Placeholder for deal-specific extensions |

## Object: Inventory

Attributes in Inventory objects are meant to be an overview of the kinds of ads and inventory where the deal might appear.

| Attribute | Type | Description |
|-----------|------|-------------|
| `inclinventory` | integer array | High-level information about the kind of inventory included in the deal:  `1` = site  `2` = app  `3` = dooh  `4` = audio  `5` = endemic  `6` = other    If this is empty or missing, the deal is assumed to apply to all types of inventory |
| `devicetype` | integer array | The general type of device. Refer to List: [Device Type](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/main/AdCOM%20v1.0%20FINAL.md#list--device-types-) in AdCOM 1.0 |
| `sellerids` | string array | The identifier associated with the seller or reseller account within the advertising system. If used, the values in this attribute must contain the same value used in transactions (i.e. OpenRTB bid requests) in the field specified by the SSP/exchange.   An empty list implies the deal may runs across all sellers.   Typically, in OpenRTB, this is `publisher.id`.   For OpenDirect it is typically the publisher's organization ID. Should be limited to 64 characters in length. |
| `sitedomains` | string array | An array containing one or more site domain(s).   An empty list implies the deal may run across many unspecified site domain(s).|
| `appbundles` | string array | An array containing one or more bundle/package name(s) of the app.   An empty list implies the deal may run across many unspecified bundles/package(s) |
| `cat` | string array | Array of IAB Tech Lab content categories included in the deal. The taxonomy to be used is defined by the cattax field. |
| `cattax` | integer | The taxonomy in use for the cat attribute. Refer to [List: Category Taxonomies](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/main/AdCOM%20v1.0%20FINAL.md#list_categorytaxonomies). |
| `ext` | object | Placeholder for deal-specific extensions |


## Object: Curation

Information about the selection and organization of inventory using technology and data, with the goal of creating effective packages for advertisers through prepackaged or real-time operations.

| Attribute | Type | Description |
|-----------|------|-------------|
| `curator` | string | Canonical domain of the business entity that did the packaging of inventory, technology and/or data. Most often, this will be the seller of the deal. |
| `cdealid` | string | Unique identifier for the deal in the Curators namespace. |
| `curfeetype` | int | Fee type being applied for curation of the deal:  `0` = undisclosed  `1` = percentage of spend  `2` = flat fee  `3` = CPM  `4` = no fee is paid for curation services  [See Implementation Guidance for additional detail](#curation-fee) |
| `ext` | object | Placeholder for deal-specific extensions |

---

# Receiving System Endpoint
An HTTP POST endpoint implemented by the receiving system that allows the Origin system to request current information for a specific deal.

## Object: BuyerSeat

Information about the status of the deal in the buying system at a seat level.

| Attribute | Type | Description |
|-----------|------|-------------|
| `version` | string, **required** | Version of the Deal API in use |
| `id` | string, **required** | A unique identifier for the deal as passed in the initial push that this response is referring to. This should always be the same id as `deal.id` |
| `buyerstatus` | object array | Information about the buying seat where the Deal will be trafficked |
| `ext` | object | Placeholder for deal-specific extensions |

## Object: BuyerStatus

Information about the status of the deal at a seat level in the buying system.

| Attribute | Type | Description |
|-----------|------|-------------|
| `buyerseatid` | string | Seat ID in the buying system that the response refers to |
| `status` | int | Status of the deal in the buying system:  `0` = pending approval  `1` = buyer has approved (ie. non PG deal is ready for bid requests)  `2` = buyer has rejected  `3` = ready to serve (ie. deal is in a campaign - ready to receive bid requests, relevant especially for PG deals)  `4` = active (i.e. deal is actively serving impressions)  `5` = paused  `6` = complete (ie. buying system shows deal has completed)|
| `ext` | object | Placeholder for deal-specific extensions |

---

# Implementation Guidance

## Matching Bid Requests to Deals

Some level of trust is required when buying any Deal ID. It is incumbent on the buyer of the deal to compare information from the Deal API with information contained in OpenRTB Bid Requests to ensure that it meets their expectations.

Version 1.0 of this API does not support deal revisions. However, some attributes may be subject to change over the flight of the deal. Conversations between implementers should be had around what attributes, if any, may be subject to change after the deal has gone live.

The `deal.id` from both the sender and receiver should match the `deal.id` in the OpenRTB request when bidding. Implementers should use the Deal ID from the Origin system that did the PUSH.

Implementers are strongly encouraged to discuss where targeting criteria will be set. In instances where additional targeting will be applied in the receiving system, implementers should discuss potential implicaitons to delivery if sources of targeting may differ.

## Authorization

Supply Chain validation should always be done using Object: Supply Chain from OpenRTB. If this information is unavailable, implementers should proceed with extreme caution with the understanding that there is no mechanism to know if a given path is authorized to sell the inventory.

## Sending and Receiving Information

To send information about a new deal, the origin system will send a PUSH request to the receiving system partner's API endpoint.

Once a deal has been sent by the origin system to the receiving system, it may query the endpoint setup by the receiving system for information about the status of the Deal.

Implementers may choose to accept incoming webhooks to their API endpoints for events. Please discuss this feature and support with your chosen integration partners.

## Deal Object Guidance

### Auxiliary Data

`auxdata` should be used whenever any non-publisher data is expected to be part of a given deal. This will most often be traditional data providers, but can include optimization services that do NOT belong to the publisher. While the non-publisher data entities are not named, if any company is being paid for their data and/or optimization, this value should indicate the presence of non-publisher data.

This attribute also communicates information about whether or not additional data layers may be applied after the deal has gone live. For example, a deal starts with some additional data and expects the list of data and/or optimization services to be added or updated as the deal is in flight should use a value of 2.

### Publisher Count

`pubcount` is meant to communicate if the deal is for a single publishing company, or if it spans multiple publishing companies. Deals covering a single company with multiple web and app properties are considered to be a single publisher. Inventory aggregation services representing multiple publishing sites may also be considered a single publisher deal.

Note that the `pubcount` attribute does **not** contemplate non-publisher parties, including ad tech stacks involved in the transaction. Intermediaries should be identified using Supply Chain Validation from OpenRTB requests.

### Dynamic Inventory

`dinventory` communicates information about whether or not the sites and apps included in the initial offering are expected to be updated after the deal goes live. In other words, this attribute communicates the expectation that inventory will (or will not) change by adding or removing sites and/or apps after the deal has gone live. Implementers are strongly encouraged to communicate and discuss the specifics of any and all inventory updates to ensure expectations are met.

## Terms Object

Price attribute must be provided if the deal is a fixed price deal, especially if it's a programmatic guaranteed deal, but otherwise can be used as pricing guidance or not provided at all if there is no pricing guidance (for example, for a Run-of-Exchange deal where there is no pricing guidance)

Where multiple DSP seats are included, per seat acceptance/rejection is on the DSP to surface in their internal systems and User Interfaces.

Examples of Deal name and description so there's a reference point for a standard way of what the fields should contain

## Inventory Object

This object should only be included when the deal is for a static set of sites or applications (`dinventory=1`).

## Included Inventory

This attribute conveys the type of inventory where the deal will run, not the specifics of the inventory itself. Therefore, there is no specific object in OpenRTB that directly relates to this attribute.

For example, `inclinventory.adtype=1,2` means the deal is inclusive of both banner and video ads. Implementers should expect to see ORTB bid requests using either `imp.banner` or `imp.video` once the deal is in flight.

## Price and Floor Guidance

Historically deals have been negotiated at agreed upon rates to guarantee delivery at a certain price. In the new world many SSPs and curators aggregate media around data points that are not directly related to the inventory itself. Impressions for deals thus curated could have varying price points on a request by request basis. In lieu of a floor provided in these cases, suppliers offer bid guidance that will provide an effective win rate across inventory but do not describe the individual floors of the bid requests included in the deal.

## Origin, Curator, and Seller

The `origin` attribute refers to the system with the UI where the deal is first input. This will typically be an SSP.

The `curator` attribute names the business entity that did the packaging of inventory, technology and/or data. Most often, although not always, this will be the party that sold the deal to the buyer.

The `seller` attribute represents the business entity who has sourced the demand (aka contracted with the buyer of the deal). When this is NOT either of the entities named in the `origin` or `curator` attributes, this field can be especially valuable.

### Example 1

- SALESHOUSE has the sales team and sources the demand
- The curated deal incorporates data provided by DATA PROVIDER A, DATA PROVIDER B, and potentially DATA PROVIDER C and/or DATA PROVIDER D
- The deal is entered into the SSP
- CURATOR does all the ops to help SALESHOUSE launch the deal

In this case the `seller`=saleshousedomain.com, the `curator`=curatordomain.com, and the `origin`=sspdomain.com

### Example 2

- PUBLISHER has an agreement with DATA PROVIDER A to decorate bid requests and packages the publisher's inventory
- PUBLISHER sources demand for the deal
- PUBLISHER inputs the deal into SSP User interface

In this case the `seller`=publishercompany.com, the `curator`=datacompany.com, and the `origin`=sspdomain.com

## Curation Object

### Curation Fee

`curationfee` provides information about the type of fee being applied in the bidstream, but not what that fee is. For example, if a curator is charging a CPM of $5, the `curationfee` will equal 3 because it is a CPM. If a curator is charging a flat fee of $100, the value sent in the `curationfee` attribute will be 2, because it is a flat fee. If the curator is packaging their data alongside the inventory and not taking a specific fee for the Curation service itself, the value will be 4 for no fee.

## Example Scenarios

| Scenario | curationfee | auxdata | pubcount | dinventory |
|----------|:-----------:|:-------:|:--------:|:----------:|
| Publisher packages their O&O inventory and data, and sells a deal to a buyer. No other party is or will be involved in the deal and the inventory will remain static throughout the term of the deal. | 4 | 3 | 1 | 1 |
| Data company packages their data across multiple publishers, but does not charge a fee for the specific curation service. Data providers will not be changed, but inventory may be updated after the start of the deal. | 4 | 1 | 2 | 2 |
| Curation company charges a CPM fee to aggregate inventory across multiple publishers that they will add and remove as the deal is in flight to optimize deal performance. They have an optimization service, and work with additional data providers to increase addressability, and expect to add additional data partners throughout the flight. | 3 | 2 | 2 | 2 |
| Curation company works with inventory aggregation company that regularly adds new websites and charges a % of spend to optimize deals. They do not currently work with other data providers, but may layer them in based on deal performance. | 1 | 4 | 1 | 2 |
| SSP pays a Curator a CPM to decorate inventory across the SSP universe that they do not pass on to the publishers. All inventory and data is subject to change. | 3 | 2 | 2 | 2 |

---
