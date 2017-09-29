# Apps REST API

The Apps object defines an external application that requires access to the API
gateway.

External apps are able to request for API access tokens for themselves or on behalf
of any user by using the [OAuth 2.0](https://tools.ietf.org/html/rfc6749) Authorization
Framework.

{% method %}

## Specification {#specification}

| Attribute                             | Description       |
| ----:                                 | :----              |
| id<br/>`alphanum` `maxlen=64`         | Unique identifier for the object. |
| entity_tag<br>`string` `maxlen=64`   | String representing the object’s entity type. |
| name<br>`string`  `maxlen=64`        | Display name of the object. |
| type<br>`enum`                       | Security classification of the app. Valid values include <ul><li>`public` - Apps that run in untrusted locations e.g. mobile apps or web browsers, with an individual end user's privileges <li>`confidential` - Apps that run in trusted locations e.g a protected server, with an individual end user's privileges<li>`service` - Apps that run in trusted locations with their owner's privileges. |
| parameters<br>`object`               | Extended attributes |
| <o>parameters.</o>homepage_url<br>`uri`     | URL that provides more information about the app |
| <o>parameters.</o>icon_url<br>`imageuri`     | URL that loads the app's icon image |
| <o>parameters.</o>redirect_uris<br>`uri` `list`  | The valid set URIs that are permitted in the `redirect_uri` parameter of the OAuth flow. Queries and fragments are excluded but may be included during the OAuth flow. |

{% common %}

#### Sample JSON
```js
{
  "id":"ndjx7rpk",
  "entity_tag":"api-apps",
  "name":"Postman Test",
  "type":"confidential",
  "client_id":"q3j48rk2-2189992826423650.api-apps.demo.formelo.com"
  "parameters":{
    "homepage_url":"https://postman.com",
    "icon_url":"https://cdn.formelo.com/xxxx/postman.jpg",
    "redirect_uris":[
      "https://www.getpostman.com/oauth2/callback"
    ]
  }
  ... // + common properties
}
```

{% endmethod %}





{% method %}

## Create an App  {#create}

Creates an [App object](.#specification)

| Argument                      | Notes      |
| ----:                         | :----              |
| name<br><r>`required`            | |
| type<br>`optional`            | Defaults to `public`. |
| <o>parameters.</o>homepage_url<br>`optional`     |  |
| <o>parameters.</o>icon_url<br>`optional`     |  |
| <o>parameters.</o>redirect_uris<br>`optional`  | At least one valid `uri` is required for `public` and `confidential` apps to function correctly. You can specify up to 20 values. |

### Returns

Returns a new App object

{% sample lang="http" %}

#### Definition
```
POST https://demo.formelo.com/api/v1/api-apps
```

#### Sample Request
```bash
$ curl https://demo.formelo.com/api/v1/api-apps \
    -H "Bearer: xxxx-xxxx-xxxx-xxxx-xxxx" \
    -d name="Yet Another Client App" \
    -d parameters.redirect_uris="https://www.getpostman.com/oauth2/callback"
```

#### Sample Response

```js
{
  "id":"b8v12ns5",
  "entity_tag":"api-apps",
  "name":"Yet Another Client App",
  "type":"public",
  "client_id":"q3j48rk2-2198794720183082.api-apps.demo.formelo.com"
  "parameters":{
    "homepage_url":null,
    "icon_url": null,
    "redirect_uris":[
      "https://www.getpostman.com/oauth2/callback"
    ]
  }
  ... // + common properties
}
```

{% endmethod %}






{% method %}
## Retrieves an App  {#retrieve}

Retrieves an [App object](.#specification)

| Argument                      | Notes      |
| ----:                         | :----              |
| id<br><r>`required`            |  Unique id of the app that needs to be retrieved|

### Returns

Upon success, it returns the requested App object, otherwise it returns an [Error](../introduction.md#errors)

{% sample lang="http" %}

#### Definition
```
GET https://demo.formelo.com/api/v1/api-apps/:id
```

#### Sample Request
```bash
$ curl https://demo.formelo.com/api/v1/api-apps/b8v12ns5.json \
    -H "Bearer: xxxx-xxxx-xxxx-xxxx-xxxx"
```

#### Sample Response
```js
{
  "id":"b8v12ns5",
  "entity_tag":"api-apps",
  "name":"Yet Another Client App",
  "type":"public",
  "client_id":"q3j48rk2-2198794720183082.api-apps.demo.formelo.com"
  "parameters":{
    "homepage_url":null,
    "icon_url": null,
    "redirect_uris":[
      "https://www.getpostman.com/oauth2/callback"
    ]
  }
  ... // + common properties
}
```

{% endmethod %}






{% method %}

## Update an App  {#update}

Updates an existing [App object](.#specification)

| Argument                      | Notes      |
| ----:                         | :----              |
| id<br><r>`required`            |  Unique id of the app that needs to be updated|
| name<br><r>`optional`            |  |
| type<br>`optional`            | |
| <o>parameters.</o>homepage_url<br>`optional`     |  |
| <o>parameters.</o>icon_url<br>`optional`     |  |
| <o>parameters.</o>redirect_uris<br>`optional`  | At least one valid `uri` is required for `public` and `confidential` apps to function correctly. You can specify up to 20 values. |

### Returns

Upon a success, it returns the updated App object. Otherwise it returns an [error](../introduction.md#errors) 

{% sample lang="http" %}

#### Definition
```
PUT https://demo.formelo.com/api/v1/api-apps/:id
```

#### Sample Request

This example updates the name and sets two origin and redirect URIss
```bash
$ curl https://demo.formelo.com/api/v1/api-apps/b8v12ns5 \
    -H "Bearer: xxxx-xxxx-xxxx-xxxx-xxxx" \
    -d name="Yet Another Client App - Renamed" \
    -d parameters.origin_uris="https://www.mywebsite.com" \
    -d parameters.origin_uris="http://localhost" \
    -d parameters.redirect_uris="https://www.mywebsite.com/oauth2/callback" \
    -d parameters.redirect_uris="http://localhost/oauth2/callback"
```

#### Sample Response

```js
{
  "id":"b8v12ns5",
  "entity_tag":"api-apps",
  "name":"Yet Another Client App - Renamed",
  "type":"public",
  "client_id":"q3j48rk2-2198794720183082.api-apps.demo.formelo.com"
  "parameters":{
    "homepage_url":null,
    "icon_url": null,
    "origin_uris":[
      "https://www.getpostman.com",
      "http://localhost"
    ],
    "redirect_uris":[
      "https://www.getpostman.com/oauth2/callback",
      "http://localhost/oauth2/callback"
    ]
  }
  ... // + common properties
}
```

{% endmethod %}







{% method %}
## Deletes an App  {#delete}

Deletes an [App object](.#specification)

| Argument                      | Notes      |
| ----:                         | :----              |
| id<br><r>`required`            |  Unique id of the app that needs to be deleted|

### Returns

If successful, it returns `true` or a `200 - OK` HTTP status code, otherwise it returns an [Error](../introduction.md#errors)

{% sample lang="http" %}

#### Definition
```
DELETE https://demo.formelo.com/api/v1/api-apps/:id
```

#### Sample Request
```bash
$ curl https://demo.formelo.com/api/v1/api-apps/b8v12ns5.json \
    -H "Bearer: xxxx-xxxx-xxxx-xxxx-xxxx" \
    -X DELETE
```

#### Sample Response
```bash
HTTP/1.1 200 OK
```

{% endmethod %}







{% method %}
## Rollover the cryptographic keys  {#rollover}

Rolls over the cryptographic keys of a [Realm object](.#specification)

| Argument                      | Notes      |
| ----:                         | :----              |
| id<br><r>`required`           |  Unique id of the realm |
| action<br><r>`required`       | Must be set to `rollover` |
| use<br><r>`required`       | Indicates the type of key that should be rolled over. Valid values include<ul><li>`signature` - applies the operation to the signature key<li>`encryption` - applies the operation to the encryption key |
| alg<br>`optional`       | Indicates the cryptographic algorithm that new key will use.<br><br>Valid values for `signature` key rollovers include<ul><li><code>HS256</code> - HMAC using SHA-256<li><code>HS384</code> - HMAC using SHA-384<li><code>HS512</code> - HMAC using SHA-512<li><code>RS256</code> - RSASSA-PKCS-v1_5 using SHA-256.<li><code>RS384</code> - RSASSA-PKCS-v1_5 using SHA-384<li><code>RS512</code> - RSASSA-PKCS-v1_5 using SHA-512<li><code>ES256</code> - ECDSA using P-256 curve and SHA-256 hash algorithm<li><code>ES384</code> - ECDSA using P-384 curve and SHA-384 hash algorithm<li><code>ES512</code> - ECDSA using P-521 curve and SHA-512 hash algorithm</ul>The default `signature` algorithm is `RS256`<br><br>Valid values for `encryption` key rollovers include<ul><li><code>RSA-OAEP-256</code> - RSAES using Optimal Asymmetric Encryption Padding (OAEP) (RFC 3447), with the SHA-256 hash function and the MGF1 with SHA-256 mask generation function.<li><code>A128KW</code> - Advanced Encryption Standard (AES) Key Wrap Algorithm (RFC 3394) using 128 bit keys.<li><code>A192KW</code> - Advanced Encryption Standard (AES) Key Wrap Algorithm (RFC 3394) using 192 bit keys.<li><code>A256KW</code> - Advanced Encryption Standard (AES) Key Wrap Algorithm (RFC 3394) using 256 bit keys.<li><code>A128GCMKW</code> - AES in Galois/Counter Mode (GCM) (NIST.800-38D) 128 bit keys.<li><code>A192GCMKW</code> - AES in Galois/Counter Mode (GCM) (NIST.800-38D) 192 bit keys.<li><code>A256GCMKW</code> - AES in Galois/Counter Mode (GCM) (NIST.800-38D) 256 bit keys.</ul>The default `encryption` algorithm is `RSA-OAEP-256` |
### Returns

If successful, it returns `true` or a `200 - OK` HTTP status code, otherwise it returns an [Error](../introduction.md#errors)

{% sample lang="http" %}

#### Definition
```
POST https://demo.formelo.com/api/v1/api-apps/process
```

#### Sample Request
```bash
$ curl https://demo.formelo.com/api/v1/api-apps/process \
    -H "Bearer: xxxx-xxxx-xxxx-xxxx-xxxx" \
    -d id="b8v12ns5" \
    -d action="rollover" \
    -d use="signature" \
```

#### Sample Response
```bash
HTTP/1.1 200 OK
```

{% endmethod %}
