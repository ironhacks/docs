# IronHacks Platform Docs

Documentation is generated using Markdown with __MkDocs__ and the *Read the Docs* style theme.

The following documents cover information for the following RCODI IronHacks projects that make up the IronHacks Ecosystem

Docs files can be hosted on GitHub Pages in a separate repository or can exist as a subfolder of an individual project, or can live on it's own `gh-pages` branch within a repository. GitHub will automattically update the documentation each time files under these locations are changed with a new commit.

## Setup

The following instructions refer to steps needed to update the documentation site itself, unrelated to the main ironhacks-app or services.

### Install Dependencies

- [mkdocs](https://www.mkdocs.org/)

__Python Markdown Extensions__

These optional and most are already included with MKDocs

- [python-markdown/extensions/](https://python-markdown.github.io/extensions/)

List of builtin markdown extensions: [python-markdown.github.io/extensions/](https://python-markdown.github.io/extensions/)


### Project layout

    mkdocs.yml        # The configuration file.
    docs/
      - index.md      # The documentation homepage.
      - sectionA.md   # Other markdown pages
      ...

      subfolder/      # Creates a new section with the title of the folder
          - index.md
          - sectionB.md  


### Config

**mkdocs.yml**

```yaml
theme: 'readthedocs'
```

__List of all mkdocs config options:__

[mkdocs.org/user-guide/configuration](https://www.mkdocs.org/user-guide/configuration/)

### Usage

__Development__

In the main project folder, run `mkdocs serve` and then visit `http://localhost:8000` in your web browser.

__Build__

In the main project folder `mkdocs build`. This will compile all of the files needed to serve the site in the `site` folder.

*Note: GitHub uses a folder named "docs" to serve static sites from a project.*

__Deploy__

This project uses GitHub actions to automatically rebuild the site each time there is a commit to the main branch.

This runs the build command and publishes the output to a branch named `gh-pages` where the files are served by GitHub at [https://ironhacks.github.io/ironhacks-docs](https://ironhacks.github.io/ironhacks-docs).

You should not need to manually publish the project to make updates to the site.

In case this step is required the command `mkdocs gh-deploy` will do the same thing. You should exercise caution when using this command because it will update the project repository directly and commit changes to the main branch.

---

View the docs live at: [https://ironhacks.github.io/ironhacks-docs](https://ironhacks.github.io/ironhacks-docs/)

View the docs repository: [https://github.com/ironhacks/ironhacks-docs](https://github.com/ironhacks/ironhacks-docs)
