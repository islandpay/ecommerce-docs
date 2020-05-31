# Island Pay e-Commerce Documentation

Using the Island Pay eComm Gateway, you will be able to create and query orders as a merchant on Island Pay.

If you prefer to use Postman, the collection is also available in this repository.

* [ISLAND_PAY_ECOMM.postman_collection.json](ISLAND_PAY_ECOMM.postman_collection.json)

The testing environment uses the host `conch.islandpay.com`.
When you are finished testing and want to start working in the live environment, please change the host to `snapper.islandpay.com`.

* Testing environment: `conch.islandpay.com`
* Live environment: `snapper.islandpay.com`

## Create Order

`POST` `https://conch.islandpay.com/api/merchant/ecomm/orders`

Headers:

* `Content-Type`: `application/json`

Request Parameters (in body):

* `merchant_account_id`: your Merchant Account ID
* `device_id`: your Device ID
* `pin`: your PIN
* `amount`: order amount

Request example:

```json
{
    "merchant_account_id": "99",
    "device_id": "999999999999999",
    "pin": "9999",
    "amount": 9.99
}
```

The response object will contain:

* `code`: order code
* `status`: order status
* `amount`: order amount

Response example:

```json
{
    "code": "ed99f78e-9ed2-9922-b912-999981a0bfe0",
    "status": "pending",
    "amount": 9.99
}
```

## Get Order

`GET` `https://conch.islandpay.com/api/merchant/ecomm/orders/{{order_code}}`

Parameter (in path):

* `order_code`: received when creating an order

The response object will contain:

* `code`: order code
* `status`: order status
* `amount`: order amount

Response example:

```json
{
    "code": "ed99f78e-9ed2-9922-b912-999981a0bfe0",
    "status": "pending",
    "amount": 9.99
}
```

## Get Order QR Code

Get the a QR code for the order, this QR code can be used by the Island Pay app to pay.

`GET` `https://conch.islandpay.com/api/merchant/ecomm/qrcodeimage/{{order_code}}?size={{size}}`

Parameters (in path and query):

* `order_code`: received when creating an order
* `size` (optional): size in pixels of each square of the QR code

The response will be a string with the QR code encoded in base 64 that can be used inside an HTML `img`:

```text
data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAZoAA [...]
```
