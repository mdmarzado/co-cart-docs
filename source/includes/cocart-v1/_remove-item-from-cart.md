## Remove Item from Cart ##

<img src="images/github.svg" width="20" height="20" alt="GitHub Mark Logo"> [Edit on GitHub](https://github.com/co-cart/co-cart-docs/blob/master/source/includes/cocart-v1/_remove-item-from-cart.md)

This API helps you to remove an item from the cart. You can also request to return the whole cart once item is removed to reduce API requests and use the [Get Cart Content](#cart-get-cart-contents) properties.

### Properties ###

| Property        | Type   | Description                                                                                         |
| --------------- | ------ | --------------------------------------------------------------------------------------------------- |
| `cart_key`      | string | Unique identifier for the cart. <i class="label label-info">optional</i>                            |
| `cart_item_key` | string | The cart item key of the product in the cart. <i class="label label-info">mandatory</i>             |
| `return_cart`   | bool   | Set as true to return the whole cart once item is removed. <i class="label label-info">optional</i> |

### HTTP request ###

<div class="api-endpoint">
  <div class="endpoint-data">
    <i class="label label-delete">DELETE</i>
    <h6>/wp-json/cocart/v1/item</h6>
  </div>
</div>

```shell
curl -X DELETE https://example.com/wp-json/cocart/v1/item \
  -H "Content-Type: application/json" \
  -d '{
    "cart_item_key": 404dcc91b2aeaa7caa47487d1483e48a
  }'
```

```javascript--jquery
var settings = {
  "url": "https://example.com/wp-json/cocart/v1/item",
  "method": "DELETE",
  "data": {
    "cart_item_key" : "404dcc91b2aeaa7caa47487d1483e48a"
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
  'cart_item_key' => '404dcc91b2aeaa7caa47487d1483e48a'
);

curl_setopt_array( $curl, array(
  CURLOPT_URL => "https://example.com/wp-json/cocart/v1/item",
  CURLOPT_CUSTOMREQUEST => "DELETE",
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
    'cart_item_key' => '404dcc91b2aeaa7caa47487d1483e48a'
  ] ),
  'method' => 'DELETE',
  'timeout' => 30
);

$response = wp_remote_request( 'https://example.com/wp-json/cocart/v1/item', $args );
$body = wp_remote_retrieve_body( $response );
```

> JSON response example

```json
"Item has been removed from cart."
```
