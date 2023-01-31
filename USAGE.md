
<!-- START-INCLUDE:repo-usage.md -->


<!-- START-INCLUDE:usage/h1.standard-parser-usage.md -->

<x-tag-head>
<x-tag-meta http-equiv="X-UA-Compatible" content="IE=edge"/>

<x-tag-script language="JavaScript"><!--
<X-INCLUDE url="https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@10.0.0/build/highlight.min.js"/>
--></x-tag-script>

<x-tag-script language="JavaScript"><!--
<X-INCLUDE url="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js" />
--></x-tag-script>

<x-tag-script language="JavaScript"><!--
<X-INCLUDE url="${gradleHelpersLocation}/spa_readme.js" />
--></x-tag-script>

<x-tag-style><!--
<X-INCLUDE url="https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@10.0.0/build/styles/github.min.css" />
--></x-tag-style>

<x-tag-style><!--
<X-INCLUDE url="${gradleHelpersLocation}/spa_readme.css" />
--></x-tag-style>
</x-tag-head>

# Fortify SSC Sample Parser Plugin - Usage

## Introduction


<!-- START-INCLUDE:p.marketing-intro.md -->

Build secure software fast with [Fortify](https://www.microfocus.com/en-us/solutions/application-security). Fortify offers end-to-end application security solutions with the flexibility of testing on-premises and on-demand to scale and cover the entire software development lifecycle.  With Fortify, find security issues early and fix at the speed of DevOps. 

<!-- END-INCLUDE:p.marketing-intro.md -->



<!-- START-INCLUDE:repo-intro.md -->

This project provides an alternative implementation for the Fortify SSC sample parser provided at https://github.com/fortify/sample-parser. Compared to the original sample parser:

* This project only provides parser functionality; it currently doesn't include  functionality for generating sample parser input.
* This alternative implementation provides better separation of concerns:
    * The main parser plugin class just provides very simple implementations for the parser SPI methods; actual parsing is done by dedicated parser classes.
    * Functionality for technical JSON parsing (looking for start and end of objects/arrays) is provided by the [fortify-ssc-parser-util](https://github.com/fortify/fortify-ssc-parser-util) library
    * Parser implementations define handlers or use domain objects containing @JsonPropery-annotated fields for handling specific JSON elements.
* This implementation includes some incomplete unit tests. These unit tests will  try to parse a sample input file, failing if there are any parsing exceptions. Information about the parsed data is sent to stderr, but the unit tests don't test whether the actual data was parsed correctly.

<!-- END-INCLUDE:repo-intro.md -->


## Plugin Installation

These sections describe how to install, upgrade and uninstall the parser plugin in SSC.

### Install & Upgrade

* Obtain the plugin binary jar file; either:
     * Download from the repository release page: https://github.com/fortify/fortify-ssc-parser-sample/releases
     * Build the plugin from source: https://github.com/fortify/fortify-ssc-parser-sample/CONTRIB.md
* If you already have another version of the plugin installed, first uninstall the previously  installed version of the plugin by following the steps under [Uninstall](#uninstall) below
* In Fortify Software Security Center:
	* Navigate to Administration->Plugins->Parsers
	* Click the `NEW` button
	* Accept the warning
	* Upload the plugin jar file
	* Enable the plugin by clicking the `ENABLE` button
  
### Uninstall

* In Fortify Software Security Center:
     * Navigate to Administration->Plugins->Parsers
     * Select the parser plugin that you want to uninstall
     * Click the `DISABLE` button
     * Click the `REMOVE` button 

## Obtain results


<!-- START-INCLUDE:parser-obtain-results.md -->

Sample data is included in the [sampleData](sampleData) directory. Additional sample data can be obtained using the original sample parser code; see https://github.com/fortify/sample-parser#generating-scan-with-fixed-or-random-data for instructions.

<!-- END-INCLUDE:parser-obtain-results.md -->


## Upload results

Results can be uploaded through the SSC web interface, REST API, or SSC client utilities like FortifyClient or [fcli](https://github.com/fortify-ps/fcli). The SSC web interface, FortifyClient and most other Fortify clients require the raw results to be packaged into a zip-file; REST API and fcli allow for uploading raw results directly.

To upload results through the SSC web interface or most clients:

* Create a `scan.info` file containing a single line as follows:   
     `engineType=SAMPLE_ALTERNATIVE`
* Create a zip file containing the following:
	* The scan.info file generated in the previous step
	* The raw results file as obtained from the target system (see [Obtain results](#obtain-results) section above)
* Upload the zip file generated in the previous step to SSC
	* Using any SSC client, for example FortifyClient or Maven plugin
	* Or using the SSC web interface
	* Similar to how you would upload an FPR file
	
Both SSC REST API and fcli provide options for specifying the engine type directly, and as such it is not necessary to package the raw results into a zip-file with accompanying `scan.info` file. For example, fcli allows for uploading raw scan results using a command like the following:

`fcli ssc appversion-artifact upload <raw-results-file> --appversion MyApp:MyVersion --engine-type SAMPLE_ALTERNATIVE`

<!-- END-INCLUDE:usage/h1.standard-parser-usage.md -->


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

<!-- END-INCLUDE:repo-usage.md -->


---

*This document was auto-generated from USAGE.template.md; do not edit by hand*
