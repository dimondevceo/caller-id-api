# Caller ID API

Enhance your software with real-time caller identification, fraud prevention, and spam protection at scale.

## Table of Contents
- [Authentication](#authentication)
- [Get User Information](#get-user-information)
- [Get Phone Number Information](#get-phone-number-information)
- [Get Phone Number Picture](#get-phone-number-picture)

## Authentication

To use the CallerAPI, include your API key in the header of each request:

```
X-Auth: YOUR_API_KEY
```

Replace `YOUR_API_KEY` with the actual API key provided in your CallerAPI dashboard.

## Get User Information

Retrieve information about the authenticated user.

**Endpoint:**
```
GET https://callerapi.com/api/me
```

**Response:**
```json
{
    "status": "success",
    "email": "john@example.com",
    "credits_spent": 23498,
    "credits_monthly": 250000,
    "credits_left": 226502
}
```

**Code Examples:**

<details>
<summary>cURL</summary>

```bash
curl -H 'X-Auth: YOUR_API_KEY' 'https://callerapi.com/api/me'
```
</details>

<details>
<summary>Python</summary>

```python
import requests

url = "https://callerapi.com/api/me"
headers = {
    "X-Auth": "YOUR_API_KEY"
}

response = requests.get(url, headers=headers)
print(response.json())
```
</details>

<details>
<summary>JavaScript</summary>

```javascript
fetch('https://callerapi.com/api/me', {
  headers: {
    'X-Auth': 'YOUR_API_KEY'
  }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```
</details>

<details>
<summary>PHP</summary>

```php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, 'https://callerapi.com/api/me');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_HTTPHEADER, array('X-Auth: YOUR_API_KEY'));

$response = curl_exec($ch);
curl_close($ch);

$data = json_decode($response, true);
print_r($data);
```
</details>

## Get Phone Number Information

Retrieve detailed information about a specific phone number.

**Endpoint:**
```
GET https://callerapi.com/api/phone/info/{phone}
```

Replace `{phone}` with the phone number you want to look up. The phone number should be in E.164 format (e.g., +18006927753).

**Response:**

The response is a JSON object containing information from various sources. Here's a breakdown of the main sections:

- `truecaller`: Information from Truecaller API
- `callapp`: Information from CallApp API
- `viewcaller`: Information from ViewCaller API
- `eyecon`: Information from EyeCon API

```json
{
  "status": "success",
  "eyecon": "Apple Inc.",
  "callapp": {
    "name": "apple inc.",
    "websites": [
      {"websiteUrl": "http://www.apple.com/"},
      {"websiteUrl": "https://www.apple.com/"},
      {"websiteUrl": "http://m.yelp.com/biz/apple-computer-headquarters-cupertino"}
    ],
    "addresses": [
      {"type": 1, "street": "Summit Boulevard, 35243, Vestavia Hills"},
      {"type": 1, "street": "320 S Capital of Texas Hwy, West Lake Hills, TX 78746, USA"}
    ],
    "photoUrl": "https://lh3.googleusercontent.com/p/AF1QipPmIDDqiF56xI9-dF3etwxfTYmlZrpKJKn_2T9r=k",
    "categories": [
      {"name": "Shopping & Retail"},
      {"name": "Computer & Equipment Dealers"}
    ],
    "avgRating": 4.599999904632568,
    "priceRange": 3,
    "description": "Apple retail store showcasing the brand's phones, tablets & more in sleekly designed spaces.",
    "openingHours": {
      "sunday": ["07:00 - 16:00"],
      "monday": ["05:00 - 20:00"],
      "tuesday": ["05:00 - 20:00"],
      "wednesday": ["05:00 - 20:00"],
      "thursday": ["05:00 - 20:00"],
      "friday": ["05:00 - 20:00"],
      "saturday": ["07:00 - 16:00"]
    },
    "facebookID": {"id": "114092991968595", "sure": true, "version": 1},
    "linkedinPubProfileUrl": {"id": "http://www.linkedin.com/pub/claudia-smith/30/565/a31", "sure": true, "version": 1},
    "twitterScreenName": {"id": "djsetroc", "sure": true, "version": 1},
    "googlePlusID": {"id": "115474023033355232032", "sure": true, "version": 1},
    "foursquareID": {"id": "12550046", "sure": true, "version": 1},
    "instagramID": {"id": "230216465", "sure": true, "version": 1},
    "pinterestID": {"id": "caseybrunetti", "sure": true, "version": 1},
    "lat": 30.30219640000001,
    "lng": -97.8296238,
    "url": "https://maps.google.com/?cid=2099657283551182410",
    "googlePlacesId": "ChIJfTemqIdKW4YRopyJNzlsVwE",
    "huaweiPlacesId": "798EC49D94E53FA0CC39A9A66E3FCA90",
    "spamScore": 343,
    "priority": 37744
  },
  "viewcaller": [
    {"name": "apple inc.", "occurrences": 9273, "isSpam": false},
    {"name": "apple", "occurrences": 609, "isSpam": false},
    {"name": "apple inc", "occurrences": 416, "isSpam": false}
  ],
  "truecaller": {
    "number": "+1 800-692-7753",
    "is_valid": true,
    "country_code": 1,
    "national_number": 8006927753,
    "number_type": 3,
    "number_type_label": "Toll free",
    "provider": "",
    "time_zones": [
      "America/Adak",
      "America/Anchorage",
      "America/Chicago"
    ]
  }
}
```

**Code Examples:**

<details>
<summary>cURL</summary>

```bash
curl -H 'X-Auth: YOUR_API_KEY' 'https://callerapi.com/api/phone/info/18006927753'
```
</details>

<details>
<summary>Python</summary>

```python
import requests

phone_number = "18006927753"
url = f"https://callerapi.com/api/phone/info/{phone_number}"
headers = {
    "X-Auth": "YOUR_API_KEY"
}
response = requests.get(url, headers=headers)
print(response.json())
```
</details>

<details>
<summary>JavaScript</summary>

```javascript
const phoneNumber = '18006927753';
fetch(`https://callerapi.com/api/phone/info/${phoneNumber}`, {
    headers: {
        'X-Auth': 'YOUR_API_KEY'
    }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```
</details>

<details>
<summary>PHP</summary>

```php
$phone_number = "18006927753";
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://callerapi.com/api/phone/info/$phone_number");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_HTTPHEADER, array('X-Auth: YOUR_API_KEY'));
$response = curl_exec($ch);
curl_close($ch);
$data = json_decode($response, true);
print_r($data);
```
</details>

## Get Phone Number Picture

Retrieve the profile picture associated with a phone number.

**Endpoint:**
```
GET https://callerapi.com/api/phone/pic/{phone}
```

Replace `{phone}` with the phone number you want to look up. The phone number should be in E.164 format (e.g., +18006927753).

**Response:**

The response is a base64-encoded image.

```
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
```

**Code Examples:**

<details>
<summary>cURL</summary>

```bash
curl -H 'X-Auth: YOUR_API_KEY' "https://callerapi.com/api/phone/pic/18006927753"
```
</details>

<details>
<summary>Python</summary>

```python
import requests

phone_number = "18006927753"
url = f"https://callerapi.com/api/phone/pic/{phone_number}"
headers = {
    "X-Auth": "YOUR_API_KEY"
}
response = requests.get(url, headers=headers)
print(response.json())
```
</details>

<details>
<summary>JavaScript</summary>

```javascript
const phoneNumber = '18006927753';
fetch(`https://callerapi.com/api/phone/pic/${phoneNumber}`, {
    headers: {
        'X-Auth': 'YOUR_API_KEY'
    }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```
</details>

<details>
<summary>PHP</summary>

```php
$phone_number = "18006927753";
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://callerapi.com/api/phone/pic/$phone_number");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_HTTPHEADER, array('X-Auth: YOUR_API_KEY'));
$response = curl_exec($ch);
curl_close($ch);
$data = json_decode($response, true);
print_r($data);
```
</details>
