# HoneyComb set up guide
This guide will walk you through how to set up a basic usage of HoneyComb SDK Script to track Affiliate Transactions.

## Installation

Replace {SDK URL} with the URL you receive. Then paste this snippet into your `<body>` tag. Ensure this runs on all pages.

    <!-- Load JavaScript SDK -->
    <script src="{SDK URL}"></script>
    <script>
      // Initialize Script
      window.honeycombAffiliate.initializeSDK();
    </script>
This snippet will initialize the HoneyComb SDK and track and manage Affiliate info.

## Event Tracking (Funnel)

HoneyComb provides functionality to help you collect insights of users brought to you by each Affiliator. You can find how to track individual event below.

### Page view

Call the Page View function on the page where you want to track `page_view` from a user coming from an Affiliate’s URL. As a user land, this will send `page_view` event to HoneyComb system.

```javascript
// Sending "page_view" event. Similar to page view in GA4.
window.honeycombAffiliate.pageView();
```

If your website is using the SPA (Single Page Application) or similar tech stack that pages are routed on the client side, and you want to track every single page view of the users, you’ll need to execute this `pageView` function every time the route is changed.

### Add to Cart

Call this function where the `Add to Cart` action happens.

```jsx
window.honeycombAffiliate.addToCart(**items**);
```

Where `items` is **an array of an item object** with a structure like this. All fields are required.

| Key | type | Description |
| --- | --- | --- |
| name | string | Product name |
| quantity | number | Quantity of the product added to the cart by that action. In most case it can be 1. |
| sku | string | Product SKU (can be empty) |
| price | number | Product price (each) in Thai baht. Support up to 2 decimal points. eg: 1234.50 |

For example, if you have a function that handles an Add to Cart button, you can execute the addToCart function along with it.

```javascript
// Your website add to cart function
function addToCart(product) {
  // Do your process 
  ...
  // End of your process
  // Then call the HoneyComb Affiliate script 'addToCart'
  // to send an add to cart event
  window.honeycombAffiliate.addToCart([
    {
      name: product.title,
      quantity: 1,
      sku: product.sku,
      price: poduct.price,
    },
  ]);
}
```

### Payment Success

In your payment flow, find the final page that a user will land on after payment is confirmed. On that page, place this snippet in your `<body>` tag.

```javascript
window.honeycombAffiliate.purchased({
  reference_number: '',
  total_price: 0,
  items: [],
});
```

If you have the purchase detail you can fill in the data passed into the purchased function **but it works fine with the data in the example!**

Here are the variable types for the object.
| Key | type | Description |
| --- | --- | --- |
| reference_number | string | Reference number or order id. |
| total_price | number | Total paid price in Thai Baht. Support up to 2 decimal points. eg: 1234.50 |
| items | item[] | Array of an item type similar to addToCart function. Refers to the same **Item** in the [Add to Cart section](#add-to-cart) |


## Get current tracking information
```javascript
window.honeycombAffiliate.getTracking();
```

By calling `getTracking` function. You will get all the tracking information that is applied to current session.

| Name | Type |
|--|--|
| affiliateId | string |
| expireDate | Date |
| landingUrl | string |
| sessionId | string (UUID) |
| utmContent | string |
