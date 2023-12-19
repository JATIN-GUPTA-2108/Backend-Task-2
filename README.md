
**Authentication API's**

1.) <i>Register API: http://localhost:3000/api/auth/register</i>  (POST)

    request-body: Pass a JSON object with user's name,username,password and userType.

    Example: 
    {
      "name":"TestBuyer",
      "username": "testBuyer@email.com",
      "password":"9876543210",
      "userType":"buyer"
    }

2.) <i>Login API: http://localhost:3000/api/auth/login</i>  (POST)

  Request-Body Example:
  ```json
  {
    "username":"testBuyer@email.com",
    "password":"9876543210",
    "userType":"buyer"
  }
```

3.) <i>Logout API: http://localhost:3000/api/auth/logout </i> (GET)   , Pass header- Authorization: Bearer JWT-Token



**Buyers API's**

1.)<i> Get a list of all sellers:  </i> (GET)  ,Pass header- Authorization: Bearer JWT-Token
API: http://localhost:3000/api/buyer/list-of-sellers 

Sample Response Data:

```json

{
   "message": "List of available sellers!",
   "status": "success",
   "data": {
      "sellers": [
         {
            "_id": "657b039d4bab09f0b13bc524",
            "name": "Seller-1",
            "email": "seller1@email.com",
            "__v": 0,
            "userType": "seller"
         },
         {
            "_id": "657b03a54bab09f0b13bc527",
            "name": "Seller-2",
            "email": "seller2@email.com",
            "__v": 0,
            "userType": "seller"
         }
      ]
   }
}

```

Pass the any _id of a seller, received from the above list of seller data


2.) <i>Get the catalog of a seller by seller_id: </i>

API: http://localhost:3000/api/buyer/seller-catalog/657b03a54bab09f0b13bc527   (GET)  ,Pass header- Authorization: Bearer JWT-Token

Sample Response Body:
```json
{
  "message": "List of available sellers!",
  "status": "success",
  "data": {
    "sellerData": {
      "seller": {
        "_id": "657b039d4bab09f0b13bc524",
        "name": "Seller-1",
        "__v": 0,
        "userType": "seller"
      },
      "catalog": [
        {
          "name": "Product-1",
          "price": "Rs.170",
          "_id": "657b1410dab7ef6776dacd85"
        },
        {
          "name": "Product-2",
          "price": "Rs.180",
          "_id": "657b1410dab7ef6776dacd86"
        },
        {
          "name": "Product-3",
          "price": "Rs.120",
          "_id": "657b1410dab7ef6776dacd87"
        },
        {
          "name": "Product-4",
          "price": "Rs.250",
          "_id": "657b1410dab7ef6776dacd88"
        },
        {
          "name": "Product-5",
          "price": "Rs.90",
          "_id": "657b1410dab7ef6776dacd89"
        }
      ]
    }
  }
}
```

3.) <i>Send a list of items to create an order for seller with id = seller_id </i>

API: http://localhost:3000/api/buyer/create-order/657b039d4bab09f0b13bc524  (POST)  ,Pass header- Authorization: Bearer JWT-Token

Sample Request Body: Send array of objects, with each object having the product name and price.
```json
{
  "orderData":[
    {
      "name":"Product-1",
      "price":"Rs.170"
    },
    {
      "name":"Product-2",
      "price":"Rs.180"
    },
    {
      "name":"Product-2",
      "price":"Rs.130"
    }
  ]
}
```

**Seller API's**

1.) <i>Send a list of items to create a catalog for a seller</i> 

API: http://localhost:3000/api/seller/create-catalog/  (POST)  ,Pass header- Authorization: Bearer JWT-Token

Sample Request Body: An array of product objects, with name and price of the product
```json
{
  "products":[
    {
      "name":"Product-1",
      "price": "Rs.170"
    },
    {
      "name":"Product-2",
      "price": "Rs.180"
    },
    {
      "name":"Product-3",
      "price": "Rs.120"
    },
    {
      "name":"Product-4",
      "price": "Rs.250"
    },
    {
      "name":"Product-5",
      "price": "Rs.90"
    }
  ]
}
```

2.) <i>Retrieve the list of orders received by a seller </i>

API: http://localhost:3000/api/seller/orders/   (GET)  ,Pass header- Authorization: Bearer JWT-Token

Sample Response Body:
```json
{
  "message": "Customer Orders",
  "status": "success",
  "data": {
    "orders": {
      "_id": "657b039d4bab09f0b13bc524",
      "orders": [
        {
          "buyer": "657b03cf16faa550e20697b4",
          "products": [
            {
              "name": "Product-1",
              "price": "Rs.170",
              "_id": "657b233a268d6d94ea49fd3a"
            },
            {
              "name": "Product-2",
              "price": "Rs.180",
              "_id": "657b233a268d6d94ea49fd3b"
            },
            {
              "name": "Product-2",
              "price": "Rs.130",
              "_id": "657b233a268d6d94ea49fd3c"
            }
          ],
          "_id": "657b233a268d6d94ea49fd39"
        }
      ]
    }
  }
}
```

