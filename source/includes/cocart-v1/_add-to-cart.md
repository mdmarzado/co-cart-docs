## Add Item to Cart ##

<img src="images/github.svg" width="20" height="20" alt="GitHub Mark Logo"> [Edit on GitHub](https://github.com/co-cart/co-cart-docs/blob/master/source/includes/cocart-v1/_add-to-cart.md)

This API helps you to add an item to the cart. You can also request to return the whole cart once item is added to reduce API requests and use the [Get Cart Content](#cart-get-cart-contents) properties.

### Properties ###

| Property         | Type    | Description                                                                                                 |
| ---------------- | ------- | ----------------------------------------------------------------------------------------------------------- |
| `cart_key`       | string  | Unique identifier for the cart. <i class="label label-info">optional</i>                                    |
| `product_id`     | integer | The product ID is required in order to add a product to the cart. <i class="label label-info">mandatory</i> |
| `quantity`       | float   | Set the quantity of the product you want to add to the cart. <i class="label label-info">Default is 1</i>   |
| `variation_id`   | integer | Used to set the variation of the product being added to the cart. <i class="label label-info">optional</i>  |
| `variation`      | array   | Attribute values.                                                 <i class="label label-info">optional</i>  |
| `cart_item_data` | array   | Used to apply extra cart item data we want to pass with the item. <i class="label label-info">optional</i>  |
| `return_cart`    | bool    | Set as true to return the cart once item added. <i class="label label-info">optional</i>                    |

### HTTP request ###

<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-post">POST</i>
    <h6>/wp-json/cocart/v1/add-item</h6>
  </div>
</div>

```shell
curl -X POST https://example.com/wp-json/cocart/v1/add-item \
  -H "Content-Type: application/json" \
  -d '{
    "product_id": 32,
    "quantity": 1
  }'
```

```javascript--jquery
var settings = {
  "url": "https://example.com/wp-json/cocart/v1/add-item",
  "method": "POST",
  "data": {
    "product_id" : 32,
    "quantity" : 1
  }
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

```php
<?php
$curl = curl_init();

$args = array(
  'product_id' => 32,
  'quantity' => 1
);

curl_setopt_array( $curl, array(
  CURLOPT_URL => "https://example.com/wp-json/cocart/v1/add-item",
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => $args,
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTPHEADER => array(
    'Accept: application/json',
    'Content-Type: application/json',
    'User-Agent: CoCart API/v1',
  )
) );

$response = curl_exec($curl);

curl_close($curl);

echo $response;
```

```php--wp-http-api
<?php
$args = array(
  'headers' => array(
    'Content-Type' => 'application/json; charset=utf-8',
  ),
  'body' => wp_json_encode( [
    'product_id' => 32,
    'quantity' => 1
  ] ),
  'timeout' => 30
);

$response = wp_remote_post( 'https://example.com/wp-json/cocart/v1/add-item', $args );
$body = wp_remote_retrieve_body( $response );
```

> JSON response example

```json
{
  "404dcc91b2aeaa7caa47487d1483e48a":{
    "key":"404dcc91b2aeaa7caa47487d1483e48a",
    "product_id":32,
    "variation_id":0,
    "variation":[],
    "quantity":1,
    "line_tax_data":{
      "subtotal":[],
      "total":[]
    },
    "line_subtotal":18,
    "line_subtotal_tax":0,
    "line_total":18,
    "line_tax":0,
    "data":{}
  }
}
```

## Add Variation Item to Cart ##

Adding a variation of a product to the cart is easy. All you need is to identify the attributes and which attribute your customer has selected.

While the `variation_id` is important, it is not required to be know as the API will look it up for you based on the attributes passed. Without the attributes of the variation, there is no way to identify the variation added.

### What are attributes? ###

Attributes are what identify a variation of a variable product from the colour of a t-shirt to the size.

Attributes can be managed in two ways. Globally or via the product if they are custom. It's important to know what attributes are used for the variation of the product.

All attributes start with a prefix `attribute_`. A global attribute extends the prefix like so `attribute_pa_`, while a custom attribute just has the prefix `attribute_`. Both are followed by the attribute slug. See the examples for comparison.

<aside class="notice">
  If any of your attributes are set for "Any" in the backend, your customer will still be required to select the attribute in order to add the variation to the cart.
</aside>

<aside class="warning">
  You can not add a simple product with attributes like a variation! If you wish to pass attribute data for a simple product, use the `cart_item_data` parameter instead.
</aside>

```shell
curl -X POST https://example.com/wp-json/cocart/v1/add-item \
  -H "Content-Type: application/json" \
  -d '{
    "product_id": 1723,
    "quantity": 1,
    "variation_id": 1820,
    "variation": {
      "attribute_colours": "Red",
      "attribute_pa_size": "2x-large"
    }
  }'
```

```javascript--jquery
var settings = {
  "url": "https://example.com/wp-json/cocart/v1/add-item",
  "method": "POST",
  "data": {
    "product_id": 1722,
    "quantity": 1,
    "variation_id": 1820,
    "variation": {
      "attribute_colours": "Red",
      "attribute_pa_size": "2x-large"
    }
  }
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

```php
<?php
$curl = curl_init();

$args = array(
  'product_id' => 1722,
  'quantity' => 1,
  'variation_id' => 1820,
  'variation' => {
    'attribute_colours': 'Red',
    'attribute_pa_size': '2x-large'
  }
);

curl_setopt_array( $curl, array(
  CURLOPT_URL => "https://example.com/wp-json/cocart/v1/add-item",
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => $args,
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTPHEADER => array(
    'Accept: application/json',
    'Content-Type: application/json',
    'User-Agent: CoCart API/v1',
  )
) );

$response = curl_exec($curl);

curl_close($curl);

echo $response;
```

```php--wp-http-api
<?php
$args = array(
  'headers' => array(
    'Content-Type' => 'application/json; charset=utf-8',
  ),
  'body' => wp_json_encode( [
    'product_id' => 1722,
    'quantity' => 1
    'variation_id' => 1820,
    'variation' => {
      'attribute_colours': 'Red',
      'attribute_pa_size': '2x-large'
    }
  ] ),
  'timeout' => 30
);

$response = wp_remote_post( 'https://example.com/wp-json/cocart/v1/add-item', $args );
$body = wp_remote_retrieve_body( $response );
```

> JSON response example

```json
{
    "key": "2c698d686c6cd8872e825fd9b05bd322",
    "product_id": 1722,
    "variation_id": 1820,
    "variation": {
        "attribute_colours": "Red",
        "attribute_pa_size": "2x-large"
    },
    "quantity": 1,
    "data": {},
    "data_hash": "89f41c195ac99955ca64fafcc1225796",
    "line_tax_data": {
        "subtotal": [],
        "total": []
    },
    "line_subtotal": 12,
    "line_subtotal_tax": 0,
    "line_total": 12,
    "line_tax": 0,
    "product_name": "T-shirt - Red",
    "product_title": "T-shirt",
    "product_price": "£12.00"
}
```

## Add Item to Cart + Custom Data ##

Need to pass custom data? This example will show you how.

```shell
curl -X POST https://example.com/wp-json/cocart/v1/add-item \
  -H "Content-Type: application/json" \
  -d '{
    "product_id": 3008,
    "quantity": 1,
    "cart_item_data": {
      "engraved_name": "Sébastien Dumont",
      "engraved_size": "Medium"
    }
  }'
```

```javascript--jquery
var settings = {
  "url": "https://example.com/wp-json/cocart/v1/add-item",
  "method": "POST",
  "data": {
    "product_id" : 3008,
    "quantity" : 1,
    "cart_item_data" : {
      "engraved_name" : "Sébastien Dumont",
      "engraved_size" : "Medium"
    }
  }
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

```php
<?php
$curl = curl_init();

$args = array(
  'product_id' => 3008,
  'quantity' => 1,
  'cart_item_data' => array(
    'engraved_name' => 'Sébastien Dumont',
    'engraved_size' => 'Medium'
  )
);

curl_setopt_array( $curl, array(
  CURLOPT_URL => "https://example.com/wp-json/cocart/v1/add-item",
  CURLOPT_CUSTOMREQUEST => "POST",
  CURLOPT_POSTFIELDS => $args,
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTPHEADER => array(
    'Accept: application/json',
    'Content-Type: application/json',
    'User-Agent: CoCart API/v1',
  )
) );

$response = curl_exec($curl);

curl_close($curl);

echo $response;
```

```php--wp-http-api
<?php
$args = array(
  'headers' => array(
    'Content-Type' => 'application/json; charset=utf-8',
  ),
  'body' => wp_json_encode( [
    'product_id' => 3008,
    'quantity' => 1
    'cart_item_data' => array(
      'engraved_name' => 'Sébastien Dumont',
      'engraved_size' => 'Medium'
    )
  ] ),
  'timeout' => 30
);
$response = wp_remote_post( 'https://example.com/wp-json/cocart/v1/add-item', $args );
$body = wp_remote_retrieve_body( $response );
```

> JSON response example

```json
{
    "engraved_name": "Sébastien Dumont",
    "engraved_size": "Medium",
    "key": "b440b5368da5b3e3a6eb1f40fa666279",
    "product_id": 3008,
    "variation_id": 0,
    "variation": [],
    "quantity": 1,
    "data": {},
    "data_hash": "b5c1d5ca8bae6d4896cf1807cdf763f0",
    "line_tax_data": {
        "subtotal": {
            "13": 8.4
        },
        "total": {
            "13": 8.4
        }
    },
    "line_subtotal": 42,
    "line_subtotal_tax": 8.4,
    "line_total": 42,
    "line_tax": 8.4,
    "product_name": "Silver Ring",
    "product_title": "Silver Ring",
    "product_price": "£80.00"
}
```
