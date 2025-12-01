# Blog Platform for GitHub Pages & LinkedIn

A Jekyll-based blog platform for writing and publishing articles in Markdown. Designed for easy deployment to GitHub Pages with built-in LinkedIn sharing capabilities.

## Features

- ✍️ Write blog posts in Markdown
- 🚀 Automatic deployment to GitHub Pages
- 🔗 LinkedIn and social media sharing buttons
- 📱 Responsive design with Minima theme
- 🔍 SEO optimized with meta tags
- 📊 Sitemap and RSS feed generation

## Quick Start

### Prerequisites

- Ruby 3.0 or higher
- Bundler gem
- Git

### Installation

1. Clone this repository or push it to your GitHub account

2. Install dependencies:
```bash
bundle install
```

3. Update the configuration in `_config.yml`:
   - Change `title`, `email`, `description`
   - Update `url` to your GitHub Pages URL (e.g., `https://yourusername.github.io`)
   - Set your social media usernames

4. Run the site locally:
```bash
bundle exec jekyll serve
```

5. Visit `http://localhost:4000` in your browser

## Writing Blog Posts

### Creating a New Post

1. Create a new file in the `_posts` directory with the naming format:
   ```
   YYYY-MM-DD-title-of-your-post.md
   ```

2. Add front matter at the top of the file:
   ```markdown
   ---
   layout: post
   title: "Your Post Title"
   date: YYYY-MM-DD HH:MM:SS +0000
   categories: category-name
   tags: [tag1, tag2, tag3]
   author: Your Name
   description: "Brief description for SEO"
   ---
   
   Your content goes here...
   ```

3. Write your content in Markdown below the front matter

### Markdown Features

- **Headers**: Use `#` for H1, `##` for H2, etc.
- **Bold**: `**text**`
- **Italic**: `*text*`
- **Links**: `[link text](url)`
- **Images**: `![alt text](/assets/images/image.jpg)`
- **Code blocks**: Use triple backticks with language identifier

Example:
````markdown
```python
def hello():
    print("Hello, World!")
```
````

## Publishing to GitHub Pages

### Initial Setup

1. Push your repository to GitHub

2. Go to your repository Settings → Pages

3. Under "Source", select "GitHub Actions"

4. The included `.github/workflows/jekyll.yml` workflow will automatically build and deploy your site

### Automatic Deployment

Every time you push to the `main` branch:
1. GitHub Actions will build your Jekyll site
2. Deploy it to GitHub Pages
3. Your site will be available at `https://yourusername.github.io/repository-name`

## Publishing to LinkedIn

While LinkedIn doesn't support direct API posting, you can easily share your articles:

1. **After publishing to GitHub Pages**, visit your article URL

2. Click the "Share on LinkedIn" button on the post page

3. LinkedIn will open with a pre-filled post containing your article link

4. Add your own commentary and publish to LinkedIn

### Tips for LinkedIn Sharing

- Write a compelling introduction (2-3 sentences) when sharing
- Use relevant hashtags to increase visibility
- Tag relevant people or companies
- Share at optimal times (Tuesday-Thursday, 9am-12pm)

## Project Structure

```
.
├── _config.yml           # Site configuration
├── _posts/               # Blog posts (Markdown files)
├── _layouts/             # HTML templates
├── _includes/            # Reusable HTML components
├── assets/
│   ├── css/             # Custom stylesheets
│   └── images/          # Image files
├── about.md              # About page
├── index.md              # Homepage
├── Gemfile               # Ruby dependencies
└── .github/
    └── workflows/        # GitHub Actions workflows
```

## Customization

### Changing the Theme

The default theme is Minima. To use a different theme:

1. Browse [Jekyll themes](https://jekyllrb.com/docs/themes/)
2. Update `theme` in `_config.yml`
3. Add the theme gem to `Gemfile`
4. Run `bundle install`

### Custom Styling

Add custom CSS in `assets/css/custom.css` and include it in your layouts.

### Adding Pages

Create a new `.md` file in the root directory with front matter:

```markdown
---
layout: page
title: Page Title
permalink: /page-url/
---

Page content here...
```

## Troubleshooting

### Jekyll build fails locally

```bash
bundle update
bundle exec jekyll serve
```

### GitHub Pages deployment fails

- Check the Actions tab in your GitHub repository
- Verify `_config.yml` syntax
- Ensure all front matter is valid YAML

### Posts not appearing

- Verify filename format: `YYYY-MM-DD-title.md`
- Check that the date in front matter isn't in the future
- Ensure the file is in the `_posts` directory

## Resources

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Markdown Guide](https://www.markdownguide.org/)
- [LinkedIn Sharing Best Practices](https://www.linkedin.com/help/linkedin/answer/a522735)

## License

This project structure is available for personal and commercial use.

## Contributing

Feel free to fork this repository and customize it for your needs!

---

Happy blogging! 🎉
