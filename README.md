# API Documentation for generaitiv
API specifications for the generaitiv ecosystem

## Base url
The base url for this API is
```
https://api.generaitiv.xyz/v1/
```
## Authentication
All API requests should be autheticate using the api key available on the profile setting page in generaitiv

Authentication is added via the headers on the request.
An example in javascript is below
```js
let authHeaders = new Headers();
myHeaders.append("Authorization", "Bearer [API-Key]");
myHeaders.append("Content-Type", "application/json");

await fetch("https://api.generaitiv.xyz/v1/", {
  headers: authHeaders
});
```

## Search endpoints
**/q/latest-tokens** : This endpoint returns a list of the latest tokens listed on the platform

Example

```js
const latestTokens = await fetch("https://api.generaitiv.xyz/v1/q/latest-tokens/?page=0&page_size=50", {
  headers: authHeaders
});
await latestTokens.json()
-------------------------
{
  "result": [
    {
      "collection": "0x4b3887515Cd5A0deEaBd6b59f0B8CC87d3608c95",
      "tokenId": "0xfffbfc0674fac46f2d44433192d33d5998a41b07000000000000000000000048",
      "creator": "0xFFfbFC0674faC46f2d44433192d33D5998a41b07",
      "status": "ACTIVE",
      "explicit": false,
      "virtual_address": "0xa4DCeB149FE05B86859653e4fB78191b76305096",
      "content_moderation_score": 0,
      "model": "QmWBtxpyjJwgm6hP2va2T6RuAvXTCw5gHuni5mgYVC2mUz",
      "slug": "sonic-vibration",
      "metadata": {
        "name": "Cathedral of Sorrow #2",
        "description": "Cathedral of Sorrow: A grandiose depiction of a Gothic cathedral, with towering arches, stained glass windows, and somber sculptures. This piece encapsulates the solemnity and spiritual awe associated with Gothic architecture, inviting contemplation and introspection.\n\nGenerated by ai-forever/Kandinsky-2.1",
        "image": "https://metadata.generaitiv.xyz/images/asset/8peM20khuguFaKgRsQTBh.png"
      },
      "created_at": "2023-05-17T14:55:41.218Z",
      "listing": {
        "price": "0x00000000000000000000000000000000000000000000000000b1a2bc2ec50000",
        "startTime": "0x000000000000000000000000000000000000000000000000000000006464eb00",
        "endTime": "0x0000000000000000000000000000000000000000000000000000000065577f00",
        "amount": "0x0000000000000000000000000000000000000000000000000000000000000001"
      }
    }, ...]
}
```

**/q/latest-collections** : This endpoint returns a list of thr latest collections 

Example

```js
const latestCollections = await fetch("https://api.generaitiv.xyz/v1/q/latest-collections/?page=0&page_size=50", {
  headers: authHeaders
});
await latestCollections.json()
-------------------------
{
  "result": [
    {
      "address": "0x4b3887515Cd5A0deEaBd6b59f0B8CC87d3608c95",
      "name": "The Rabbit Pact",
      "slug": "the-rabbit-pact",
      "description": "A Surreal Tale of Love and Betrayal",
      "owner": "0xE51e00dcCfa51960a1B40E1d20c9733E29581593",
      "explicit": false,
      "image": "https://metadata.generaitiv.xyz/images/asset/UG6hhvegHHJRUMl9YbUig.png",
      "virtual": true,
      "created_at": "2023-04-10T16:36:16.331Z"
    }, ...]
}
```

## Tokens
**/tokens/collection/[slug]** : This endpoint returns tokens within a collection given a collection slug or address

Example

