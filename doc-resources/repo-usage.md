{{include:usage/h1.standard-parser-usage.md}}

## Developing your own parser plugin

The official documentation for developing SSC parser plugins is available at https://github.com/fortify/plugin-api, and the official sample plugin implementation is available at https://github.com/fortify/sample-parser.

If you want to use this alternative example as a starting point for developing your own custom SSC parser plugin:

* Generic changes:
    * Update `settings.gradle` according to the name of your project.
    * Rename packages/classes according to the type of data that you will be parsing.
    * Update `src/main/resources/images` with your plugin icon and logo.
    * Update `src/main/resources/resources` with relevant message properties.
    * Update `src/main/resources/viewtemplate` with the SSC view template used to display issue details.
    * Update `src/main/resources/plugin.xml` with your plugin name, icon/logo, message property files, view template, ...
    * Update CustomVulnAttribute.java to reflect the custom issue attributes that can be reported by your plugin.
    * Implement the actual functionality for parsing your data.
    * Update the main parser plugin class to invoke your actual parser implementations, and log the appropriate start/stop messages.
    * Add one or more sample input files in `sampleData`, and create/update corresponding JUnit tests (see 
      AlternativeSampleParserPluginTest.java). 
    * Update `src/main/resources/plugin.xml` based on all changes above and other plugin configuration.
    * Update `src/main/resources/META-INF/services/com.fortify.plugin.spi.ParserPlugin` to point to your renamed parser plugin class.
    * If you need any additional/other dependencies for your plugin, update `build.gradle`.
* If you need to parse JSON data, use the [fortify-ssc-parser-util-json](https://github.com/fortify-ps/fortify-ssc-parser-util/tree/master/fortify-ssc-parser-util-json) library
* If you need to parse XML data, use the [fortify-ssc-parser-util-xml](https://github.com/fortify-ps/fortify-ssc-parser-util/tree/master/fortify-ssc-parser-util-xml) library
* If you need to parse other types of data, consider developing a similar library and contributing this back to the [fortify-ssc-parser-util](https://github.com/fortify/fortify-ssc-parser-util) project

