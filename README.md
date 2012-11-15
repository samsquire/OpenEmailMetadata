# OpenEmailMetadata
=================

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


If you're a business and wonder why you should adopt Open Email Metadata:

 * give your customers more value with your emails
 * send emails that customers are more likely to engage with
 * add uniqueness and added value to your services at little effort on your part
 * send bills by emails
 * send your updated Terms of Service



# Standards
===

Open Email Metadata is conceptually simple. When you create an email with your service, you append an attachment that conforms to one of the OEM standards. This ensures that any receipients will be able to interpret the data and act upon it.

### OEM-1

 * Metadata is attached as a MIME attachment.
 * The metadata MUST be attached as application/json

OEM-2: Invoices

```
	{
	 unit: "GBP",
	 items: [
			 {name: "Widget", quantity: 3, price: 30 }
	          name: "First Class Delivery", quantity: 1, price: 5, }
	        ],
	 total: 300
	}
```

OEM-3: Deliveries



```
	{
		expected: ["23/12/2012", "24/12/2012"]
	
	}
```
 
 

