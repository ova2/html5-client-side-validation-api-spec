# Motivation

##
- TBD, declarative, etc.

## Validation messages
Handlebars templates http://handlebarsjs.com/, pre-compiled templates for Bootstrap messages, PrimeUI messages, AlertifyJS, and some other

Validation messages can be created on failed validation in two ways
- Within any explicit defined empty container elements, such as <pre><code>&lt;section data-csv-msgname=&quot;...&quot; data-csv-template=&quot;...&quot;&gt;&lt;/section&gt;</code></pre>
 - data-csv-msgname an unique name of the messages container. It is cross-referenced via the same attributes on HTML elements, buttons or links. 
 - data-csv-template - an optional attribute with a name of the pre-defined template. It is possible to choose either a default template shipped with the implementation or some custom template defined in the application. See csv.provider.template.
- Dynamically without explicit defined empty container elements. See the attribute data-csv-onfail on HTML elements, buttons or links.

## Structure of validation messages created by API
<pre><code>
[
  {severity: 'info', message: '...', optional: ...},
  {severity: 'warn', message: '...', optional: ...},
  {severity: 'error', message: '...', optional: ...}
]
</code></pre>

## Custom message templates
- TBD

## Data attributes on HTML elements
All attributes are optional.
- data-csv-converter
 - It represents a converter's id.
- data-csv-validator
 - It represents a validator's id.
- data-csv-coptions
 - Configuration for converter as JSON, e.g. data-csv-coptions={pattern: 'dd.mm.yy'}
- data-csv-voptions
 - Configuration for validator as JSON, e.g. data-csv-voptions={minlength: 2, maxlength: 8} 
- data-csv-msgname
 - Message name of the messages container the validation message(s) will be displayed in
- data-csv-onfail
 - a script or an JS function which is invoked on failed validation. The function can be used to create and/or show a message dynamically
 - parameter: TBD
- data-csv-valueprovider
 - value provider - script or JS function which returns the value to be validated. This can be used with custom widgets, such as Select2 or many other, which hide native HTML elements and display fancy UI.
- data-csv-label
 - label which belongs to the validated value. It can be used in the validation message. See also csv.provider.label
- data-csv-highlighter
 - JS object with two functions: highlight and unhighlight. These functions highlightes and unhighlightes the label of the invalid element and the element itself. Highlighting means e.g. that the label of the invalid element becomes red and the invalid element itself gets red borders. Any custom logic can be implemented. See also csv.provider.highlighter.
 
## Attributes on button / link
All attributes are optional.
- data-csv-process
 - It points to HTML editable elements or container(s) with editable elements which should be validated. The value of this attribute should be one or multiple valid CSS selector(s). Multiple selectors should be surrounded by parentheses (...) and separated by blanks. Example: data-csv-process="(div > ul > li) (table tr.selected) (.form-group)" One selector doesn't need to be surrounded by parentheses. If this attribute is missing but either data-csv-msgname or data-csv-onfail are present, the closest form will be processed.
- data-csv-msgname
 - Message name of the messages container the validation message(s) will be displayed in. This value can be overwritten by the same attributes on HTML elements.
- data-csv-onfail
 - A script or an JS function which is invoked on failed validation. The function can be used to create a message dynamically, e.g. for growl notification. It is invoked as the last step in the validation process - after all messages have been created and linked with the templates. This value can be overwritten by the same attributes on HTML elements.

## Standard converters
- TBD

## Standard validators
- TBD
- don't forget equals of two fields (cross-field validation). Fields can be referenced by some selectors defined in data-csv-voptions
 
## Configuration
The framework should allow pluggable providers.
 - csv.provider.label Label provider. Implementation can ship some default providers, e.g. for Bootstrap, PrimeUI. A provider is an JavaScript function with Input: element with data-csv-* Output: Label element.
 - csv.provider.highlighter Highlighting provider. Implementation can ship some default providers, e.g. for Bootstrap, PrimeUI. A provider is an JavaScript object with two functions: highlight and unhighlight to highlight and unhighlight the label of the invalid element and the element itself. Every function has Input: element with data-csv-* Output: no.
 - csv.provider.template Array of templates for validation messages. Implementation can ship some default providers, e.g. for Bootstrap, PrimeUI.
 
## JavaScript API
 - csv.validate({process: ..., msgname: ..., onfail: ...})
 - TBD

## Technical notes
 - The client-side validation should work in IE9+ and all other browsers.
 - The framework should be completely declatative. That means, also AJAX updates on buttons and links should considered and new added buttons and links should be prepared for triggering validation without developers need to deal with JavaScript code.
