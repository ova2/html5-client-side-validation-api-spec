# Motivation

##
- TBD, declarative, etc.

## Validation messages
Handlebars templates http://handlebarsjs.com/, pre-compiled templates for `Bootstrap` messages,
`PrimeUI` messages, `AlertifyJS`, and some other

Validation messages can be created on failed validation in two ways
* Within any explicit defined empty container elements, such as

    ```html
    <section data-csv-msgname="..." data-csv-template="..."></section>
    ```
  
  - `data-csv-msgname` ia an unique name of the messages container. It is cross-referenced via the same attributes on HTML elements, buttons or links. 
  - `data-csv-template` is an optional attribute with a name of the pre-defined template. It is possible to choose either a default template shipped with the implementation or some custom template defined in the application. See `csv.provider.template`.
* Dynamically without explicit defined empty container elements. See the attribute `data-csv-onfail` on HTML elements, buttons or links.

## Structure of validation messages created by API
```js
[
  {"severity": 'info', "message": 'sometext', "optional": ...},
  {"severity": 'warn', "message": 'sometext', "optional": ...},
  {"severity": 'error', "message": 'sometext', "optional": ...}
]
```

## Custom message templates
- TBD

## Data attributes on HTML elements
All attributes are optional.

* `data-csv-converter`
  - The value is one or multiple converter's id(s). Multiple converter's ids should be defined as array.
  Example: `data-csv-converter=['ch.sbb.converter.DateTime', 'ch.sbb.converter.LocalDate']`. A converter does a data conversion,
  e.g. from input `String` to `Date` or `Number`. The result of the data conversion should be passed to the next converter
  in the converter chain or to the validator chain if the last converter finished the conversion. See JavaScript API for more details.
* `data-csv-validator`
  - The value is one or multiple validator's id(s). Multiple validator's ids should be defined as array.
  Example: `data-csv-validator=['ch.sbb.validator.Birthday', 'ch.sbb.validator.Range']`. Multiple validators build a validator chain
  and get applied one after another. See JavaScript API for more details.
* `data-csv-validator-on<event>`
  - Examples: `data-csv-validator-onchange`, `data-csv-validator-onblur`. This syntax is used for instant validation,
  e.g. `onchange`, `onblur`, etc. The value is one or multiple validator's id(s). Multiple validator's ids should be defined as array.
  Multiple validators build a validator chain and get applied one after another. See JavaScript API for more details.
* `data-csv-coptions`
 - Configuration for converter as JSON, e.g. `data-csv-options={"pattern": 'dd.mm.yy'}`. In case of multiple converters, an array of options
 can be defined in the same order as converters. Example: `data-csv-coptions=[{"pattern": 'dd.mm.yy'}, {"timeZone"='EST', "type": 'date'}]`.
* `data-csv-voptions`
 - Configuration for validator as JSON, e.g. `data-csv-voptions={"minlength": 2, "maxlength": 8}`. In case of multiple validators, an array of options
 can be defined in the same order as validators. Example: `data-csv-voptions=[{"regex": '[a-z]'}, {"minlength": 2, "maxlength": 8}]`.
 Options are also useful for cross-field validation, e.g. checking if values in two fields are equal. In this case, other field(s) could be
 referenced by some selectors defined in `data-csv-voptions`.
* `data-csv-msgname-ref`
 - Reference to an unique message name of the messages container the validation message(s) will be displayed in.
* `data-csv-onfail`
 - A script or an JS function which is invoked on failed validation. The function can be used to create and/or show a message dynamically.
 - Parameter: TBD
* `data-csv-label`
 - Label which belongs to the validated value. It can be used in the validation message. If this attribute is omitted, the implementation should
 try to figure out the label dynamically. An algorithm could be as follows: go to the parent element and find a child label element with
 the same value in the `for` attribute as the `id` of this element.
* `data-csv-valueprovider-ref`
 - Reference to an unique name of a registered value provider. A value provider returns the value to be validated.
 This can be used with custom widgets, such as Select2 or many other, which hide native HTML elements and display fancy UI.
 See the configuration `csv.provider.value` for more details.
* `data-csv-highlighter-ref`
 - Reference to an unique name of a registered highlighter. The highlighter is responsible for highlighting and unhighlighting the label of the invalid element
 and the element itself. Highlighting means e.g. that the label of the invalid element becomes red and the invalid element itself gets red borders.
 Any custom logic can be implemented. See the configuration `csv.highlighter` for more details.
 
## Data attributes on button / link
All attributes are optional.

* `data-csv-process`
 - It points to HTML editable elements or container(s) with editable elements which should be validated. The value of this attribute should be one
 or multiple valid CSS selector(s). Multiple selectors should be surrounded by parentheses (...) and separated by blanks.
 Example: `data-csv-process="(div > ul > li) (table tr.selected) (.form-group)"` One selector doesn't need to be surrounded by parentheses.
 If this attribute is missing but either `data-csv-msgname-ref` or `data-csv-onfail` are present, the closest `form` will be processed.
* `data-csv-msgname-ref`
 - Reference to a message name of the messages container the validation message(s) will be displayed in. This value can be overwritten
 by the same attributes on HTML elements.
* `data-csv-onfail`
 - A script or an JS function which is invoked on failed validation. The function can be used to create a message dynamically, e.g. for growl notification.
 It is invoked as the last step in the validation process - after all messages have been created and linked with the templates.
 This value can be overwritten by the same attributes on HTML elements.

## Configuration
The framework should allow pluggable providers.

* `csv.provider.template` Array of templates for validation messages. Implementation can ship some default providers, e.g. for Bootstrap, PrimeUI.
* `csv.provider.value` Value provider object with the signature TBD. function with Input: element with data-csv-* Output: value to be validated.
 Implementation can ship some default providers, e.g. for Bootstrap, PrimeUI.
* `csv.highlighter` Highlighting provider object with the signature TBD. Implementation can ship some default providers, e.g. for Bootstrap, PrimeUI.
 A provider is an JavaScript object with two functions: highlight and unhighlight to highlight and unhighlight the label of the invalid element and
 the element itself. Every function has Input: element with data-csv-* Output: no.
 
## JavaScript API
* csv.validate({process: ..., msgname: ..., onfail: ...})
* csv.registerValueProvider(type, function(element) {...})
* csv.registerHighlighter(type, function(element) {...})
* TBD

## Technical notes (recommendations)
* The client-side validation should work in IE9+ and all other browsers.
* The framework should be completely declatative. The framework observers DOM nodes insertion. That means, also AJAX updates on elements, buttons
 and links should considered and new added elements, buttons and links should be prepared for triggering validation without developers need to deal
 with JavaScript code.
