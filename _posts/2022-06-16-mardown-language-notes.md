---
title: Markdown and Chirpy notes 
date: 2022-06-16 14:00:00 +0100
categories: [Notes, Markdown]
tags: [markdown, chirpy, jekyll]     # TAG names should always be lowercase
---

## Languages for code blocks:

[`Source`](https://rdmd.readme.io/docs/code-blocks){:target="_blank"}

|Language|Available language mode(s)|
|---|---|
|ASP.NET| `asp` `aspx`|
|C| `c `|
|C++| `c++` `cpp` `cplusplus`|
|C#| `cs` `csharp`|
|Clojure| `clj` `cljc` `cljx` `clojure`|
|CSS| `css` `less` `sass` `scss` `styl` `stylus`|
|cURL| `curl`|
|D| `d`|
|Dart| `dart`|
|Diff| `diff`|
|Docker| `dockerfile`|
|Erlang| `erl` `erlang`|
|Go| `go`|
|GraphQL| `gql` `graphql `|
|Groovy| `gradle` `groovy`|
|Handlebars| `handlebars` `hbs`|
|HTML/XML| `html` `xhtml` `xml`|
|HTTP| `http`|
|Java| `java`|
|JavaScript| `coffeescript` `ecmascript` `javascript` `js` `node`|
|JSX| `jsx`|
|JSON| `json`|
|Julia| `jl` `julia`|
|Kotlin| `kotlin` `kt`|
|Liquid| `liquid`|
|Lua| `lua`|
|Markdown| `markdown`|
|Objective-C| `objc` `objectivec`|
|Objective-C++| `objc++` `objcpp` `objectivecpp` `objectivecplusplus`|
|OCaml| `ocaml` `ml`|
|Perl| `perl` `pl`|
|PHP| `php`|
|PowerShell| `powershell` `ps1`|
|Python| `py` `python`|
|R| `r`|
|React| `jsx`|
|Ruby| `jruby` `macruby` `rake` `rb` `rbx` `ruby`|
|Rust| `rs` `rust`|
|Scala| `scala`|
|Shell| `bash` `sh` `shell` `zsh`|
|Solidity| `sol` `solidity`|
|SQL| `cql` `mssql` `mysql` `plsql` `postgres` `postgresql` `pgsql` `sql`|
|Swift| `swift`|
|TypeScript| `ts` `typescript`|
|YAML| `yaml` ` yml`|

## Table:

#### Code:

```markdown
| Left |  Center  | Right |
|:-----|:--------:|------:|
| L0   | **bold** | $1600 |
| L1   |  `code`  |   $12 |
| L2   | _italic_ |    $1 |

```

#### Result:

| Left |  Center  | Right |
|:-----|:--------:|------:|
| L0   | **bold** | $1600 |
| L1   |  `code`  |   $12 |
| L2   | _italic_ |    $1 |


## Hyperlinks:
Aadding `{:target="_blank"}` after the link, opens it in new tab after cliking it.

#### Code:

```markdown
[`Twitter`](https://twitter.com/){:target="_blank"}
[Twitter](https://twitter.com/){:target="_blank"}
```
#### Result:

[`Twitter`](https://twitter.com/){:target="_blank"}
[Twitter](https://twitter.com/){:target="_blank"}


## Prompts:

#### Code:
```markdown
> This is `tip`.
{: .prompt-tip }
> This is `info`.
{: .prompt-info }
> This is `waning`.
{: .prompt-warning }
> This is `danger`.
{: .prompt-danger }
```

#### Result:
> This is `tip`.
{: .prompt-tip }
> This is `info`.
{: .prompt-info }
> This is `waning`.
{: .prompt-warning }
> This is `danger`.
{: .prompt-danger }



## References
[`Chirpy Demo`](https://chirpy.cotes.page/){:target="_blank"}
[`Language Support for code blocks`](https://rdmd.readme.io/docs/code-blocks){:target="_blank"}
