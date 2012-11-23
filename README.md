# OpenEmailMetadata
=================

**Note**: Currently Open Email Metadata is explorative and has no existing implementations.

Send your emails with attached metadata so recipients can create complex behaviours such as displaying notifications, integration and search. Let's make email semantic!

# Examples
===

These are some things that are very possible if Open Email Metadata is adopted today:

 * get notified of when a product will be delivered and when it is dispatched
 * get cross platform desktop and mobile notifications, tailored to whatever device you are on
 * take back control over your notifications
 * subscribe and unsubscribe to email newsletters from one interface
 * set up complex rules to react to different situations
 * get notified when someone replies to your forum or blog posts
 * receive notifications of what you bought, how much it cost
 * […and much more!](#moreexamples)

If you operate a service, why should you use OEM?

 * make your emails more useful - your emails will be useable in ways you never imagined
 * you will automatically support any new services and applications that spring up from supporting a given OEMS.
 * send emails that customers are more likely to engage with
 * add uniqueness and added value to your services at little effort on your part
 * send bills, updates to your ToS by emails


# OEM Metadata 0.1
===

Open Email Metadata is conceptually simple. When you create an email with your service, you append one or more attachments that conforms with the following OpenEmailMetadata standards. This ensures that any receipients will be able to interpret the data and act upon it.


 1. Metadata is attached as a MIME attachment
 2. The metadata MUST be attached as application/json.

# OEMFormats
===

The following are some early metadata formats. OEM does not define how the following formats be used - it is completely up to the consumer to decide.

### OEM-2: Itemised Receipt

This is a very basic itemised receipt that assumes a fixed currency and tax included per-item.

Considerations:
 * tax
 * item description



```
	{
	 currency: "GBP", /* iso4217 code */
	 items: [
			 {name: "Widget", quantity: 2, price: 100 },
			 {name: "Foo", quantity: 2, price: 50 },
	         {name: "First Class Delivery", quantity: 1, price: 8 }
	        ],
	 total: 308
	}
```



### OEM-3: Expected Delivery Date

 * Specify an expected delivery date in `dateFormat` format.


```
	{
		expected: {
			date: ["23/12/2012", "24/12/2012"]
		}
	
	}
```


### OEM-4: Delivery Dispatched
 
  * Specify a dispatch date in `dateFormat` format:
 
 ```
	{
		dispatched: {
			date: ["23/12/2012", "24/12/2012"]
		}
	
	}
```
 
### OEM-5: Terms of Service Update

 * Specify the date the terms of service has been updated.

```
	termsOfService: {
		updated: "15/11/2012",
		needsAccepting: true,
		url: "http://website.oem/terms"
	}
	
```

### OEM-6: Reply

 * Notification that you have received a reply.


```
	reply: {
		name: "",
		url: "",
		replee: ""
	}
```

### OEM-7: Bill

 * Receive a bill.

```
	bill: {
		amount:  300,
		currency: "GBP",
		status: "paid"
	}
```


### OEM-8: Invitation

```
	// todo
```

### OEM-9: Confirmation Subscription

```
	// todo
```

# Semantic Open Email Metadata
===

In the above examples, there is no links between metadata where it would be beneficial for there to be. It is undecided how this could be implemented. There are no standard mechanisms in JSON that support identifiers. There are a number of opportunities available:

 * Require producers of metadata give a unique identifier (IRI)
 * Use a known attempt at linking JSON metadata [HAL](http://stateless.co/hal_specification.html), [JSON-LD](http://json-ld.org/), [JSON Reference](http://tools.ietf.org/html/draft-pbryan-zyp-json-ref-00)

### Unanswered Questions
 
 * What if a user has not received an email with an existing ID?
 * Forces a client to keep a record of previous metdata. No longer idempotent.
 * Would they be able to re-fetch it?


# Considerations
===
 
There are hopes to support `application/xml` and `application/x-www-form-urlencoded` but this will have to wait until there is an obvious way to serialiser metadata to all three formats that is not serialiser dependent. For example, there are multiple ways to encode arrays in `application/x-www-form-urlencoded` and conversions between XML and JSON.

# Creating Implementations
===

You are completely free to use the established formats above in any way you can imagine but you'll need a way to read the above data.

 * node.js: Use [emailjs](https://github.com/eleith/emailjs) to send emails. Use [node-imap](https://github.com/mscdex/node-imap) and [mailparser](https://github.com/andris9/mailparser) to fetch and read emails.
 * php: Use [swiftmailer](http://swiftmailer.org/docs/messages.html) to send OEM. [Horde IMAP](http://wiki.horde.org/Project/HordeImapLib) to read.

# ClientsideFramework
===

The clientside framework is a standard application that runs on a user's machine and handles. This application is extensible and decides what to do with the OEM that is received. This is effectively [`mailcap`](http://en.wikipedia.org/wiki/Mailcap) for OEM.

 * Could be hosted in an email client. (_Too client dependent._)
 * Could run as a separate process with a standard API.
  * Could be web based to take advantage of the web ecosystem. (_Do people want to run a complete web stack?_)
 * A very basic `registry` for each OEM that fires a program up that handles it.
 * Some features make sense in the email client and others in a separate process.
 * Plugins and programs are written to interpret the OEM in different ways. See the examples list.
  * Some applications might want to send your OEM to third party services, such as a recommendation website that collects your preferences over time. Users decide who to send OEM to.
 
# [Examples](id:moreexamples)
=== 

What possibilities might OEM give rise to?

## Accounting Software

Whenever you receive a bill, your accounting software adds the item to your records.

## Game Matching Software

Game lobby software that uses your email identity to set up planned online games.

## Shopping Software

Your shopping software lets you track all your purchases from different companies from one place and lets you know when everything will arrive.

## Social Networking

Use multiple social networks from the same interface.

## Customer & Vendor Relationship Management

## Recommendation Engine

See all your recommendations from different vendors in one place.

## SPARQL Querying of Email

Ask your email more meaningful questions.
