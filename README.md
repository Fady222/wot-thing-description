# Web of Things (WoT) Thing Description

[![Follow on Twitter](https://img.shields.io/twitter/follow/W3C_WoT.svg?label=follow+W3C_WoT)](https://twitter.com/W3C_WoT)
[![Stack Exchange questions](https://img.shields.io/stackexchange/stackoverflow/t/web-of-things?style=plastic)](https://stackoverflow.com/questions/tagged/web-of-things)

General information about the Web of Things can be found on https://www.w3.org/WoT/.
  
---

Each commit here will sync it to the master, which will expose the content to http://w3c.github.io/wot-thing-description/.

For the draft TD specification for TAG review, please access this [URL](https://cdn.staticaly.com/gh/w3c/wot-thing-description/TD-TAG-review/index.html?env=dev).

To make contributions, please provide pull-requests to the appropriate files,
keeping in mind that some files, most notably `index.html` and `testing/report.html`, 
as well as most files under `visualization`, are
autogenerated and should not be modified directly.
See [github help](https://help.github.com/articles/using-pull-requests/) for 
information on how to create a pull request.

__Note (August 2022):__

__Please notice that Thing Description 1.1 is in the review phase for the Candidate Recommendation (CR) transition. 
In this and subsequent phase, only editorial changes (e.g., adding examples, additional explanations) and bug fixes can be applied to the editorial draft. New feature requests can not be considered and will be postponed to the next version of the Thing Description.__  

## Thing Description Family
This repository covers the W3C Web of Things Thing Description family of specifications.

### Thing Description (Maintenance)
* [Working Draft](http://w3c.github.io/wot-thing-description/) - Latest draft of the Thing Description Maintenance version 
* [branch](https://github.com/w3c/wot-thing-description/) - Points to the master branch of this repo
* [issues](https://github.com/w3c/wot-thing-description/issues) - Points to the issues related to the Thing Description Maintenance version
* [feature log](https://github.com/w3c/wot-thing-description/blob/master/NEW_FEATURES.md) - Log of the new features of the Thing Description Maintenance version compared to Thing Description 1.0


### Thing Description 1.0
* [REC](https://www.w3.org/TR/wot-thing-description/) - Official recommendation version of the Thing Description 1.0
* [branch](https://github.com/w3c/wot-thing-description/tree/wot-td-1.0) - Branch that correspond to the Thing Description 1.0 files
* [errata](https://w3c.github.io/wot-thing-description/errata.html) -  Errata for version 1.0 



## Specification Rendering

Part of the document is automatically rendered using the [STTL.js](https://github.com/vcharpenay/STTL.js/) RDF template engine and Node.js.
_Any change to the document must be performed on the main HTML template [`index.template.html`](index.template.html)_, and not on `index.html`.
To render `index.html`, along with SVG figures, run: 

```sh
npm run render
```

You can also invoke the rendering script directly:
```sh
./render.sh
```

Requirements: Java 8, Node.js 6, [GraphViz](https://graphviz.org/).

The script will first download and install some dependencies (triple store, Node.js dependencies) and then execute the JS script `render.js`.
The latter should always be execute within `render.sh` since it requires some env variables to be set first.

For Windows users, the script should be run in a [Cygwin shell](http://cygwin.com/). Git package from Cygwin distribution had better not be used. Alternative Git client distribution such as [Git for Windows](https://gitforwindows.org/) works better when you encounter an issue building the document using Cygwin.

### Automatic rendering
The repository is equipped with git hooks that automate the rendering process. To enable them, run `npm install` at the root folder. The hooks will render the documents automatically at every commit.
if you run the rending process manually or you do not want to execute the automatic process add `--no-verify` option to your commit command. 

## Implementation Report

To generate the implementation report,
including a list of normative assertions,
issue the following command:
```sh
npm run assertions
```
A draft implementation report will be generated and output to
[testing/report.html](testing/report.html)
which will use relative links back up to [index.html](index.html).
The input to this process is [index.html](index.html)
(_not_ `index.html.template`) so make sure to execute `npm run render` first.

For this to work, the assertions need to 
be marked up as in the following examples and follow RFC2119 conventions:
```html
<span class="rfc2119-assertion" id="additional-vocabularies">
  A JSON TD MAY contain additional optional vocabularies that are 
  not in the Thing Description core model.
</span>
<span class="rfc2119-assertion" id="additional-vocabularies-prefix">
  Terms from additional optional vocabularies used in a JSON-TD MUST 
  carry a prefix for identification within the key name
  (e.g., <tt>"http:header"</tt>).
</span>
```

The assertions must be marked up as follows:
* Enclose each assertion in a span.
* Mark the span with unique id.
  It is recommended that the section id be followed
  by a short unique name for the specific assertion.
* Mark the span with a 'class' attribute set to `rfc2119-assertion`.
* Include one (and only one) instance of the RFC2119 keywords (MUST, MAY, etc.)
  in capitals.
This markup does not change the rendering; it just clearly indicates
and uniquely names the assertion.

It is strongly recommended to make assertions independent of context.
In particular, avoid using pronouns or relational expressions
referring to previous statements not included in the assertion.
Such references can always be replaced with their
antecendent ("dereferenced") without changing the meaning,
and this is less ambigious anyway.
For example, instead of using "this serialization", use
"a JSON-TD serialization".

Also, assertions should ideally only constrain one item.
Multiple constraints should be stated in separate sentences.

Note that the above rendering process also assigns each
table entry a unique ID and these are also listed in the 
table included in the implementation report.

Other data, e.g., data from test results, test specifications,
and implementation descriptions, are also needed to complete the 
implementation report.  See [testing/README.md](testing/README.md)
for details.

The generation of the implementation report also generates a CSS file
`testing/atrisk.css`
that highlights at-risk items in the generated `index.html`.  The at-risk
items are listed in `testing/inputs/atrisk.csv`.  If at-risk items are
updated, to update the at-risk highlighting the implementation report
needs to be generated first, and then the rendering.
