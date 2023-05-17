# generaitiv-docs
API specifications for the generaitiv ecosystem

## Authentication
All API requests should be autheticate using the api key provided 

## Search endpoints
/q/latest-tokens : This endpoint returns a list of the latest tokens listed on the platform

/q/latest-collections : This endpoint returns a list of thr latest collections 

## Tokens
/tokens/collection/:id : This endpoint returns tokens within a given collection

## Image Upload
/upload/token/:tokenId/:filename : This endpoint returns a signed put url for uploading an image given a tokenId

## User endpoints
/u/:id : This endpoint returns the user metadata given a wallet address

/u/:id/collections : Return the collections made by a given user

## Collection endpoints
/c/:id : Return the metadata for a given collection

/c/:id/:tokenId : Return metadata and information for a given collection address/slug and tokenId

/c/slug-from-id/:tokenId : Return the slug of a given tokenId

/c/next/:id : Return the next tokenId for a given user address (to create a new token)

POST /c/token/:id/:tokenId : Create a new token

## API Key endpoints

/consumer/user-info : Return the given user for an api key
