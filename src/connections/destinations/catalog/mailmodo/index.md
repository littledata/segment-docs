---
title: Mailmodo Destination
rewrite: true
id: 623a07123d307e60f268a1c2
---

[Mailmodo](https://www.mailmodo.com/) is a powerful email marketing tool focused on bringing the interactive experience via AMP framework to emails. It allows businesses to create emails with web page-like interactivity right inside the user inbox, thereby increasing engagement and conversions multi-fold.


This destination is maintained by Mailmodo. For any issues with the destination, [contact the Mailmodo Support team](mailto:help@mailmodo.com).


## Getting Started

{% include content/connection-modes.md %}

1. From the Destinations catalog page in the Segment App, click **Add Destination**.
2. Search for "Mailmodo" in the Destinations Catalog, and select the "Mailmodo" destination.
3. Choose which Source should send data to the "Mailmodo" destination.
4. Go to the [Mailmodo Dashboard](https://manage.mailmodo.com/app/dashboard), navigate to **Settings > API Keys**, then create a new API Key and copy the same.
5. Enter the "API Key" in the "Mailmodo" destination settings in Segment.


## Supported methods

Mailmodo supports the following methods, as specified in the [Segment Spec](/docs/connections/spec).

### Identify

If you aren’t familiar with the Segment Spec, take a look at the [Identify method documentation](/docs/connections/spec/identify) to learn about what it does.

```js
analytics.identify('userId12345', {
  firstName: 'Bob',
  lastName: 'Dole',
  email: 'bob.dole@example.com',
  company: 'Initech',
  employees: 234
});
```

Every time you call identify with an email address included, we will:
1.	First ask Mailmodo if the email exists.
2.	If the email doesn’t exist, then we will add the user as a Contact to the Mailmodo database and match user properties with the Segment `traits` sent in identify call payload.
3.	If the email exists, then we will update the user properties for the Contact against the Segment `traits` sent in identify call payload.

All the [special traits](https://segment.com/docs/connections/spec/identify#traits) recognized by Segment will be translated and matched with the Mailmodo user properties for a Contact. These fields will be automatically created or mapped for a Contact in Mailmodo and will be available for personalization and advance segmentation.

==Please note==
==1. The email field is required. Identify calls without an email is dropped.==
==2. If different email addresses are sent against same user id in identify call, then they are treated as two different contacts in Mailmodo.==

### Track
If you aren’t familiar with the Segment Spec, take a look at the [Track method documentation](/docs/connections/spec/track) to learn about what it does. An example call would look like:

```js
analytics.track('Product Viewed', {
  product_id: '507f1f77bcf86cd799439011',
  name: 'Monopoly: 3rd Edition',
  price: 18.99,
  url: 'https://www.example.com/product/path',
  image_url: 'https://www.example.com/product/path.jpg'
});
```
Segment sends `Track` calls to Mailmodo as a Custom Event. When you call  track, we’ll send the event to Mailmodo with the event name and all properties that you specified.

Be sure you send an Identify call for any user who will trigger Track calls. If Mailmodo receives a Track call for an unknown userId, the call is dropped.