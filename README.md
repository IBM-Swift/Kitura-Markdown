<p align="center">
    <a href="http://kitura.io/">
        <img src="https://raw.githubusercontent.com/IBM-Swift/Kitura/master/Sources/Kitura/resources/kitura-bird.svg?sanitize=true" height="100" alt="Kitura">
    </a>
</p>


<p align="center">
    <a href="http://www.kitura.io/">
        <img src="https://img.shields.io/badge/docs-kitura.io-1FBCE4.svg" alt="Docs">
    </a>
    <a href="https://travis-ci.org/IBM-Swift/Kitura-Markdown">
        <img src="https://travis-ci.org/IBM-Swift/Kitura-Markdown.svg?branch=master" alt="Build Status - Master">
    </a>
        <img src="https://img.shields.io/badge/os-Mac%20OS%20X-green.svg?style=flat" alt="Mac OS X">
        <img src="https://img.shields.io/badge/os-linux-green.svg?style=flat" alt="Linux">
        <img src="https://img.shields.io/badge/license-Apache2-blue.svg?style=flat" alt="Apache 2">
    <a href="http://swift-at-ibm-slack.mybluemix.net/">
        <img src="http://swift-at-ibm-slack.mybluemix.net/badge.svg" alt="Slack Status">
    </a>
</p>

# Kitura-Markdown
A Templating engine for Kitura that uses Markdown-based templates.

## Summary
`Kitura-Markdown` enables a Kitura-based server to serve HTML content generated from Markdown templates (`.md` files). In addition, `Kitura-Markdown` can be be used to generate HTML from Markdown-formatted text passed to provided helper functions.

## Prerequisites
Swift 4 or above

## Markdown File
Markdown is a lightweight markup language with plain text formatting syntax.

[Mastering Markdown](https://guides.github.com/features/mastering-markdown/) provides documentation and examples on writing markdown files.

By default the Kitura Router will look in the 'Views' folder for Markdown files with the extension '.md'.


## Example
The following is an example of a server generated using `Kitura init` that serves Markdown-formatted text from a `.md` file.

After `Kitura init` the files we are interested in will have the following structure:

<pre>
ServerRepository
├── Package.swift
├── Sources
│    └── Application
│         └── Application.swift
└── Views
     └── Example.md
</pre>

### Package.swift
"https://github.com/IBM-Swift/Kitura-Markdown.git" is defined as a dependency
"KituraMarkdown" added to the targets for Application

### Application.swift
Inside the Application.swift file, the following code is added to render and serve the "Example.md" template to the route "/docs"

```swift
import KituraStencil
```

Inside the `postInit()` function:

```swift
router.add(templateEngine: KituraMarkdown())
router.get("/docs") { _, response, next in
    try response.render("Example.md", context: context: [String:Any]()).end()
    response.status(.OK)
    next()
}
```

### Example.md
The following template will insert the number of articles followed by a list of the articles and their authors.

```
<html>
There are {{ articles.count }} articles. <br />

{% for article in articles %}
- {{ article.title }} written by {{ article.author }}. <br />
{% endfor %}
</html>
```

When the server is running, go to [http://localhost:8080/articles](http://localhost:8080/articles) to view the rendered Stencil template.

## License
This library is licensed under Apache 2.0. Full license text is available in [LICENSE](LICENSE.txt).
