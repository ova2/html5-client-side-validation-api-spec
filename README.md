# Motivation

## Validation messages
Handlebars templates http://handlebarsjs.com/, pre-compiled templates for Bootstrap messages, PrimeUI messages, AlertifyJS, and some other

Validation messages can be created on failed validation in two ways
- Within any explicit defined empty container elements, such as <pre><code>&lt;section data-csv-msgname=&quot;...&quot; data-csv-template=&quot;...&quot;&gt;&lt;/section&gt;</code></pre>
 - data-csv-msgname an unique name of the messages container
 - data-csv-template - an optional attribut with a name of the pre-defined template
- Dynamically without explicit defined empty container elements

## Custom message templates
- TBD

## Data attributes on HTML elements
All attributes are optional.
- data-csv-converter
 - It represents a converter's id.
- data-csv-validator
 - It represents a validator's id.
- data-csv-msgname
 - Message name of the messages container the validation message(s) will be displayed in
- data-csv-onfail
 - a script or an JS function which is invoked on failed validation. The function can be used to create a message dynamically
 - parameter: TBD
- data-csv-valueprovider
 - value provider - script or JS function which returns the value to be validated
 
## Attributes on button / link
All attributes are optional.
- data-csv-process
 - It points to HTML editable elements or container(s) with editable elements which should be validated. You can define one or multiple @(...) blocks with jQuery selectors inside. The blocks should be separated by blanks. If this attribute is missing but either data-csv-msgname or data-csv-onfail are present, the closest form will be processed.
- data-csv-msgname
 - Message name of the messages container the validation message(s) will be displayed in. This value can be overwritten by the same attributes on HTML elements.
- data-csv-onfail
 - A script or an JS function which is invoked on failed validation. The function can be used to create a message dynamically. This value can be overwritten by the same attributes on HTML elements.

## Standard converters
- TBD

## Standard validators
- TBD
 
## Configuration
 - csv.labelprovider Array of labelproviders. Some default providers (Bootstrap, PrimeUI) are provided. Input: element with data-csv-* Output: Label.
 
## JS API
 - csv.validate({process: ..., msgname: ..., onfail: ...})
