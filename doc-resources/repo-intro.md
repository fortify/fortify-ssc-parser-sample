This project provides an alternative implementation for the Fortify SSC sample parser provided at https://github.com/fortify/sample-parser. Compared to the original sample parser:

* This project only provides parser functionality; it currently doesn't include  functionality for generating sample parser input.
* This alternative implementation provides better separation of concerns:
    * The main parser plugin class just provides very simple implementations for the parser SPI methods; actual parsing is done by dedicated parser classes.
    * Functionality for technical JSON parsing (looking for start and end of objects/arrays) is provided by the [fortify-ssc-parser-util](https://github.com/fortify/fortify-ssc-parser-util) library
    * Parser implementations define handlers or use domain objects containing @JsonPropery-annotated fields for handling specific JSON elements.
* This implementation includes some incomplete unit tests. These unit tests will  try to parse a sample input file, failing if there are any parsing exceptions. Information about the parsed data is sent to stderr, but the unit tests don't test whether the actual data was parsed correctly.