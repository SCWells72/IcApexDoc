# Release Notes

* [1.0.0.9](#1009)
* [1.0.0.8](#1008)
* [1.0.0.7](#1007)
* [1.0.0.6](#1006)
* [1.0.0.5](#1005)
* [1.0.0.4](#1004)
* [1.0.0.3](#1003)
* [1.0.0.2](#1002)
* [1.0.0.1](#1001)

## [1.0.0.9](https://github.com/SCWells72/IcApexDoc/releases/tag/1.0.0.9)

* [Issue 13](https://github.com/SCWells72/IcApexDoc/issues/13) - Enhanced the generated documentation for custom SObject fields to include field metadata information. Note that at present, the format of this documentation is static, though I may extract it into another Velocity template to allow it to be customized. 
* [Issue 14](https://github.com/SCWells72/IcApexDoc/issues/14) - Fixed an issue with link resolution for an unqualified type name in a project with a namespace.
* Updated [highlight.js](https://highlightjs.org/) to the latest version and incorporated support for [David Schach](https://github.com/dschach)'s [highlightjs-apex](https://github.com/highlightjs/highlightjs-apex) Apex grammar extension. These updates can be found in the `headInclude.vm` Velocity template. While optional, it is recommended that custom versions of that template be updated with the respective changes.
* Org-only custom Apex type bodies are now queried using the Salesforce CLI command `sf data query` instead of the older `sfdx force:data:soql:query` command. If you encounter issues with this feature, please make sure that your Salesforce CLI install is up-to-date and valid, potentially [uninstalling](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_uninstall.htm) and [reinstalling](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_install_cli.htm) it if necessary.
* Fixed an issue with Markdown links to standard Apex types with explicit link text, e.g., `[some text](StandardTypeName)`.
* Fixed an issue with types that implement or extend the standard Apex `System.Comparator` interface where it would not be properly included in the type inheritance signature.
* Updated the Apex jorje parser to the latest version.
* Updated standard API documentation URLs for Spring '24 and the `Slack` namespace.

## [1.0.0.8](https://github.com/SCWells72/IcApexDoc/releases/tag/1.0.0.7)

* No functional changes. Updated standard API documentation URLs for Summer '23 and Winter '24.

## [1.0.0.7](https://github.com/SCWells72/IcApexDoc/releases/tag/1.0.0.7)

* [Issue 11](https://github.com/SCWells72/IcApexDoc/issues/11) - Fixed an issue that would result in failed ApexDoc generation if Markdown included `$<something>` that would be interpreted incorrectly as a regular expression group reference.
* Issues reported by Markdown-to-HTML conversion are included in ApexDoc validation output. This can be disabled if desired using the new `validateMarkdown` [ApexDoc validator](README.md#validator-options-file) option.
* Fixed an issue with the `groupPage.vm` Velocity template that would result in an unbalanced `<div>` tag when group content is not present.
* Added a `-verbose`/`--verbose` command-line option to print the full stack trace when exceptions are caught and logged. That behavior is disabled by default but can be enabled when [troubleshooting](README.md#troubleshooting) and reporting issues.

## [1.0.0.6](https://github.com/SCWells72/IcApexDoc/releases/tag/1.0.0.6)

* [Issue 1](https://github.com/SCWells72/IcApexDoc/issues/1) - Added an **Index** tab that includes **all** visible declarations (according to the minimum visibility) partitioned by the first character of their namespace-relative (if appropriate) names hyperlinked to their respective declaration documentation. This should hopefully provide a quick and useful way to locate documentation for class constants, utility methods, etc., by name when the exact containing type name is not known.
* [Issue 2](https://github.com/SCWells72/IcApexDoc/issues/2) - Added a **Groups** tab that organizes top-level declarations by their `@group` tag values. If available, the corresponding group content is displayed, and each group name hyperlinks to a group-specific page where all declarations tagged for that group are listed. For more information about how to document groups, see [Group content files](README.md#group-content-files).
* Changed the sorting of top-level and member declarations when a namespace is present to use the namespace-relative name so that names within the same namespace aren't grouped together.
* Added two new options to the [ApexDoc validator](README.md#validator-options-file):
  * `validateMisattributedGroupTag` - If enabled, `@group` tags used in the documentation comment for non-type/trigger declarations are flagged. Enabled by default.
  * `validateGroupContentTag` - If enabled, `@group-content` tags are flagged and the user is guided toward the `-gc`/`--group-content` option. Enabled by default.
* A few cosmetic improvements including selected tab emphasis in the navigation stripe, `code` display of the top-level declaration name in the respective pages, etc.

## [1.0.0.5](https://github.com/SCWells72/IcApexDoc/releases/tag/1.0.0.5)

* [Issue 6](https://github.com/SCWells72/IcApexDoc/issues/6) - IcApexDoc now supports Markdown text formatting (in addition to HTML) in both ApexDoc comments and for overview file contents. For more information, see [Markdown support](README.md#markdown-support). A [demonstration video](https://youtu.be/gyvZaho-lD0) is also available.
  * Note that `@example` text is rendered as an Apex fenced code block when no explicit fenced code blocks are found in the example text.
  * Also note that **great care** has been taken to try to **preserve** as close to the same generated HTML output as possible given the **same** ApexDoc input. In some cases where Markdown(-ish) syntax was already being used for styling, lists, etc., the generated output may actually be **improved**. However, there are likely some situations where the existing ApexDoc content will need small touch-ups to achieve the desired result.
* Fixed an issue where the ApexDoc validator would find and flag issues with references to ApexDoc tags used in content text and not as actual tags.
* Fixed an issue where the top navigation could include dead end links to index pages for missing declaration types.
* Added generator information to the generated HTML files including the IcApexDoc version and generation date. This is included via the `headInclude.vm` Velocity template and can be changed or removed as desired.
* Changed the type of escaping applied during HTML generation from XML 1.1 to HTML 4.0 which likely eliminates a large number of unnecessary escaped entities in HTML, e.g., `&apos;` and `&quot;`, but also may result in proper escapes for some other entities.
* Generally tightened up vertical whitespace in the generated HTML.

## [1.0.0.4](https://github.com/SCWells72/IcApexDoc/releases/tag/1.0.0.4)

* [Issue 9](https://github.com/SCWells72/IcApexDoc/issues/9) - IcApexDoc now uses [Apache Velocity](https://velocity.apache.org/) templates to generate all HTML output files, and it is possible to provide custom templates via the `-ct/--custom-templates` argument. For more information, see [Custom Velocity templates](README.md#custom-velocity-templates).

## [1.0.0.3](https://github.com/SCWells72/IcApexDoc/releases/tag/1.0.0.3)

* [Issue 3](https://github.com/SCWells72/IcApexDoc/issues/3) - IcApexDoc now performs [full semantic validation](README.md#validation) of ApexDoc, reporting issues, omissions, etc., about ApexDoc comments and their respective Apex declarations. Validation rules are fully configurable via a [JSON options file](README.md#validator-options-file).

## [1.0.0.2](https://github.com/SCWells72/IcApexDoc/releases/tag/1.0.0.2)

* [Issue 4](https://github.com/SCWells72/IcApexDoc/issues/4) - IcApexDoc can now read its command-line options from a file by invoking it as `apexdoc @<file>`. Command-line options should be specified exactly one per-line, and blank lines and comments (designated by `#` in the first column) are allowed in the file.
* [Issue 5](https://github.com/SCWells72/IcApexDoc/issues/5) - Added support for generating documentation against a namespace. The namespace is either derived from the specified `sfdx-project.json` file's `namespace` value or explicitly via the `-n/--namespace <namespace>` argument. If `sfdx-project.json` contains a `namespace` value that should _not_ be used, the `-nn/--no-namespace` argument can be specified. The appropriate namespace prefix is included in the generated documentation for and links to all top-level types and triggers, and all custom SObject types and fields. 
* [Issue 7](https://github.com/SCWells72/IcApexDoc/issues/7) - The ApexDoc comment no longer needs to be on the line immediately before the corresponding declaration. The documentation comment that precedes the declaration with only intermediate whitespace is now used.
* [Issue 8](https://github.com/SCWells72/IcApexDoc/issues/8) - Added support for resolution of references from local Apex types to types that are available only in the organization via installed packages. The associated org must be available to the Salesforce CLI via username or alias which can be specified to IcApexDoc using the `-u/--username` argument, and the Salesforce CLI must be available via the system execution path. Org-only types are **not** included in generated ApexDoc by default but can be included if desired using the `-i/--include-org-types` argument.
* The anchored member is now designated visually with a subtle bounding box. This can be customized via CSS using the `.members :target` selector.

## [1.0.0.1](https://github.com/SCWells72/IcApexDoc/releases/tag/1.0.0.1)

* Changed from a single jar distribution to a multi-jar distribution retaining the original dependency jars. This should be a no-op for users.
* The standard Apex classes are now compiled alongside the local source files. This resolves an issue with inheritance relationships against standard base classes and interfaces being properly conveyed into the generated HTML files.
  * Note that I discovered a strange behavior in the Apex jorje parser with references to standard parameterized interfaces, specifically `System.Iterable`, `System.Iterator`, and `Database.Batchable`, where the type parameters must be removed from source handed to the compiler or errors are produced. IcApexDoc does this automatically, but this results in generated HTML that loses the type parameters for those interfaces. I have logged this as an open issue/question with the appropriate folks at Salesforce and will hopefully be able to address it without this negative side-effect once I hear back from them.
* Fixed an issue with stability of declaration sort order when a project contains multiple declarations with the same name but different declaration types, e.g., a class and a trigger with the same name.
* Fixed an issue with the `apexdoc` shell script not properly propagating command-line arguments with spaces.
* Removed a leading space from the `extends`/`implements` clauses of Apex type declaration signatures.
* Improved HTML generation for section details by using tables so that wrapping occurs properly. Note that this required some **updates to the CSS classes**, so if you've customized the CSS, please **reconcile** with the latest `default.css` as needed. I hope to keep these types of changes to a minimum going forward.
* Removed support for escaping of parameterized type references in HTML. This was causing no end of issues and is technically incorrect. The correct solutions are to:
  1. Replace angle brackets with the respective HTML entities, e.g., `List<Type>` becomes `List&lt;Type&gt;`.
  2. Surround the parameterized type reference with one of the macros for rendering code, e.g., <code>&#96;List&lt;Type&gt;&#96;</code> or `{@code List<Type>}`.
