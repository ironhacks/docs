## About MkDocs

Documentation is generated using Markdown with __MkDocs__ and the *Read the Docs* style theme.

Docs files can be hosted on GitHub Pages in a separate repository or can exist as a subfolder of an individual project, or can live on it's own `gh-pages` branch within a repository. GitHub will automattically update the documentation each time files under these locations are changed with a new commit.

For full documentation visit [mkdocs.org](https://mkdocs.org).


---

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.


__Options__

mkdocs build --clean


## Project layout

    mkdocs.yml        # The configuration file.
    docs/
      - index.md      # The documentation homepage.
      - sectionA.md   # Other markdown pages
      ...

      subfolder/      # Creates a new section with the title of the folder
          - index.md
          - sectionB.md  

## Setup

**mkdocs.yml**

```yaml
theme: 'readthedocs'
```

## Config

__List of all mkdocs config options:__

[mkdocs.org/user-guide/configuration](https://www.mkdocs.org/user-guide/configuration/)


## Extensions

Install with `pip install <EXTENSION_NAME>`

Currently Using:

- smarty
- extra
- toc
- meta
- tables
- fenced_code
- markdown_checklist.extension


__List of Markdown Extensions__

[github.com/Python-Markdown/markdown/wiki/Third-Party-Extensions](https://github.com/Python-Markdown/markdown/wiki/Third-Party-Extensions)
