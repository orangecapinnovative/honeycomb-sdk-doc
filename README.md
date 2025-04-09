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

## Record a Successful Affiliate Transaction

In your payment flow, find the final page that a user will land on after payment is confirmed. On that page, place this snippet in your `<body>` tag.

    <script>
      window.honeycombAffiliate.purchased({
		reference_number: '',
		total_price: 0,
		items: [],
	  });
    </script>

If you have the purchase detail you can fill in the data passed into the purchased function **but it works fine with the data in the example!**

Here are the variable types for the object.
| Name | Type |
|--|--|
| reference_number | string |
| total_price | number |
| items | Item[] |

**Item** data type
| Name | Type |
|--|--|
| name | string |
| quantity | number |
| sku | string |
| price | number |

## Get current tracking information
    <script>
      window.honeycombAffiliate.getTracking();
    </script>

By calling `getTracking` function. You will get all the tracking information that is applied to current session.

| Name | Type |
|--|--|
| affiliateId | string |
| expireDate | Date |
| landingUrl | string |
| sessionId | string (UUID) |
| utmContent | string |
