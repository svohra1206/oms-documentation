# **Check Cart Inventory API**

Checks the same day delivery eligibility for the items in the cart within specified distance parameters (ex. Zip Code) . To check inventory of items in the cart, you will need to call the API endpoint with the `/POST` method.

## **Request**

### End Point

`https://\<oms\>/api/checkCartInventory`

Example: https://demo-oms.hotwax.io/api/checkCartInventory

## Header

Content-Type:​ application/json

**Body**
```
{
  point: "\<latlon\>",
  distance: "sameDayStoreSearchProximity",
  shopifyShopId: "shopId",
  items: "cartItems",
  filters: ["\<filter1\>", "\<filter2\>"]
}
```

Example
```
{
  point: 35.833740, -78.874300
  distance: 12,
  shopifyShopId: 3256789987,
  items:
{
  "variantId": "42088603123903",
  "quantity": 1
},
  filters:[
  "sameday\_pref: true"]
} 
```

**Parameters** | **Description** | **Required (Y/N)** 
| --- | --- | --- |
| `point` | The latitude and longitude of the customer | Y |
| `distance` | The specified distance from the zipcode, within which the API should locate shopify store | Y |
| `item` | Variant Identifications with their required quantity | Y |
| `filters` | The filters used to refine search | N |

## **Response**

### Status Code

HTTP/1.1 200 OK

## **Headers**

Content-Type: application/json

**Body**

``` 
{
"facilityId": "646", 
"distance": 15, 
"cors.request.origin": "[https://originalpenguin-dev.myshopify.com](https://originalpenguin-dev.myshopify.com/)",
"shopifyShopId": "10224533555",
"filters":[
"sameday\_pref: true",
"docType: STORE",
"shopifyShop\_id:10224533555"
],
"point": "25.786909, -80.361253",
"cors.request.type": "actual",
"items": [
{
"quantity": 1,
"variantId": "42088603123903",
"availableQty": 1,
"status": "available"
}
],
"facility":
{
"docType": "STORE",
"storeCode": "646",
"identifier": "646",
"storeType": "RETAIL\_STORE",
"storeName": "Dolphin Mall",
"externalId": "646",
"primaryFacilityGroupId": "10224533555",
"primaryFacilityGroupName": "OP\_Group",
"primaryShopifyShopId": "10224533555",
"10224533555\_pref": "true",
"fac\_grp\_pref": "true",
"sameday\_pref": "true",
"address1": "11401 NW 12th Street",
"city": "Miami",
"postalCode": "33172",
"country": "United States",
"countryCode": "US",
"state": "Florida",
"stateCode": "FL",
"latlon": "25.7875845,-80.3805674",
"shopifyShop\_id": ["10224533555"],
"shopifyShops": [
"[{\"domain\":\"[originalpenguin-dev.myshopify.com](http://originalpenguin-dev.myshopify.com/)\",
\"name\":\"originalpenguin-dev\",\"myshopifyDomain\":\"[originalpenguin-dev.myshopify.com](http://originalpenguin-dev.myshopify.com/)\",
\"shopifyShopId\":\"10224533555\",\"shopId\":\"OP\_SHOP\"}]" ],
"productStore\_id": ["OP\_STORE"],
"productStores": [
"[{\"storeName\":\"Original Penguin\",\"productStoreId\":\"OP\_STORE\"}]" ],
"monday\_open": "10:00:00",
"monday\_close": "21:00:00",
"tuesday\_open": "10:00:00",
"tuesday\_close": "21:00:00",
"wednesday\_open": "10:00:00",
"wednesday\_close": "21:00:00",
"thursday\_open": "10:00:00",
"thursday\_close": "21:00:00",
"friday\_open": "10:00:00",
"friday\_close": "21:00:00",
"saturday\_open": "10:00:00",
"saturday\_close": "21:00:00",
"sunday\_open": "11:00:00",
"sunday\_close": "20:00:00",
"updatedDatetime": "2023-06-15T13:41:09.708Z",
"docType-identifier": "STORE-646",
"_version_": 1768776238064730000,
"dist": 1.9352518 }} |
```

**##Case 2 -** When Same day delivery is unavailable at the selected store
```
{
  "facilityId": "\<facilityId\>",
  "distance": 15,
  "shopifyShopId": "\<shopId\>",
  "filters": ["sameday\_pref: true",
  "docType: STORE",
  "shopifyShop\_id: \<shopId\>"],
  "point": "\<latlon\>",
  "items": [
{
  "variantId": "42088603123903",
  "quantity": 1,
  "available\_qty": 0,
  "status": "unavailable"
}
],
"facility": \<facilityInformation\>
}

```
**Params**

| **Parameters** | **Description** |
| --- | --- |
| `facilityId` | The unique identification of the facility from where the products will be delivered. |
| `distance` | The distance parameter defined by retailers for same day delivery service. |
| `shopifyShopId` | The ID of the virtual Shopify store where the customer is operating. |
| `docType` | Reference index |
| `filters` | The filters used to refine search |
| `point` | The latitude and longitude of the store location |
| `items` | The items requested to check same day eligibility |
| `quantity` | The quantity of the items in the cart |
| `variantId` | The product ID of the specific variant selected by the customer |
| `availableQty` | The quantity available at store |
| `status` | The item availability status |
| `facility` | The facility details |
| `storeCode` | The Shopify store code |
| `identifier` | DocType-Identifier |
| `storeType` | The store type, ex: Retail or Outlet Stores |
| `storeName` | The registered name of the Shopify Store |
| `externalId` | The Id of the store in the external reference source |
| `primaryFacilityGroupId` | The Id of the primary facility group |
| `primaryFacilityGroupName` | The name of the primary facility group |
| `primaryShopifyShopId` | The Id of the primary Shopify Shop |
| `sameday\_pref` | The preference selected for same day delivery |
| `address1` | The address of the store |
| `city` | City |
| `postalCode` | Postal Code |
| `country` | Country |
| `countryCode` | Country Code |
| `state` | State |
| `stateCode` | State Code |
| `latlon` | The latitude and longitude of the facility |
| `shopifyShops` | The associated Shopify shops with the facility |
| `productStore\_id` | The product store Id to which facility is associated |
| `productStores` | The details of the store where facility is associated |
| `\<weekday\>\_open` | The opening time of the store on the day of a week |
| `\<weekday\>\_close` | The closing time of the store on the day of a week |
| `updatedDatetime` | The date time when opening and closing hours data was updated |

## **Error Handling**

In case we have any error "\__ERROR\_MESSAGE\_"_ field in the response indicates the details.
