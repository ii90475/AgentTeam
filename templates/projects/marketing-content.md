# Marketing/Content Project Template

## Description
Content-focused projects — landing pages, marketing sites, documentation sites, blogs, product launches.

## Typical Tech Stacks

| Layer | Options |
|-------|---------|
| Site Generator | Astro, Next.js, Hugo, Docusaurus |
| Styling | Tailwind CSS, CSS Modules |
| CMS | Contentful, Sanity, MDX files |
| Analytics | Plausible, PostHog, Google Analytics |
| Forms | Formspree, Netlify Forms |
| Hosting | Vercel, Netlify, Cloudflare Pages |

## Recommended Agents

### Local Agents (Routine Tasks)
| Agent | Use For |
|-------|---------|
| **doc-generator** | Landing page copy, blog posts, docs |
| **status-updater** | Campaign progress, launch checklists |
| **changelog-writer** | Product update announcements |
| **code-scaffolder** | Page templates, components |

### Claude Agents (Complex Tasks)
| Agent | Use For |
|-------|---------|
| **project-manager** | Launch timelines, content calendar |
| **technology-analyst** | Platform selection, SEO strategy |

## Project Structure

```
{project-name}/
├── .claude/
├── CLAUDE.md
├── README.md
├── docs/
│   ├── project-status.md
│   ├── content-calendar.md
│   └── changelog.md
├── src/
│   ├── pages/           # Site pages
│   ├── components/      # UI components
│   ├── layouts/         # Page layouts
│   └── styles/          # CSS/Tailwind
├── content/
│   ├── blog/            # Blog posts (MDX)
│   ├── docs/            # Documentation
│   └── assets/          # Images, videos
├── public/
│   ├── images/
│   └── favicon.ico
├── .env.example
├── .gitignore
└── package.json
```

## Initial Setup Checklist

- [ ] Initialize site generator
- [ ] Set up design system/styling
- [ ] Create base layouts
- [ ] Configure CMS or content structure
- [ ] Set up analytics
- [ ] Configure SEO (meta tags, sitemap, robots.txt)
- [ ] Set up form handling
- [ ] Configure deployment
- [ ] Create content templates
- [ ] Set up social sharing previews
