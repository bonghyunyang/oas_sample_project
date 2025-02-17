# Go API client for openapi

This is a sample server Petstore server. For this sample, you can use the api key `special-key` to test the authorization filters.

## Overview
This API client was generated by the [OpenAPI Generator](https://openapi-generator.tech) project.  By using the [OpenAPI-spec](https://www.openapis.org/) from a remote server, you can easily generate an API client.

- API version: 1.0.0
- Package version: 1.0.0
- Generator version: 7.10.0-SNAPSHOT
- Build package: org.openapitools.codegen.languages.GoClientCodegen

## Installation

Install the following dependencies:

```sh
go get github.com/stretchr/testify/assert
go get golang.org/x/oauth2
go get golang.org/x/net/context
```

Put the package under your project folder and add the following in import:

```go
import openapi "github.com/GIT_USER_ID/GIT_REPO_ID"
```

To use a proxy, set the environment variable `HTTP_PROXY`:

```go
os.Setenv("HTTP_PROXY", "http://proxy_name:proxy_port")
```

## Configuration of Server URL

Default configuration comes with `Servers` field that contains server objects as defined in the OpenAPI specification.

### Select Server Configuration

For using other server than the one defined on index 0 set context value `openapi.ContextServerIndex` of type `int`.

```go
ctx := context.WithValue(context.Background(), openapi.ContextServerIndex, 1)
```

### Templated Server URL

Templated server URL is formatted using default variables from configuration or from context value `openapi.ContextServerVariables` of type `map[string]string`.

```go
ctx := context.WithValue(context.Background(), openapi.ContextServerVariables, map[string]string{
	"basePath": "v2",
})
```

Note, enum values are always validated and all unused variables are silently ignored.

### URLs Configuration per Operation

Each operation can use different server URL defined using `OperationServers` map in the `Configuration`.
An operation is uniquely identified by `"{classname}Service.{nickname}"` string.
Similar rules for overriding default operation server index and variables applies by using `openapi.ContextOperationServerIndices` and `openapi.ContextOperationServerVariables` context maps.

```go
ctx := context.WithValue(context.Background(), openapi.ContextOperationServerIndices, map[string]int{
	"{classname}Service.{nickname}": 2,
})
ctx = context.WithValue(context.Background(), openapi.ContextOperationServerVariables, map[string]map[string]string{
	"{classname}Service.{nickname}": {
		"port": "8443",
	},
})
```

## Documentation for API Endpoints

All URIs are relative to *http://petstore.swagger.io/v2*

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*PetAPI* | [**AddPet**](docs/PetAPI.md#addpet) | **Post** /pet | Add a new pet to the store
*PetAPI* | [**DeletePet**](docs/PetAPI.md#deletepet) | **Delete** /pet/{petId} | Deletes a pet
*PetAPI* | [**FindPetsByStatus**](docs/PetAPI.md#findpetsbystatus) | **Get** /pet/findByStatus | Finds Pets by status
*PetAPI* | [**FindPetsByTags**](docs/PetAPI.md#findpetsbytags) | **Get** /pet/findByTags | Finds Pets by tags
*PetAPI* | [**GetPetById**](docs/PetAPI.md#getpetbyid) | **Get** /pet/{petId} | Find pet by ID
*PetAPI* | [**UpdatePet**](docs/PetAPI.md#updatepet) | **Put** /pet | Update an existing pet
*PetAPI* | [**UpdatePetWithForm**](docs/PetAPI.md#updatepetwithform) | **Post** /pet/{petId} | Updates a pet in the store with form data
*PetAPI* | [**UploadFile**](docs/PetAPI.md#uploadfile) | **Post** /pet/{petId}/uploadImage | uploads an image
*StoreAPI* | [**DeleteOrder**](docs/StoreAPI.md#deleteorder) | **Delete** /store/order/{orderId} | Delete purchase order by ID
*StoreAPI* | [**GetInventory**](docs/StoreAPI.md#getinventory) | **Get** /store/inventory | Returns pet inventories by status
*StoreAPI* | [**GetOrderById**](docs/StoreAPI.md#getorderbyid) | **Get** /store/order/{orderId} | Find purchase order by ID
*StoreAPI* | [**PlaceOrder**](docs/StoreAPI.md#placeorder) | **Post** /store/order | Place an order for a pet
*UserAPI* | [**CreateUser**](docs/UserAPI.md#createuser) | **Post** /user | Create user
*UserAPI* | [**CreateUsersWithArrayInput**](docs/UserAPI.md#createuserswitharrayinput) | **Post** /user/createWithArray | Creates list of users with given input array
*UserAPI* | [**CreateUsersWithListInput**](docs/UserAPI.md#createuserswithlistinput) | **Post** /user/createWithList | Creates list of users with given input array
*UserAPI* | [**DeleteUser**](docs/UserAPI.md#deleteuser) | **Delete** /user/{username} | Delete user
*UserAPI* | [**GetUserByName**](docs/UserAPI.md#getuserbyname) | **Get** /user/{username} | Get user by user name
*UserAPI* | [**LoginUser**](docs/UserAPI.md#loginuser) | **Get** /user/login | Logs user into the system
*UserAPI* | [**LogoutUser**](docs/UserAPI.md#logoutuser) | **Get** /user/logout | Logs out current logged in user session
*UserAPI* | [**UpdateUser**](docs/UserAPI.md#updateuser) | **Put** /user/{username} | Updated user


## Documentation For Models

 - [ApiResponse](docs/ApiResponse.md)
 - [Category](docs/Category.md)
 - [Order](docs/Order.md)
 - [Pet](docs/Pet.md)
 - [Tag](docs/Tag.md)
 - [User](docs/User.md)


## Documentation For Authorization


Authentication schemes defined for the API:
### petstore_auth


- **Type**: OAuth
- **Flow**: implicit
- **Authorization URL**: http://petstore.swagger.io/api/oauth/dialog
- **Scopes**: 
 - **write:pets**: modify pets in your account
 - **read:pets**: read your pets

Example

```go
auth := context.WithValue(context.Background(), openapi.ContextAccessToken, "ACCESSTOKENSTRING")
r, err := client.Service.Operation(auth, args)
```

Or via OAuth2 module to automatically refresh tokens and perform user authentication.

```go
import "golang.org/x/oauth2"

/* Perform OAuth2 round trip request and obtain a token */

tokenSource := oauth2cfg.TokenSource(createContext(httpClient), &token)
auth := context.WithValue(oauth2.NoContext, openapi.ContextOAuth2, tokenSource)
r, err := client.Service.Operation(auth, args)
```

### api_key

- **Type**: API key
- **API key parameter name**: api_key
- **Location**: HTTP header

Note, each API key must be added to a map of `map[string]APIKey` where the key is: api_key and passed in as the auth context for each request.

Example

```go
auth := context.WithValue(
		context.Background(),
		openapi.ContextAPIKeys,
		map[string]openapi.APIKey{
			"api_key": {Key: "API_KEY_STRING"},
		},
	)
r, err := client.Service.Operation(auth, args)
```


## Documentation for Utility Methods

Due to the fact that model structure members are all pointers, this package contains
a number of utility functions to easily obtain pointers to values of basic types.
Each of these functions takes a value of the given basic type and returns a pointer to it:

* `PtrBool`
* `PtrInt`
* `PtrInt32`
* `PtrInt64`
* `PtrFloat`
* `PtrFloat32`
* `PtrFloat64`
* `PtrString`
* `PtrTime`

## Author



