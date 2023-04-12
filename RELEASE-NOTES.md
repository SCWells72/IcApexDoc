# Release Notes

* [1.0.0.3](#1003)
* [1.0.0.2](#1002)
* [1.0.0.1](#1001)

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
  2. Surround the parameterized type reference with one of the macros for rendering code, e.g., <code>\`List&lt;Type&gt;\`</code> or `{@code List<Type>}`.
