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
- data-csv-validator
 - The value is one or multiple validator's id(s). Multiple validator's ids should be space separated. Example: TBD. Multiple validators should be applied one after another. A validator can do a data conversion if it needs a not String object, e.g. Date or Number. The result of the data conversion should be saved in the attribute data-csv-converted for the purpose of reusing. This behavior can be changed per configuration csv.saveconverted.
- data-csv-validator-on<event>
 - Examples: data-csv-validator-onchange, data-csv-validator-onblur. This syntax is used for instant validation, e.g. onchange, onblur, etc. The value is one or multiple validator's id(s). Multiple validator's ids should be space separated. Multiple validators should be applied one after another. The result of the data conversion should be saved in the attribute data-csv-converted for the purpose of reusing. This behavior can be changed per configuration csv.saveconverted.
- data-csv-options
 - Configuration for validator as JSON, e.g. data-csv-voptions={pattern: 'dd.mm.yy'} or data-csv-options={minlength: 2, maxlength: 8}. In case of multiple validators, an array of options can be defined in the same order as validators. Example: data-csv-options=[{pattern: 'dd.mm.yy'}, {minlength: 2, maxlength: 8}]. 
- data-csv-msgname
 - Message name of the messages container the validation message(s) will be displayed in
- data-csv-onfail
 - a script or an JS function which is invoked on failed validation. The function can be used to create and/or show a message dynamically
 - parameter: TBD
- data-csv-valueprovider
 - value provider - script or JS function which returns the value to be validated. This can be used with custom widgets, such as Select2 or many other, which hide native HTML elements and display fancy UI. See also the configuration csv.provider.value.
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
 - csv.provider.value Generic value provider. Implementation can ship some default providers, e.g. for Bootstrap, PrimeUI. A provider is an JavaScript function with Input: element with data-csv-* Output: value to be validated.
 - csv.provider.highlighter Highlighting provider. Implementation can ship some default providers, e.g. for Bootstrap, PrimeUI. A provider is an JavaScript object with two functions: highlight and unhighlight to highlight and unhighlight the label of the invalid element and the element itself. Every function has Input: element with data-csv-* Output: no.
 - csv.provider.template Array of templates for validation messages. Implementation can ship some default providers, e.g. for Bootstrap, PrimeUI.
 
## JavaScript API
 - csv.validate({process: ..., msgname: ..., onfail: ...})
 - TBD

## Technical notes (recommendations)
 - The client-side validation should work in IE9+ and all other browsers.
 - The framework should be completely declatative. The framework observers DOM nodes insertion. That means, also AJAX updates on elements, buttons and links should considered and new added elements, buttons and links should be prepared for triggering validation without developers need to deal with JavaScript code.
