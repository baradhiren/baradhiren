# Hiren's Blog

Personal blog built with [Hugo](https://gohugo.io/) and the [Cactus](https://github.com/monkeyWzr/hugo-theme-cactus) theme.

**Live site:** [hiren.netlify.app](https://hiren.netlify.app/)

## Local Development

### Prerequisites

- [Hugo](https://gohugo.io/getting-started/installing/) (v0.83.1+)
- [Git](https://git-scm.com/)

### Setup

```bash
# Clone the repository with submodules
git clone --recurse-submodules https://github.com/baradhiren/baradhiren.git
cd baradhiren

# Start the development server
hugo server -D
```

The site will be available at `http://localhost:1313/`.

### Creating a New Post

```bash
hugo new posts/my-new-post.md
```

## Deployment

The site is deployed automatically via:

- **Netlify** - Builds and deploys on every push to the main branch
- **GitHub Pages** - Deploys via GitHub Actions workflow on push to `main`

## Structure

```
.
├── archetypes/     # Default front matter templates
├── content/        # Blog posts and pages
│   ├── about/      # About page
│   ├── now/        # Now page
│   └── posts/      # Blog posts
├── public/         # Generated site output
├── themes/cactus/  # Hugo theme (git submodule)
├── config.toml     # Hugo site configuration
└── netlify.toml    # Netlify deployment configuration
```
