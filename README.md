# Salesfire Installation Instructions

## JavaScript Tag

Add the JavaScript tag to your website. Its recommended that you place it after the opening `<head>` tag. Replace {SITE_ID} with your Salesfire Site ID.

```
    <html>
    <head>
    <script async src="https://cdn.salesfire.co.uk/code/{SITE_ID}.js"></script>
    </head>
```


## Data Layer

We use a data layer to provide Salesfire with further information which is otherwise difficult to pull from the page itself.

Define the Data Layer:

```
    window.sfDataLayer = window.sfDataLayer || [];
```

You can then push information into the data layer via:

```
    window.sfDataLayer.push(layer);
```

It is common among our clients to build one layer with the neccessary information and insert it after the JavaScript tag.

```
    <html>
    <head>
    <script async src="https://cdn.salesfire.co.uk/code/{SITE_ID}.js"></script>
    <script>
    window.sfDataLayer = window.sfDataLayer || [];
    window.sfDataLayer.push({
        "ecommerce" : {
            "purchase": {
                "id": "WEB212026",
                "revenue": 95.83,
                "shipping": 0,
                "tax": 19.17,
                "currency": "GBP",
                "coupon": "",
                "city": "Stockton",
                "state": "County Durham",
                "country": "GB",
                "products":[{
                    "sku": "220165",
                    "parent_sku": "220164",
                    "name": "Zip Through Silicone Croc Hooded Sweat",
                    "variant": "Colour: GREEN, Size: XL",
                    "brand": "Lacoste Live",
                    "category": "Mens > Clothing > Hoodies",
                    "price": 95.83,
                    "quantity": 1,
                    "currency": "GBP",
                    "position": 1
                }]
            }
        }
    });
    </script>
```

### Data Layer Elements

`ecommerce.purchase` is required on the checkout completion page.

##### Base Elements

| Key       | Type      | Description                  |
| --------- |:---------:| ---------------------------- |
| ecommerce | ecommerce | Any ecommmerce information.  |
| controq   | controq   | Website queuing information. |

##### ecommerce

| Key       | Type               | Description                      | Required |
| --------- |:------------------:| -------------------------------- | -------- |
| purchase  | ecommerce.purchase | Describes a purchase.            | Yes      |
| view      | ecommerce.view     | Describes a product view.        |          |
| add       | ecommerce.add      | Describes a added to basket.     |          |
| remove    | ecommerce.remove   | Describes a removed from basket. |          |

##### ecommerce.purchase

**This is required on the checkout completion page.** We remove duplicate transactions sent up.

| Key       | Type                                | Description                                                                          | Required |
| --------- |:-----------------------------------:| ------------------------------------------------------------------------------------ | -------- |
| id        | String                              | Transaction ID.                                                                      | Yes      |
| revenue   | Float                               | Total order revenue excluding tax and shipping. Rounded to nearest 2 decimal places. | Yes      |
| tax       | Float                               | Rounded to nearest 2 decimal places.                                                 | Yes      |
| shipping  | Float                               | Rounded to nearest 2 decimal places.                                                 | Yes      |
| coupon    | String                              |                                                                                      |          |
| currency  | String                              | ISO 4217 String                                                                      | Yes      |
| affiliate | String                              |                                                                                      |          |
| city      | String                              |                                                                                      |          |
| state     | String                              |                                                                                      |          |
| country   | String                              | ISO 3166-1 Alpha-2                                                                   |          |
| products  | Array of ecommerce.purchase.product | The products purchased in the transaction.                                           | Yes      |

##### ecommerce.purchase.product

| Key        | Type               | Description            | Required |
| ---------- |:------------------:| ---------------------- | -------- |
| sku        | String             | Product sku.           | Yes      |
| parent_sku | String             | Parent product sku.    | Yes      |
| name       | String             | Product name.          | Yes      |
| variant    | String             | Product variant name.  |          |
| brand      | String             | Product brand name.    |          |
| category   | String             | Product category name. |          |
| price      | Float              | Product unit price.    | Yes      |
| quantity   | Integer            | Product quantity.      | Yes      |
| coupon     | String             | Product coupon.        |          |
| position   | Integer            | Product position.      |          |
| currency   | ISO 4217 String    | Product currency.      |          |

##### ecommerce.view

| Key        | Type               | Description                     | Required |
| ---------- |:------------------:| ------------------------------- | -------- |
| sku        | String             | Product sku.                    | Yes      |
| parent_sku | String             | Parent product sku.             | Yes      |
| name       | String             | Product name.                   | Yes      |
| variant    | String             | Product variant name.           |          |
| brand      | String             | Product brand name.             |          |
| category   | String             | Product category name.          |          |
| price      | Float              | Product unit price. (ex VAT)    | Yes      |
| currency   | ISO 4217 String    | Product currency.               | Yes      |

##### ecommerce.add

| Key        | Type               | Description            | Required |
| ---------- |:------------------:| ---------------------- | -------- |
| sku        | String             | Product sku.           | Yes      |
| parent_sku | String             | Parent product sku.    | Yes      |
| name       | String             | Product name.          | Yes      |
| variant    | String             | Product variant name.  |          |
| brand      | String             | Product brand name.    |          |
| category   | String             | Product category name. |          |
| price      | Float              | Product unit price.    | Yes      |
| quantity   | Integer            | Product quantity.      | Yes      |
| currency   | ISO 4217 String    | Product currency.      | Yes      |

##### ecommerce.remove

| Key        | Type               | Description            | Required |
| ---------- |:------------------:| ---------------------- | -------- |
| sku        | String             | Product sku.           | Yes      |
| parent_sku | String             | Parent product sku.    | Yes      |
| name       | String             | Product name.          | Yes      |
| variant    | String             | Product variant name.  |          |
| brand      | String             | Product brand name.    |          |
| category   | String             | Product category name. |          |
| price      | Float              | Product unit price.    | Yes      |
| quantity   | Integer            | Product quantity.      | Yes      |
| currency   | ISO 4217 String    | Product currency.      | Yes      |

##### controq

| Key                | Type                       | Description                                              |
| ------------------ |:--------------------------:| -------------------------------------------------------- |
| server_integration | Boolean. Defaults to false | Whether you have integrated server side Website Queuing. |
