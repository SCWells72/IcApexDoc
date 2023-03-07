# Release Notes

* [1.0.0.1](#1001)

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
