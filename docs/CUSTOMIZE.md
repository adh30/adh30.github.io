# Customize

Here we will give you some tips on how to customize the website. One important thing to note is that **ALL** the changes you make should be done on the **main** branch of your repository. The `gh-p[...]

> **Note for users without coding experience:** You do **not** need to understand the technology stack or have any coding background to create and customize your own website with al-folio. This tem[...]

<!--ts-->

- [Customize](#customize)
  - [Project structure](#project-structure)
  - [Configuration](#configuration)
  - [GitHub Copilot Customization Agent](#github-copilot-customization-agent)
    - [What the Agent Can Help With](#what-the-agent-can-help-with)
    - [How to Use the Agent](#how-to-use-the-agent)
    - [Important: Verify Agent Output](#important-verify-agent-output)
  - [Understanding the Codebase with Code Wiki and DeepWiki](#understanding-the-codebase-with-code-wiki-and-deepwiki)
    - [What are these tools?](#what-are-these-tools)
    - [When to use them](#when-to-use-them)
  - [Technology Stack](#technology-stack)
    - [Frontend](#frontend)
    - [Backend](#backend)
    - [Build and Deployment](#build-and-deployment)
    - [Key Integration Points](#key-integration-points)
  - [Modifying the CV information](#modifying-the-cv-information)
    - [RenderCV Format (Recommended)](#rendercv-format-recommended)
    - [JSONResume Format](#jsonresume-format)
    - [Using Both Formats Simultaneously](#using-both-formats-simultaneously)
    - [Automatic PDF Generation (RenderCV only)](#automatic-pdf-generation-rendercv-only)
  - [Modifying the user and repository information](#modifying-the-user-and-repository-information)
    - [Configuring external service URLs](#configuring-external-service-urls)
  - [Creating new pages](#creating-new-pages)
  - [Creating new blog posts](#creating-new-blog-posts)
  - [Creating new projects](#creating-new-projects)
  - [Adding some news](#adding-some-news)
  - [Adding Collections](#adding-collections)
    - [Creating a new collection](#creating-a-new-collection)
    - [Using frontmatter fields in your collection](#using-frontmatter-fields-in-your-collection)
    - [Creating a teachings collection](#creating-a-teachings-collection)
      - [Course file format](#course-file-format)
      - [Important course collection notes](#important-course-collection-notes)
      - [Required fields](#required-fields)
      - [Optional fields](#optional-fields)
    - [Collections with categories and tags](#collections-with-categories-and-tags)
    - [Creating custom metadata groups and archive pages](#creating-custom-metadata-groups-and-archive-pages)
      - [Understanding Jekyll's special handling of fields](#understanding-jekylls-special-handling-of-fields)
      - [Example: Adding a custom "adaptations" field](#example-adding-a-custom-adaptations-field)
      - [Field naming best practices](#field-naming-best-practices)
      - [Complete example: Book reviews with custom adaptations field](#complete-book-reviews-with-custom-adaptations-field)
  - [Adding a new publication](#adding-a-new-publication)
    - [Author annotation](#author-annotation)
    - [Buttons (through custom bibtex keywords)](#buttons-through-custom-bibtex-keywords)
  - [Changing theme color](#changing-theme-color)
  - [Customizing layout and UI](#customizing-layout-and-ui)
  - [Adding social media information](#adding-social-media-information)
  - [Adding a newsletter](#adding-a-newsletter)
  - [Configuring search features](#configuring-search-features)
  - [Social media previews](#social-media-previews)
    - [How to enable](#how-to-enable)
    - [Configuring preview images](#configuring-preview-images)
    - [Preview image best practices](#preview-image-best-practices)
  - [Related posts](#related-posts)
    - [How it works](#how-it-works)
    - [Configuration](#configuration-1)
    - [Disable related posts for a specific post](#disable-related-posts-for-a-specific-post)
    - [Additional configuration in _config.yml](#additional-configuration-in-_configyml)
  - [Managing publication display](#managing-publication-display)
  - [Adding a Google Calendar](#adding-a-google-calendar)
    - [Basic usage](#basic-usage)
    - [Enable the calendar script for your page](#enable-the-calendar-script-for-your-page)
    - [Optional: Customize the calendar style](#optional-customize-the-calendar-style)
  - [Updating third-party libraries](#updating-third-party-libraries)
  - [Removing content](#removing-content)
    - [Removing the blog page](#removing-the-blog-page)
    - [Removing the news section](#removing-the-news-section)
    - [Removing the projects page](#removing-the-projects-page)
    - [Removing the publications page](#removing-the-publications-page)
    - [Removing the repositories page](#removing-the-repositories-page)
    - [You can also remove pages through commenting out front-matter blocks](#you-can-also-remove-pages-through-commenting-out-front-matter-blocks)
  - [Adding Token for Lighthouse Badger](#adding-token-for-lighthouse-badger)
    - [Personal Access Token (fine-grained) Permissions for Lighthouse Badger:](#personal-access-token-fine-grained-permissions-for-lighthouse-badger)
  - [Customizing fonts, spacing, and more](#customizing-fonts-spacing-and-more)
  - [Scheduled Posts](#scheduled-posts)
    - [Name Format](#name-format)
    - [Important Notes](#important-notes)
  - [GDPR Cookie Consent Dialog](#gdpr-cookie-consent-dialog)
    - [How it works](#how-it-works-1)
    - [When to use](#when-to-use)
    - [How to enable](#how-to-enable-1)
    - [Customizing the consent dialog](#customizing-the-consent-dialog)
    - [Supported analytics providers](#supported-analytics-providers)
  - [Setting up a Personal Access Token (PAT) for Google Scholar Citation Updates](#setting-up-a-personal-access-token-pat-for-google-scholar-citation-updates)
    - [Why is a PAT required?](#why-is-a-pat-required)
    - [How to set up the PAT](#how-to-set-up-the-pat)

<!--te-->

## Project structure

The project is structured as follows, focusing on the main components that you will need to modify:

```txt
.
├── 📂 assets/: contains the assets that are displayed in the website
│   └── 📂 json/
    │   └── 📄 resume.json: CV in JSON format (https://jsonresume.org/)
├── 📂 _bibliography/
│   └── 📄 papers.bib: bibliography in BibTeX format
├── 📂 _books/: contains the bookshelf pages
├── 📄 _config.yml: the configuration file of the template
├── 📂 _data/: contains some of the data used in the template
│   ├── 📄 cv.yml: CV in YAML format, used when assets/json/resume.json is not found
│   ├── 📄 repositories.yml: users and repositories info in YAML format
│   └── 📄 socials.yml: your social media and contact info in YAML format
├── 📂 _includes/: optional local override includes (default includes are gem-owned in `v1.x`)
├── 📂 _layouts/: optional local override layouts (default layouts are gem-owned in `v1.x`)
├── 📂 _news/: the news that will appear in the news section in the about page
├── 📂 _pages/: contains the pages of the website
|   └── 📄 404.md: 404 page (page not found)
├── 📂 _posts/: contains the blog posts
├── 📂 _projects/: contains the projects
└── 📂 test/: starter integration + visual regression checks
```

In `v1.x`, the starter is intentionally thin. Theme internals (layouts/includes/style pipeline/runtime assets) are owned by gems such as `al_folio_core` and `al_folio_distill`.

### Where common files moved in `v1.x`

Most customizations still live in your site repo. The difference is that default implementations now come from gems, so local files with the same path act as overrides.

| Pre-v1 path or feature                                                                                 | v1 owner                           | Customize locally when...                          [...]
| ------------------------------------------------------------------------------------------------------ | ---------------------------------- | ---------------------------------------------------[...]
| `_layouts/default.liquid`, `_layouts/page.liquid`, `_includes/head.liquid`, `_includes/scripts.liquid` | `al_folio_core`                    | you intentionally need site-specific shell/runtime [...]
| `_includes/cv/**`, CV layouts, RenderCV wiring                                                         | `al_folio_cv`                      | you need a one-site CV display override            [...]
| Distill layouts and `assets/js/distillpub/**`                                                          | `al_folio_distill`                 | you maintain custom Distill article behavior       [...]
| Search assets and search setup                                                                         | `al_search`                        | you change the local search UI only for your site  [...]
| Citation badges, Scholar/Inspire helpers, bibliography helpers                                         | `al_citations` and `al_folio_core` | your publication layout needs a local display overr[...]
| External posts                                                                                         | `al_ext_posts`                     | your site has custom external-source rendering     [...]
| Comments                                                                                               | `al_comments`                      | your site needs custom comment markup              [...]
| Analytics                                                                                              | `al_analytics`                     | your site needs a custom analytics provider        [...]
| Math, TikZ, charts, diagrams                                                                           | `al_math` and `al_charts`          | your site has custom rendering snippets            [...]

When migrating an older customized fork, remove old local copies of files that you did not intentionally customize. In the `dfuchss/fuchss.org` rehearsal, deleting old local `_includes/head.liqui[...]

## Configuration

The configuration file [_config.yml](../_config.yml) contains the main configuration of the website. Most of the settings is self-explanatory and we also tried to add as much comments as possibl[...]

> Note that the `url` and `baseurl` settings are used to generate the links of the website, as explained in the [install instructions](INSTALL.md).

All changes made to this file are only visible after you rebuild the website. That means that you need to run `bundle exec jekyll serve` again if you are running the website locally or push your [...]

For `v1.x` starter sites, no local npm style build is required. Core CSS/runtime assets are shipped by the owning gems.

If changes don't appear after refreshing, try:

- **Hard refresh** to reload the page ignoring cached content:
  - [Shift + F5 on Chromium-based browsers](https://support.google.com/chrome/answer/157179#zippy=%2Cwebpage-shortcuts)
  - Ctrl + F5 on Firefox-based browsers
- **Clear your browser cache** completely
- **Use a private/incognito session** to ensure no cached content:
  - [Chrome](https://support.google.com/chrome/answer/95464)
  - [Firefox](https://support.mozilla.org/en-US/kb/private-browsing-use-firefox-without-history)

## GitHub Copilot Customization Agent

This repository includes a specialized GitHub Copilot agent (`.github/agents/customize.agent.md`) designed to help you customize your al-folio website. The agent acts as an expert assistant that [...]

- Guide you through common customization tasks step-by-step
- Modify configuration files, add content, and update your website
- Explain technical concepts in plain language (especially helpful if you're not familiar with Jekyll or web development)
- Apply changes directly to your repository files
- Answer questions about how to customize specific features

### What the Agent Can Help With

The customization agent can assist with tasks such as:

- Changing basic site information (title, author name, contact details)
- Updating your CV or resume
- Adding and managing publications from BibTeX files
- Creating blog posts, projects, and news items
- Customizing theme colors and styling
- Managing social media links
- Enabling or disabling features in `_config.yml`
- Adding profile pictures and other assets
- Troubleshooting configuration issues

### How to Use the Agent

To use the customization agent:

1. Ensure you have a [GitHub Copilot](https://github.com/features/copilot) subscription
2. Open your repository in an editor with GitHub Copilot support (such as VS Code with the GitHub Copilot extension)
3. Interact with GitHub Copilot and ask questions or request changes. For more information, check [Using custom agents in your IDE](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-[...]
4. The agent will guide you through the customization process and can make changes directly to your files

For example, you can ask:

- "How do I change my website's theme color to blue?"
- "Help me add a new blog post about my research"
- "Update my profile information with my new university email"
- "How do I add a publication to my website?"

The agent is designed to be patient and helpful, explaining each step clearly so you understand what's being changed and why.

### Important: Verify Agent Output

**The customization agent can make mistakes or produce incorrect information.** Always review and verify the agent's suggestions and changes before applying them to your repository:

- **Review all changes** – Before applying any modifications, carefully read what the agent suggests and ensure it makes sense for your needs
- **Test locally first** – Before pushing changes to GitHub, test them locally using Docker or native setup (see the [Installation instructions](INSTALL.md))
- **Check syntax** – Make sure any YAML, Markdown, or BibTeX files have correct syntax. Incorrect syntax can break your website
- **Verify configuration** – If the agent modifies `_config.yml` or other configuration files, check that the changes align with your intentions
- **Preview on your site** – Run your site locally and navigate through it to ensure everything displays correctly and works as expected
- **Don't blindly apply changes** – Understand what's being changed and why before committing to your repository

**Example scenarios where verification is important:**

- If the agent suggests a BibTeX entry, verify the syntax matches existing entries in your `_bibliography/papers.bib` file
- If the agent modifies your `_config.yml`, check that indentation is correct (YAML is very sensitive to spacing)
- If the agent creates a new blog post or page, verify the frontmatter (the metadata at the top) is correct
- If the agent suggests changes to theme colors or styling, preview your site locally to ensure the changes look as intended

> **Note:** The customization agent requires GitHub Copilot to be enabled. For more information about GitHub Copilot and its features, see the [GitHub Copilot documentation](https://docs.github.c[...]

## Understanding the Codebase with Code Wiki and DeepWiki

If you're interested in learning more about how al-folio works under the hood, or want to understand specific aspects of the codebase for deeper customization, you can use Code Wiki and DeepWiki [...]

### What are these tools?

**Code Wiki** and **DeepWiki** are AI-powered tools that help you explore and understand GitHub repositories through interactive documentation:

- **Code Wiki** (powered by Google Gemini) generates interactive documentation from the repository code. You can browse the project structure, search for specific functions or modules, view archi[...]
- **DeepWiki** provides an AI chat interface where you can ask natural language questions about the codebase, similar to having an engineer available 24/7. You can ask how features work, search f[...]

### When to use them

Use Code Wiki and DeepWiki **only after**:

- You have reviewed the relevant sections in this `CUSTOMIZE.md` file
- You have checked the [project structure](#project-structure) section above
- You have explored the [documentation index](README.md) and the main guides linked from the root [README](../README.md)

...[content unchanged after this point]