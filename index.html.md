# Moss

<p align="center">
  <img src="_assets/logo-DBv7Qu6L.png" alt="Moss Logo" width="200" />
</p>

<p align="center">
  <strong>A whimsical static site generator for building blogs with Markdown and Vue</strong>
</p>

<p align="center">
  <a href="#installation">Installation</a> •
  <a href="#features">Features</a> •
  <a href="#getting-started">Getting Started</a> •
  <a href="#cli-reference">CLI Reference</a> •
  <a href="#configuration">Configuration</a>
</p>

***

## Installation

### System Requirements

* Node.js 22.17.0 or later
* npm, yarn, or pnpm

### Install Moss

Install Moss globally to use the CLI:

```bash
pnpm add -g @znck/moss
```

Or use it locally in your project:

```bash
pnpm add -D @znck/moss
```

## Features

✨ **Markdown-First**: Write your content in Markdown with frontmatter support\
⚡ **Fast Development**: Hot-reload development server with Vite\
🔗 **Clean URLs**: Automatic clean URL generation for better SEO\
📱 **SEO Optimized**: Canonical URLs, meta tags, and structured data\
🎭 **RSS/Atom Feeds**: Automatic feed generation for your blog\
📦 **Zero Config**: Works out of the box with sensible defaults\
🔧 **Customizable**: Flexible configuration and theming options\
🚀 **TypeScript Support**: Built with TypeScript for better developer experience\
📝 **Syntax Highlighting**: Code blocks with syntax highlighting via Shiki\
🧮 **Math Support**: LaTeX math rendering with KaTeX\
🏷️ **Tag Support**: Organize content with tags and categories

## Getting Started

### 1. Create a new project

```bash
mkdir my-blog
cd my-blog
pnpm init -y
```

### 2. Install Moss

```bash
pnpm add -D @znck/moss
```

### 3. Create configuration file (optional)

Moss works out of the box with zero configuration, but you can customize your site by creating a `moss.json` file or adding configuration to your `package.json`:

**Option A: Using moss.json**

```json file=moss.json
{
  "title": "My Blog",
  "description": "This is my first blog using Moss",
  "author": "Your Name"
}
```

**Option B: Using package.json**

```json file=package.json
{
  "name": "my-blog",
  "displayName": "My Blog",
  "description": "This is my first blog using Moss",
  "author": "Your Name"
}
```



### 4. Create your first post

Create an `index.md` file:

```markdown file=index.md
---
title: Welcome to My Blog
description: This is my first blog post using Moss
---

# Welcome to My Blog

This is my first blog post built with **Moss**!

Moss makes it easy to create beautiful, fast static sites with Markdown and Vue.

## Features I love

- Easy Markdown writing
- Vue component support
- Fast development server
- SEO optimization
```

### 5. Start the development server

```bash
pnpx moss serve
```

Your site will be available at `http://localhost:5173`

### 6. Build for production

```bash
pnpx moss build
```

The built site will be in the `.moss/dist` directory.

### Deployment

After building, you can deploy the contents of `.moss/dist` to any static hosting service:

```bash
# Build the site
moss build

# Deploy to various platforms
# Netlify
netlify deploy --prod --dir .moss/dist

# Vercel
vercel --prod .moss/dist

# GitHub Pages (copy to docs folder)
cp -r .moss/dist/* docs/

# Or serve locally for testing
cd .moss/dist && python -m http.server 8000
```

## CLI Reference

### `moss serve [directory]`

Starts a development server for your site.

**Options:**

* `directory` - The root directory of your site (defaults to current directory)

**Example:**

```bash
moss serve
moss serve ./my-blog
```

### `moss build [directory]`

Builds your site for production.

**Options:**

* `directory` - The root directory of your site (defaults to current directory)

**Example:**

```bash
moss build
moss build ./my-blog
```

### `moss help`

Shows help information and usage examples.

**Example:**

```bash
moss help
moss --help
moss -h
```

### `moss version`

Shows the current version of Moss.

**Example:**

```bash
moss version
moss --version
moss -v
```

## Configuration

Moss works with zero configuration out of the box, but you can customize your site using either a dedicated `moss.json` file or by adding configuration to your existing `package.json`. Configuration in `moss.json` takes priority over `package.json`.

### Configuration Options

**Using moss.json (recommended for dedicated configuration):**

```json
{
  "title": "My Awesome Blog",
  "description": "A blog about web development and technology",
  "author": "Your Name",
  "baseUrl": "https://yourdomain.com",
  "icon": "path/to/favicon.ico"
}
```

**Using package.json (convenient for simple projects):**

```json
{
  "name": "my-blog",
  "displayName": "My Awesome Blog",
  "description": "A blog about web development and technology",
  "author": "Your Name",
  "homepage": "https://yourdomain.com",
  "icon": "path/to/favicon.ico"
}
```

### Supported Configuration Fields



### Ignored Files and Directories

By default, Moss ignores the following directories when scanning for Markdown files:

* `node_modules/` - Node.js dependencies
* `public/` - Static assets (typically served directly)
* `DRAFT/` - Draft content not ready for publication
* Hidden directories (starting with `.`)

### Clean URLs

Moss automatically generates clean URLs for your pages:

* `about.md` → `/about/`
* `posts/my-post.md` → `/posts/my-post/`
* `index.md` → `/` (homepage)

### Frontmatter Options

Each Markdown file can include frontmatter with the following options:

```yaml
---
title: Page Title
description: Page description for SEO
layout: default # or 'homepage'
type: article # or 'page' or 'homepage'
tags: [web, javascript, tutorial]
---
```



## Directory Structure

A typical Moss project structure:

```
my-blog/
├── package.json          # Basic project info and optional config
├── moss.json             # Optional dedicated config file
├── index.md              # Homepage
├── about.md              # About page
├── posts/                # Blog posts
│   ├── first-post.md
│   └── second-post.md
└── .moss/                # Generated files (git-ignored)
    └── dist/             # Built site
```

## Advanced Usage

### Vue Components

You can use Vue components directly in your Markdown:

```markdown
# My Post

<script setup>
import { ref } from 'vue'
const count = ref(0)
</script>

Click count: {{ count }}

<button @click="count++">Increment</button>
```

Moss uses **Vue 3** with the Composition API, giving you access to all modern Vue features including:

* Composition API with `<script setup>`
* Reactivity (ref, reactive, computed, watch)
* Lifecycle hooks (onMounted, onUnmounted, etc.)
* Custom components and imports

### Custom Layouts

Moss supports different layout types via frontmatter:

* `homepage` - Minimal layout for your main landing page
* `default` - Standard layout with header and navigation (used for both articles and pages)

The layout is determined by the frontmatter `layout` field, but the `type` field helps with content categorization:

```yaml
---
title: My Homepage
layout: homepage # Uses minimal homepage layout
type: homepage # Content type for categorization
---
```

```yaml
---
title: My Blog Post
layout: default # Uses standard layout (default)
type: article # Content type for categorization
---
```

## Example Sites

Looking for inspiration? Check out these websites built with Moss:

* [znck.dev](https://znck.dev) - Personal blog
* [moss.znck.dev](https://moss.znck.dev) - Documentation for Moss

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

MIT License - see [LICENSE](https://znck.dev/licenses/MIT) file for details.

***

<p align="center">
  Made with ❤️ by <a href="https://github.com/znck">@znck</a>
</p>