```js
const tokensInCollection = await fetch("https://api.generaitiv.xyz/v1/tokens/collection/red-every-day/?cursor=0", {
  headers: authHeaders
});
await tokensInCollection.json()
-------------------------
{
  "pageSize": 14,
  "result": [
    {
      "metadata": {
        "name": "R.E.D. #001",
        "description": "Each intricate piece in the R.E.D collection portrays the red-hooded figures in various scenarios, exploring the depths of their characters and challenging the conventional notions of good and evil. Bold, vivid, and undeniably mesmerizing, these high-resolution digital masterpieces represent the perfect fusion of cutting-edge AI technology and the timeless allure of traditional oil paintings.",
        "image": "https://metadata.generaitiv.xyz/images/asset/f_H5ip5KoxWLr2memvCk7.png"
      },
      "token_refresh_requested_at": "2023-04-13T16:22:39.054Z",
      "tokenId": "0x02d65b0fd9bd351e3b92ebe3d492e0c50d55554a000000000000000000000002",
      "collection": "0x4b3887515Cd5A0deEaBd6b59f0B8CC87d3608c95",
      "status": "ACTIVE",
      "total": "1",
      "entity": "TOKEN",
      "name": "R.E.D. #001",
      "created": "2023-03-28T18:04:32.269Z",
      "modified": "2023-04-13T16:22:39.106Z",
      "contract_type": "ERC1155",
      "token_uri": "https://metadata.generaitiv.xyz/token/02d65b0fd9bd351e3b92ebe3d492e0c50d55554a000000000000000000000002.json",
      "amount": "0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF",
      "virtual_address": "0x47FA5Db2949BfC5aE791Ef34d7C5e20FD894D3c2",
      "pk": "TOKEN",
      "creator_address": "0x02d65B0Fd9bd351e3b92ebe3d492E0c50D55554A"
    }, ...]
}
```
## Image Upload
**/upload/token/[tokenId]/[fileName]** : This endpoint returns a signed put url for uploading an image given a tokenId. The signed url returned accepts a javascript [File](https://developer.mozilla.org/en-US/docs/Web/API/File) object as the body of a put request which will be uploaded and set as the image of the token.

Example

```js
const uploadPutUrl = await fetch("https://api.generaitiv.xyz/v1/upload/token/0xb6bdb5f73b6d717eb6949aee9f9551298493390e000000000000000000000002/a.jpg/", {
  headers: authHeaders
});
await uploadPutUrl.json()
-------------------------
{
  "url":"https://s3.us-east-1.amazonaws.com/scratch.generaitiv.xyz/upload/production/..."
}
```

## User endpoints
**/u/[address]** : This endpoint returns the user metadata given a wallet address

Example

```js
const user = await fetch("https://api.generaitiv.xyz/v1/u/0x4e3A99830E5ffb86952B14aDBD5746ce84A6F6F3/", {
  headers: authHeaders
});
await user.json()
-------------------------
{
  "username": "zkBrain",
  "bio": "$ /dev/null",
  "link": "https://generaitiv.ai",
  "image": "https://img.generaitiv.xyz/profile/64x64/MLuydpuSwkBglk7VoZGKR.png",
  "address": "0x4e3A99830E5ffb86952B14aDBD5746ce84A6F6F3",
  "twitter": "https://twitter.com/zk_brain",
  "twitter_verified": true
}
```

**/u/[address]/collections** : Return the collections made by a given user

Example

```js
const userCollections = await fetch("https://api.generaitiv.xyz/v1/u/0x1BEC0E6266e97f0C7C42aa720959e46598DD8Ce1/collections/", {
  headers: authHeaders
});
await userCollections.json()
-------------------------
{
  "collections": [
    {
      "name": "Poetic Animations by Ashu",
      "slug": "poetic-animations-by-ashu",
      "address": "0x4b3887515Cd5A0deEaBd6b59f0B8CC87d3608c95",
      "description": "Enter the world of cosmic poetry and poetic cosmos.",
      "explicit": false,
      "image": "https://img.generaitiv.xyz/collection_thumbnail/64x64/DoufsO6BuIZvtGEE3cFep.png",
      "twitter": "https://twitter.com/AshwiniDodani",
      "twitter_verified": true,
      "owner": "0x1BEC0E6266e97f0C7C42aa720959e46598DD8Ce1",
      "virtual": true,
      "royalty_fee": 1000,
      "status": "ACTIVE",
      "virtual_address": "0x2E4aae69D95C5F15b151243bDc97795B1D2c0E07",
      "slugOrAddress": "poetic-animations-by-ashu"
    }, ...]
}
```

## Collection endpoints
**/c/[slug]** : Return the metadata for a collection given a slug or address

Example

```js
const collectionMetadata = await fetch("https://api.generaitiv.xyz/v1/u/0x1BEC0E6266e97f0C7C42aa720959e46598DD8Ce1/collections/", {
  headers: authHeaders
});
await collectionMetadata.json()
-------------------------
{
  "name": "Poetic Animations by Ashu",
  "slug": "poetic-animations-by-ashu",
  "address": "0x4b3887515Cd5A0deEaBd6b59f0B8CC87d3608c95",
  "description": "Enter the world of cosmic poetry and poetic cosmos.",
  "explicit": false,
  "image": "https://img.generaitiv.xyz/collection_thumbnail/64x64/DoufsO6BuIZvtGEE3cFep.png",
  "twitter": "https://twitter.com/AshwiniDodani",
  "twitter_verified": true,
  "owner": "0x1BEC0E6266e97f0C7C42aa720959e46598DD8Ce1",
  "virtual": true,
  "royalty_fee": 1000,
  "virtual_address": "0x2E4aae69D95C5F15b151243bDc97795B1D2c0E07"
}
```

**/c/[address]/[tokenId]** : Return metadata and information for a token given a collection address/slug and tokenId

*Hint* the collection address for and virtual token will be 0x4b3887515Cd5A0deEaBd6b59f0B8CC87d3608c95

Example

```js
const tokenMetadata = await fetch("https://api.generaitiv.xyz/v1/c/0x4b3887515Cd5A0deEaBd6b59f0B8CC87d3608c95/0x1bec0e6266e97f0c7c42aa720959e46598dd8ce100000000000000000000004e/", {
  headers: authHeaders
});
await tokenMetadata.json()
-------------------------
{
  "collection": "0x4b3887515Cd5A0deEaBd6b59f0B8CC87d3608c95",
  "tokenId": "0x1bec0e6266e97f0c7c42aa720959e46598dd8ce100000000000000000000004e",
  "amount": "0x0000000000000000000000000000000000000000000000000000000000000003",
  "contract_type": "ERC1155",
  "name": "To The Moon And Back",
  "token_uri": "https://metadata.generaitiv.xyz/token/1bec0e6266e97f0c7c42aa720959e46598dd8ce100000000000000000000004e.json",
  "metadata": {
    "name": "To The Moon And Back",
    "description": "Let the lines not decide our destiny but our destinies change the lines of the world's legacy.",
    "image": "https://metadata.generaitiv.xyz/images/asset/UkVI3r_CjBrJ4QFbSQfoK.gif",
    "attributes": [
      {
        "value": "Genesis Animation",
        "trait_type": "Category"
      },
      {
        "value": "Words to ART",
        "trait_type": "Format"
      },
      {
        "value": "Limited",
        "trait_type": "Edition"
      },
      {
        "value": "Life",
        "trait_type": "Theme"
      },
      {
        "value": "Ashwini Dodani",
        "trait_type": "Artist"
      }
    ]
  },
  "total": "1",
  "creator_address": "0x1BEC0E6266e97f0C7C42aa720959e46598DD8Ce1",
  "virtual_address": "0x2E4aae69D95C5F15b151243bDc97795B1D2c0E07",
  "workload_id": "0xed0fbcda7a00686163bb4afc444866ef"
}
```

**/c/virtual/slug-from-id/[tokenId]** : Return the collection slug of a given tokenId

Example

```js
const tokenSlug = await fetch("https://api.generaitiv.xyz/v1/c/virtual/slug-from-id/0x1bec0e6266e97f0c7c42aa720959e46598dd8ce100000000000000000000004e/", {
  headers: authHeaders
});
await tokenSlug.json()
-------------------------
{
  "slug": "poetic-animations-by-ashu"
}
```

**/c/virtual/next/[address]** : Return the next tokenId for a given user wallet address (to create a new token)

Example

```js
const nextTokenId = await fetch("https://api.generaitiv.xyz/v1/c/virtual/next/0xB6BdB5F73b6d717eb6949AeE9F9551298493390E", {
  headers: authHeaders
});
await nextTokenId.json()
-------------------------
{
  "tokenId":"0xb6bdb5f73b6d717eb6949aee9f9551298493390e000000000000000000000002"
}
```

## POST Endpoints

**/c/virtual/token/[slug]/[tokenId]** : Create a new token

Example

```js
const newToken = await fetch("https://api.generaitiv.xyz/v1/c/virtual/token/aaabbb/0xb6bdb5f73b6d717eb6949aee9f9551298493390e000000000000000000000002/", {
  headers: authHeaders,
  method: "POST",
  body: JSON.stringify({
    "tokenId":"0xb6bdb5f73b6d717eb6949aee9f9551298493390e000000000000000000000002",
    "amount":"0x0000000000000000000000000000000000000000000000000000000000000002",
    "attributes":[{"trait_type":"2","value":"2"}],
    "name":"2",
    "description":"2"
  })
});
await newToken.json()
-------------------------
{
  "success":"true"
}
```

## API Key endpoints

**/consumer/user-info** : Return the given user for an api key

Example

```js
const currentAddress = await fetch("https://api.generaitiv.xyz/v1/consumer/user-info/", {
  headers: authHeaders
});
await currentAddress.json()
-------------------------
{
  "address":"0xB6BdB5F73b6d717eb6949AeE9F9551298493390E"
}
```
