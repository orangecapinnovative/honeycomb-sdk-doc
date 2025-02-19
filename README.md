# HoneyComb setup guide
This guide will walkthrough how to setup a basic usage of HoneyComb SDK Script to track Affiliate Transaction.

## Installation

Replace {SDK URL} with the URL you receive. Then paste this snippet into your `<body>` tag. Ensure this will get to run on all pages.

    <!-- Load JavaScript SDK -->
    <script src="{SDK URL}"></script>
    <script>
      // Initialize Script
      window.honeycombAffiliate.initializeSDK();
    </script>
This snippet will initialize the HoneyComb SDK and will track, manage Affiliate info.

## Record a Successful Affilaite Transaction

In your payment flow, find the final page that a user will land into after payment is confirmed. On that page, place this snippet in your `<body>` tag.

    <script>
      window.honeycombAffiliate.purchased({
		reference_number: '',
		total_price: 0,
		items: [],
	  });
    </script>

If you have the purchase detail you can fill in the data passed into purchased function **but it works totally fine with the data similar to the example!**

Here are the variable types for the object.
| Name | Type |
|--|--|
| reference_number | string |
| total_price | number |
| items | Item[] |

**Item** data type
| Name | Type |
|--|--|
| reference_number | string |
| name | string |
| quantity | number |
| sku | string |
| price | number |
