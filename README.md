# Fortify SSC Sample Parser Plugin 


<!-- START-INCLUDE:p.marketing-intro.md -->

[Fortify Application Security](https://www.microfocus.com/en-us/solutions/application-security) provides your team with solutions to empower [DevSecOps](https://www.microfocus.com/en-us/cyberres/use-cases/devsecops) practices, enable [cloud transformation](https://www.microfocus.com/en-us/cyberres/use-cases/cloud-transformation), and secure your [software supply chain](https://www.microfocus.com/en-us/cyberres/use-cases/securing-the-software-supply-chain). As the sole Code Security solution with over two decades of expertise and acknowledged as a market leader by all major analysts, Fortify delivers the most adaptable, precise, and scalable AppSec platform available, supporting the breadth of tech you use and integrated into your preferred toolchain. We firmly believe that your great code [demands great security](https://www.microfocus.com/cyberres/application-security/developer-security), and with Fortify, go beyond 'check the box' security to achieve that.

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


## Resources


<!-- START-INCLUDE:repo-resources.md -->

* **Usage**: [USAGE.md](USAGE.md)
* **Releases**: https://github.com/fortify/fortify-ssc-parser-sample/releases
    * _Development releases may be unstable or non-functional. The `*-thirdparty.zip` file is for informational purposes only and does not need to be downloaded._
* **Sample input files**: [sampleData](sampleData)
* **Source code**: https://github.com/fortify/fortify-ssc-parser-sample
* **Automated builds**: https://github.com/fortify/fortify-ssc-parser-sample/actions
* **Contributing Guidelines**: [CONTRIBUTING.md](CONTRIBUTING.md)
* **Code of Conduct**: [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)
* **License**: [LICENSE.txt](LICENSE.txt)
* **Original sample parser**: https://github.com/fortify/sample-parser

<!-- END-INCLUDE:repo-resources.md -->



<!-- START-INCLUDE:h2.support.md -->

## Support

The only warranties for products and services of Open Text and its affiliates and licensors (“Open Text”) are as may be set forth in the express warranty statements accompanying such products and services. Nothing herein should be construed as constituting an additional warranty. Open Text shall not be liable for technical or editorial errors or omissions contained herein. The information contained herein is subject to change without notice.

The software is provided "as is" and is not supported through the regular OpenText Support channels. Support requests may be submitted through the [GitHub Issues](https://github.com/fortify/fortify-ssc-parser-sample/issues) page for this repository. A (free) GitHub account is required to submit new issues or to comment on existing issues. 

Support requests created through the GitHub Issues page may include bug reports, enhancement requests and general usage questions. Please avoid creating duplicate issues by checking whether there is any existing issue, either open or closed, that already addresses your question, bug or enhancement request. If an issue already exists, please add a comment to provide additional details if applicable.

Support requests on the GitHub Issues page are handled on a best-effort basis; there is no guaranteed response time, no guarantee that reported bugs will be fixed, and no guarantee that enhancement requests will be implemented. If you require dedicated support for this and other Fortify software, please consider purchasing OpenText Fortify Professional Services. OpenText Fortify Professional Services can assist with general usage questions, integration of the software into your processes, and implementing customizations, bug fixes, and feature requests (subject to feasibility analysis). Please contact your OpenText Sales representative or fill in the [Professional Services Contact Form](https://www.microfocus.com/en-us/cyberres/contact/professional-services) to obtain more information on pricing and the services that OpenText Fortify Professional Services can provide.

<!-- END-INCLUDE:h2.support.md -->


---

*[This document was auto-generated from README.template.md; do not edit by hand](https://github.com/fortify/shared-doc-resources/blob/main/USAGE.md)*
