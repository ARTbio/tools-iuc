# New Tool Review Guide

This document describes a checklist suitable as a guide for reviewers of pull requests against the IUC's tools repo. It is a guide only and reviewer discretion is still advised.

**This document is a work in progress!**

The comprehensive list is aimed at new tools. Obviously for tool updates just use the appropriate section of the checklist on the PR diffs.

This checklist is based on the IUC's [Best Practices](https://galaxy-iuc-standards.readthedocs.io/en/latest/index.html) document.

## Repository

* [ ] Is this tool appropriate for the IUC repo (see [CONTRIBUTING.md](https://github.com/galaxyproject/tools-iuc/blob/master/CONTRIBUTING.md))
* [ ] Does the tool already exist in the toolshed?
    * [ ] Is this tool warranted?
    * [ ] Does the IUC account have access to the current repo?
* [ ] If the repository contains more than one tool, should it be separated or made a tool collection?
* [ ] Is there a `.shed.yml` file?
* [ ] Is there a tool `.xml` file?
* [ ] No `tool_dependencies.xml` file. (Has been deprecated and is no longer "Best Practice")


## Files

### .shed.yml

* [ ] Is there a correctly formatted `.shed.yml` file?
* [ ] Are the categories appropriate?
* [ ] Does the name match the `.xml` file?
* [ ] Is the owner set to `iuc`? If not, is the owner set to a current wrapper?
* [ ] Is there a `description`?
* [ ] Are there `homepage_url` & `remote_repository_url` fields and do they point somewhere sensible?

### tool.xml

**Linting**

* [ ] Does the tool pass planemo/travis lint with no warnings or errors?
* [ ] 4 spaces indentation?

**Order of XML Elements**

* [ ] Are the xml elements in the suggested order?
    * tool
    * description
    * macros
    * edam_topics
    * edam_operations
    * parallelism
    * requirements
    * ~~code~~ *deprecated*
    * stdio
    * version_command
    * command
    * environment_variables
    * configfiles
    * inputs
    * request_param_translation
    * outputs
    * tests
    * help
    * citations

**&lt;tool&gt; (name and id etc.)**

* [ ] id and name sensible and not previously used?
* [ ] Version follow [PEP 440](https://www.python.org/dev/peps/pep-0440/) with `+galaxyN`?
* [ ] Is there a `@TOOL_VERSION@` macro token used? (Should there be?)
* [ ] If there is a `profile`, is it appropriate?

**&lt;description&gt;**

* [ ] Is there a description tag?
* [ ] Is the description of suitable length?

**&lt;macros&gt;**

* [ ] If there is more than one tool present (tool collection), is there a `macros.xml` file?
* [ ] Is it appropriate?

**&lt;edam_topics&gt;**

**&lt;edam_operations&gt;**

**&lt;[parallelism]&gt;**

**&lt;requirements&gt;**

* [ ] Are there corresponding conda packages?
* [ ] Are they versioned correctly with `@TOOL_VERSION@`? (or multiple packages/docker containers with correctly described versions)
* [ ] If using R/Perl/Python/Ruby packages etc versions specified in correctly formatted `*_environment` tags?

**&lt;~~code~~&gt;**

* [ ] this tagset has been deprecated and should not be used.

**&lt;stdio&gt;**

* [ ] Is `<stdio>` tagset warranted (or should it use `detect_errors` in the `<command>` tag)

**&lt;version_command&gt;**

* [ ] Is there a version command?
* [ ] `<![CDATA[ ... ]]>` tags?

**&lt;command&gt;**

* [ ] `<![CDATA[ ... ]]>` tags?
* [ ] Is there `detect_errors` in the `<command ... >` tag? Or is it handled by a more comprehensive `<stdio>` tagset?
* [ ] No `interpreter` field in `<command ... >` tag - This is deprecated.
* [ ] Text parameters, input and output files `'single quoted'`?
* [ ] Is the Cheetah indented and readable?
* [ ] Are multiple commands joined with `&&`?
* [ ] Are any extra temporary files (such as indices etc.) created in the CWD?

**&lt;environment_variables&gt;**



**&lt;configfiles&gt;**

**&lt;inputs&gt; and &lt;parameters&gt;**

*General*
* [ ] Order of parameter attributes:
    * name
    * argument
    * type
    * format
    * min | truevalue
    * max | falsevalue
    * value | checked
    * optional
    * label
    * help
* [ ] Do the `argument` attributes include the long form of the underlying tool parameters?

*Boolean*
* [ ] Are the `truevalue` and `falsevalue` set with the underlying tool parameter?

*Dynamic Options*
* [ ] Do conditional parameters use a `select` and not a `boolean`
* [ ] Are the advanced parameters of the tool hidden with appropriate `<section>` tags?

**&lt;request_param_translation&gt;**

**&lt;outputs&gt;**

* [ ] Are optional output files selected using `<filter>` tags (with corresponding `<select>` tags in the `<inputs>` section)

**&lt;tests&gt;**

* [ ] Are there tests?
* [ ] Is most of the functionality of the tool tested?
* [ ] Are the test datasets included in the `test-data` directory?
* [ ] Is the test data of suitable size? (i.e. small..)
* [ ] Do the tests pass?

**&lt;help&gt;**

* [ ] Is it book-ended with `<![CDATA[ ... ]]>` tags?
* [ ] Is it correctly formatted *restructuredText*?
* [ ] Are any images in the `./static/images` directory?

**&lt;citations&gt;**

* [ ] Is there a citation
    - [ ] Is it in bibtex or doi format?
