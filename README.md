# Motivation

## Validation messages
Handlebars templates http://handlebarsjs.com/, pre-compiled templates for Bootstrap messages, PrimeUI messages, AlertifyJS, and some other

Validation messages can be created on failed validation in two ways
- Within any explicit defined empty container elements, such as <pre><code>&lt;div data-jcsv-msgname=&quot;...&quot; data-jcsv-template=&quot;...&quot;&gt;&lt;/div&gt;</code></pre>
 - data-jcsv-msgname an unique name of the messages container
 - data-jcsv-template - an optional attribut with a name of the pre-defined template
- Dynamically without explicit defined empty container elements

## Custom message templates
- TBD

## Data attributes on native HTML elements or JSF components
- data-jcsv-converter
 - converter's id
- data-jcsv-validator
 - validator's id
- data-jcsv-msgname
 - Message name of the messages container the validation message(s) will be displayed in
- data-jcsv-onfail
 - a script or an JS function which is invoked on failed validation. The function can be used to create a message dynamically
 - parameter: TBD
- data-jcsv-valprovider
 - value provider - script or JS function which returns the value to be validated
 
## ClientBehavior
<pre><code>&lt;s:csv process=&quot;@(...)&quot; msgname=&quot;...&quot; onfail=&quot;...&quot;/&gt;</code></pre>
 - process points to HTML editable elements or container(s) with editable elements which should be validated. You can define one or multiple @(...) blocks with jQuery selectors inside. The blocks should be separated by blanks.
 
## Configuration
 - jcsv.labelprovider Array of labelproviders. Some default providers (Bootstrap, PrimeUI) are provided. Input: element with data-jcsv-* Output: Label.
 
## JS API
 - jcsv.validate({process: ..., msgname: ..., onfail: ...})
