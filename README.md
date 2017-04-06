# api documentation for  [cssshrink (v0.0.5)](https://github.com/stoyan/cssshrink)  [![npm package](https://img.shields.io/npm/v/npmdoc-cssshrink.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-cssshrink) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-cssshrink.svg)](https://travis-ci.org/npmdoc/node-npmdoc-cssshrink)
#### CSS minifier

[![NPM](https://nodei.co/npm/cssshrink.png?downloads=true)](https://www.npmjs.com/package/cssshrink)

[![apidoc](https://npmdoc.github.io/node-npmdoc-cssshrink/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-cssshrink_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-cssshrink/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-cssshrink/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-cssshrink/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Stoyan",
        "email": "ssttoo@ymail.com"
    },
    "bin": {
        "cssshrink": "./bin/cli.js"
    },
    "bugs": {
        "url": "https://github.com/stoyan/cssshrink/issues"
    },
    "dependencies": {
        "csscolormin": "*",
        "gonzales-ast": "*",
        "prettyugly": "*"
    },
    "description": "CSS minifier",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "b9f2b16eab68b897efcde0f3873229068072dd64",
        "tarball": "https://registry.npmjs.org/cssshrink/-/cssshrink-0.0.5.tgz"
    },
    "gitHead": "58252380c9a80e86ba09e13ff7c5e05123b1b080",
    "homepage": "https://github.com/stoyan/cssshrink",
    "keywords": [
        "css",
        "transform",
        "browser",
        "minify"
    ],
    "main": "index",
    "maintainers": [
        {
            "name": "stoyan",
            "email": "ssttoo@ymail.com"
        }
    ],
    "name": "cssshrink",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/stoyan/cssshrink.git"
    },
    "scripts": {
        "test": "node tests/t.js"
    },
    "version": "0.0.5"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module cssshrink](#apidoc.module.cssshrink)
1.  [function <span class="apidocSignatureSpan">cssshrink.</span>shrink (css)](#apidoc.element.cssshrink.shrink)
1.  [function <span class="apidocSignatureSpan">cssshrink.</span>shrinkAST (ast)](#apidoc.element.cssshrink.shrinkAST)
1.  object <span class="apidocSignatureSpan">cssshrink.</span>util

#### [module cssshrink.util](#apidoc.module.cssshrink.util)
1.  [function <span class="apidocSignatureSpan">cssshrink.util.</span>addslashes (str, q)](#apidoc.element.cssshrink.util.addslashes)
1.  [function <span class="apidocSignatureSpan">cssshrink.util.</span>stripLeadingZero (n)](#apidoc.element.cssshrink.util.stripLeadingZero)
1.  [function <span class="apidocSignatureSpan">cssshrink.util.</span>stripslashes (str)](#apidoc.element.cssshrink.util.stripslashes)
1.  [function <span class="apidocSignatureSpan">cssshrink.util.</span>unfix (str)](#apidoc.element.cssshrink.util.unfix)



# <a name="apidoc.module.cssshrink"></a>[module cssshrink](#apidoc.module.cssshrink)

#### <a name="apidoc.element.cssshrink.shrink"></a>[function <span class="apidocSignatureSpan">cssshrink.</span>shrink (css)](#apidoc.element.cssshrink.shrink)
- description and source-code
```javascript
function shrink(css) {
  var ast = gonzo.parse(css);
  ast = traverseAST(ast);
  return gonzo.toCSS(ast);
}
```
- example usage
```shell
...

## Usage

'''js
  var cssshrink = require('cssshrink');
  var css =
    'a{color: #ff0000;}';
  css = cssshrink.shrink(css);
'''

Result:

    a{color:red}

## Playground
...
```

#### <a name="apidoc.element.cssshrink.shrinkAST"></a>[function <span class="apidocSignatureSpan">cssshrink.</span>shrinkAST (ast)](#apidoc.element.cssshrink.shrinkAST)
- description and source-code
```javascript
function shrinkAST(ast) {
  return traverseAST(ast);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.cssshrink.util"></a>[module cssshrink.util](#apidoc.module.cssshrink.util)

#### <a name="apidoc.element.cssshrink.util.addslashes"></a>[function <span class="apidocSignatureSpan">cssshrink.util.</span>addslashes (str, q)](#apidoc.element.cssshrink.util.addslashes)
- description and source-code
```javascript
function addslashes(str, q) {
  str = stripslashes(str);
  return str.replace(new RegExp(q, 'g'), '\\' + q);
}
```
- example usage
```shell
...
  process: function(node) {
for (var i = 0; i < node.length; i++) {
  if (node[i][0] === 'uri') {
    if (node[i][1][0] === 'raw') { // unquoted url
      var q = '"';
      // replace with a string quoted with default " and escape other "s
      // later the quotes visitor optimizes " vs '
      node[i] = ['string', [q, util.addslashes(node[i][1][1], q), q].join('')];
    } else if (node[i][1][0] === 'string') {
      // rewrite node throwing out url() and leaving string only
      node[i] = ['string', node[i][1][1]];
    }
  }
}
return node;
...
```

#### <a name="apidoc.element.cssshrink.util.stripLeadingZero"></a>[function <span class="apidocSignatureSpan">cssshrink.util.</span>stripLeadingZero (n)](#apidoc.element.cssshrink.util.stripLeadingZero)
- description and source-code
```javascript
function stripLeadingZero(n) {
  // strip leading 0.
  if (n > 0 && n < 1) {
    n = String(n).replace('0.', '.');
  }
  return String(n);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cssshrink.util.stripslashes"></a>[function <span class="apidocSignatureSpan">cssshrink.util.</span>stripslashes (str)](#apidoc.element.cssshrink.util.stripslashes)
- description and source-code
```javascript
function stripslashes(str) {
  return str.replace(/\\(.?)/g, function(match, sym) {
    return sym === '"' || sym === "'"
      ? sym
      : match;
  });
}
```
- example usage
```shell
...
module.exports = {

  test: function(name, nodes) {
return name === 'string';
  },

  process: function(node) {
var str = util.stripslashes(node[1].slice(1, -1));

// try consistent " first
var q = '"';
var doubles = str.match(/"/g);
if (!doubles) {
  node[1] = [q, str, q].join('');
  return node;
...
```

#### <a name="apidoc.element.cssshrink.util.unfix"></a>[function <span class="apidocSignatureSpan">cssshrink.util.</span>unfix (str)](#apidoc.element.cssshrink.util.unfix)
- description and source-code
```javascript
function unfix(str) {
  return str.toLowerCase().replace(/^\-(ms|webkit|moz|o)\-/, '');
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
