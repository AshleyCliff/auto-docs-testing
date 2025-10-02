(sphinx_autodocs)=

# How to import docstrings with Sphinx Autodocs

Module and function details are useful reference material to have in documentation, but the process of manually pulling all the necessary details over can become tedious. The [Sphinx Autodocs extension](https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html) provides capabilities to automatically pull in docstrings and module information for Python code.

## Prerequisites

To use the Sphinx autodocs extension with the Starter Pack, you need:

* Python module files located within the same repository as your documentation

OR

* The code repository added as a [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) into the docs repository

## Setup

In the conf\.py file in your docs directory, update the sys.path so that Sphinx can find your module files. At the top of the file, add a `sys.path.insert` that adds your `<code>` directory:

```{code-block} python
:caption: conf.py

import sys
from pathlib import Path

sys.path.insert(0,str(Path('..','<code>').resolve()))
```

Then, further down in the conf.py, add `sphinx.ext.autodoc` to the list of extensions:

```{code-block} python
:caption: conf.py

extensions = [
    ...
    'sphinx.ext.autodoc',
]
```

## Usage

See [Sphinx's Autodoc instructions](https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html#usage) for details.

## Known issues and limitations

There are a few issues and limitations that should be taken into consideration.

### Language

The extension's usage is limited to Python code. There may exist extensions for other languages that have not been fully tested with the Starter Pack, such as [sphinxcontrib-rust](https://sphinxcontrib-rust.readthedocs.io/en/stable/) for Rust.

### Docstring format

The autodocs extension pulls the docstrings straight into the the reStructuredText document, which requires the docstrings to be in rST format. For docstrings in the Numpy or Google style, the [napoleon](https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html#module-sphinx.ext.napoleon) extension can be enabled to preprocess the docstrings and convert them into rST prior to processing by autodocs.

For documentation that is written in MyST Markdown, wrap the `eval-rst` directive around the autdocs calls:

````{code-block} md

```{eval-rst}

.. py:currentmodule:: code.Fibonacci

.. automodule:: Fibonacci
    :members:

```

````

## Canonical examples

### Ops

* [ops Python source](https://github.com/canonical/operator/tree/main/ops)
* [conf.py](https://github.com/canonical/operator/blob/main/docs/conf.py) - lines 16, 384-416
* Raw rST doc - [ops.rst](https://github.com/canonical/operator/blob/main/docs/reference/ops.rst)
* [Rendered doc](https://documentation.ubuntu.com/ops/latest/reference/ops/)


<!-- 
### Starcraft (not using Starter Pack) 
* [Python source](https://github.com/canonical/craft-application/blob/main/craft_application/services/project.py)
* [conf.py](https://github.com/canonical/craft-application/blob/436e0d53a17c5128271292167de5050979c5bfd4/docs/conf.py)
    * Line 65
* [Raw rST doc](https://github.com/canonical/craft-application/blob/436e0d53a17c5128271292167de5050979c5bfd4/docs/reference/services/project.rst?plain=1#L98)
    * Lines 3, 98-101
* [Rendered doc](https://canonical-craft-application.readthedocs-hosted.com/en/latest/reference/services/project/#craft_application.services.project.ProjectService) 
-->