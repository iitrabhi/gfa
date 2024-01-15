## Building the website
In MkDocs, the default folder for documentation source files is named "docs," and the generated static site files are placed in a folder named "site" after building the documentation. However, since GitHub Pages requires a "docs" folder at the root of the repository to serve the website, I store my MkDocs content in a separate "mkdocs" folder. The provided command restructures the output to meet GitHub Pages' requirements, ensuring the built site is moved to a "docs" folder at the root of my repository.

```bash
"rm -rf ../docs && mkdocs build && mv site ../docs"
```

The command performs three actions in sequence. 
-   First, it removes the existing `docs` directory at the parent path. 
-   Then, it builds the static site with `mkdocs build`, outputting the files to the `site` directory. 
-   Finally, it moves the generated `site` directory to replace the just-deleted `docs` directory at the parent path. 

This sequence is helpful for GitHub Pages, which requires the `docs` folder with site content at the repository's root, especially when your Markdown documentation resides in a separate `mkdocs` folder.

---

Mkdocs expects the logo and favicon to live under `img` folder in `docs` directory.