# Made With Claw

An open-source website template for [OpenClaw](https://docs.openclaw.ai) users — clone, customize, and deploy marketing websites with 11ty and AWS Amplify.

**Live site:** https://madewithclaw.com

## Quick Start

```bash
# Clone the template
git clone https://github.com/eastsidehealthcare/made-with-claw.git my-site
cd my-site

# Install dependencies
npm install

# Start dev server
npm run dev
```

Then follow the [setup guide](https://madewithclaw.com/guide/clone-template/) to connect AWS Amplify and your domain.

## The Stack

- **Static Site Generator:** [11ty (Eleventy)](https://www.11ty.dev/)
- **Hosting:** AWS Amplify
- **DNS:** AWS Route 53
- **SSL:** Auto-provisioned by Amplify
- **CI/CD:** Auto-deploy on git push
- **PR Previews:** Built-in preview URLs

## Guides

1. [Clone the Template](https://madewithclaw.com/guide/clone-template/) — Fork or clone this repo
2. [GitHub Setup](https://madewithclaw.com/guide/github-setup/) — Configure SSH keys for your assistant
3. [AWS Amplify](https://madewithclaw.com/guide/amplify-setup/) — Set up hosting with auto-deploy
4. [Domain Setup](https://madewithclaw.com/guide/domain-setup/) — Connect your custom domain
5. [Customize](https://madewithclaw.com/guide/customize/) — Update content and branding
6. [SEO Guidelines](https://madewithclaw.com/guide/seo-guidelines/) — Optimize every page

## Project Structure

```
├── src/
│   ├── _data/
│   │   └── site.json         # Site config (name, URL, etc.)
│   ├── _includes/
│   │   └── layouts/
│   │       └── base.njk      # Base HTML template
│   ├── assets/
│   │   └── css/
│   │       └── style.css     # Styles (customize CSS variables)
│   ├── guide/                # Guide pages
│   └── index.njk             # Homepage
├── docs/
│   └── SEO-GUIDELINES.md     # Complete SEO checklist
├── .eleventy.js              # 11ty configuration
├── amplify.yml               # AWS Amplify build settings
└── package.json
```

## SEO Requirements

Every page should include:
- **1000+ words** of unique content
- **Primary keyword** in title, H1, URL, first 100 words
- **3+ external links** to high-authority sites
- **5+ FAQ Q&As** with schema markup
- **Embedded Google Map** in footer

See [docs/SEO-GUIDELINES.md](docs/SEO-GUIDELINES.md) for the complete checklist.

## Contributing

This is an open-source resource for the OpenClaw community. Contributions welcome!

## License

MIT
