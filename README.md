# Apigee-API-Mashup-Proxy
Calling a third-party service, extracting data, and adding the data to the target's API response.

## Created
- The retail-v1 API proxy
- The oauth-v1 API proxy (for generating OAuth tokens)
- The TS-Retail target server in the eval environment (used by retail-v1)
- The API products, developer, and developer app (used by retail-v1)
- The ProductsKVM key value map in the eval environment (used by retail-v1)
- The ProductsKVM key value map entries backendId and backendSecret

### Tasks

1. **Extract the latitude and longitude from backend response.**

 Proxy endpoints > default > getStoreById > ADDED Extract variable policy.

2. **The service callout calls the Google Geocoding API, passing the latitude and longitude variables to the API**
   
    Proxy endpoints > default > getStoreById > ADDED Service callout policy.
   
3. **Extract the formatted address**

   Proxy endpoints > default > getStoreById > Extract variable policy

4. **Add the address to the target response**

    Proxy endpoints > default > getStoreById > JS policy

   <img width="776" height="700" alt="image" src="https://github.com/user-attachments/assets/d89a57ee-d89d-4951-ab58-54108d49a5a4" />

**CURL to get the final response**

`curl -i -k -X GET -H "apikey:${API_KEY}" "https://eval.example.com/retail/v1/stores/benbrook"`

{
   "**address**" : "6008 Benbrook Blvd, Benbrook, TX 76126, USA",
   "affiliate" : "Walsample",
   "location" : {
      "latitude" : 32.677649,
      "longitude" : -97.465539
   },
   "name" : "Bensample",
   "phone" : "682-233-6820",
   "site_type" : "store"
}

   
   
