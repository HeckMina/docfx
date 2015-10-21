Docfx Flavored Markdown
==========================================
Docfx supports "Docfx Flavored Markdown," or DFM. It is 100% compatiable with [Github Flavored Markdown](https://help.github.com/articles/github-flavored-markdown/), and adds some additional functionality, including cross reference and file inclusion.
### Yaml Header
Yaml header in DFM is considered as the metadata for the markdown file. It will be transformed to `yamlheader` tag when processed.
Yaml header MUST be the first thing in the file and MUST take the form of valid YAML set between triple-dashed lines. Here is a basic example:

```md
---
uid: A.md
title: A
---
```

### Cross Reference
Using `@uid` to quickly reference to other documentations.
Generally the value of `uid` can be found in the `YAML` file generated by running `docfx metadata`. For API in DOTNET world, [2.Identifiers in Metadata Dotnet Spec](metadata_dotnet_spec.md) describes the way to generate `id` for API in dotnet language. For other files, you can add YAML header at the top of the file to define its id.
```md
---
uid: A.md
---
This is a markdown file
```

### File Inclusion
DFM adds syntax to include other file parts into current file, the included file will also be considered as in DFM syntax. *NOTE* that YAML header is **NOT** supported when the file is an inclusion.
There are two types of file inclusion: inline one and block one, as similar to inline code span and block code.

#### Inline
Inline file inclusion is in the following syntax, in which `<title>` stands for the title of the included file, and `<filepath>` stands for the file path of the included file, file path can be either absolute file path or relative file path.`<filepath>` can be wrapped by `'` or `"`. *NOTE* that for inline file inclusion, the file included will be considered as containing only inline tags, e.g. `###header` inside the file will not be transformed as `<h3>` is a block tag, while `[a](b)` will be transformed to `<a href='b'>a</a>` as `<a>` is an inline tag.
```
...Other inline contents... [!inc[<title>](<filepath>)]
```
#### Block
Block file inclusion must be in a single line and with no prefix characters before the start `[`. Content inside the included file will be transformed using DFM syntax.
```
[!inc[<title>](<filepath>)]
```