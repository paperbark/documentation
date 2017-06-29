# Creating PDF files
The goal of PaperBark is to make is as easy as possible to create PDF files.
To achieve this goal we created a bunch of SDKs to minimize the developers effort implementing PaperBark.
A list of our SDK's can be found in the [API][docs-api] document.

Explanation about using the SDK's can be found in their own repositories, this document will explain how the HTML documents work.

## Properties
PaperBark gets its data inline, this means that configurations to generate a PDF file are put in the HTML file itself.
There's multiple ways to define the so called "properties". We recommend using meta tags.

### Meta tags
Just like in normal HTML documents meta tags are defined in the `<head>` section of a document.
We support both RDFa (property attribute) and native meta tags (name attribute).
```html
<!DOCTYPE html>
<html>
<head>
	<title>My wonderful PDF!</title>
	<meta property="pb:width" content="200px" />
	<meta name="pb:height" content="200px" />
...
```
Please note that when specifying both property and name attributes we use the property attribute.

### Property list
PaperBark supports a wide variety of customization, therefore we have quite a lot of properties.

| Property name | Property type | Default value | Description                   |
| ------------- | ------------- | ------------- | ----------------------------- |
| width         | size          | 210cm (A4)    | Width of the PDF              |
| height        | size          | 297cm (A4)    | Height of the PDF             |
| title         | string        | -             | Alternative for title element |
| base          | string        | -             | Domain for relative resources |
| subject       | string        | -             | PDF Metadata                  |
| author        | string        | -             | PDF Metadata                  |
| keywords      | string        | -             | PDF Metadata                  |
| storage       | boolean       | false         | Save PDF in PaperPark storage |

All size properties support the following units:
 - PX (pixels)
 - MM (millimeters, default)
 - Q  (quarter-millimeters)
 - CM (centimeters)
 - IN (inches)
 - PT (points)
 - PC (picas)
 
[docs-api]: api.md