# PaperBark API
The PaperBark API is fairly easy to use.
We recommend using one of our available SDK's but implementing the API yourself is also a possibility.

## Using our SDK
### PHP SDK
During private beta we will only support our official [PHP SDK][php-sdk].
We will release more SDK's after the private beta has ended.

## Creating your own implementation
We recommend using our own SDK's for full compatibility but it is possible to create your own implementation.
### Authentication
For authentication we use the `Bearer` scheme in the `Authorization` header.
Example request (where `TOKEN` is your project token):
```
GET /
Host: api.paperbark.io
Authorization: Bearer TOKEN
```
If authentication failed PaperBark responds with a 401 status code.
### Endpoints
The API is based on endpoints, each endpoint serves a different purpose.
During our private beta we will only use a single endpoint: /pdf
#### /pdf
The PDF endpoint requires JSON input with all pages to convert into one PDF.
A simple PDF request would look like this (where `TOKEN` is your project token):
```
POST /pdf
Host: api.paperbark.io
Authorization: Bearer TOKEN
Content-Type: application/json

[
	"<h1>Example page!</h1>",
	"<h1>Second page</h1>"
]
...
```
As you can see, we specify a content-type header (application/json) and the body is our JSON object with two HTML pages.
When the PDF is created the response head looks like the following:
```
200 OK
Content-Type: application/pdf
```
If something went wrong the response might be JSON:
```
500 Internal Server Error
Content-Type: application/json

{"error": "Invalid content-type header"}
```
##### Advanced input
In some cases, an array with HTML pages isn't enough, you might want to add properties or specify the document type. In that case we can use a slightly more advanced JSON format.
A single page can be defined as string:
```json
"<h1>As a string</h1>"
```
Or as object:
```json
{"properties": {"title": "Document title"}, "content": "<h1>As object</h1>"}
```
When using the object syntax it is possible to define properties (instead of using the meta tags).

To define the whole document we can use an array or object:
```json
[
	"<h1>As a string</h1>",
	{"properties": {"title": "Document title"}, "content": "<h1>As object</h1>"}
]
```
```json
{
	"properties": {
		"title": "Test document"
	},
	"pages": [
		"<h1>As a string</h1>",
		{"properties": {"width": "100px"}, "content": "<h1>As object</h1>"}
	]
}
```
In this case, the bonus of using an object is the ability to add properties for all pages.

[php-sdk]: https://github.com/paperbark/php-sdk "paperbark/php-sdk on GitHub"