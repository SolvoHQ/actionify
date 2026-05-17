# DescribeIt

Generate working HTML/CSS/JS from natural language prompts.

## How it works

Describe your desired UI and get instant, working code.

**Example:**

```
Input: "A landing page hero section with a bold headline, a subheadline, and a CTA button"
```

```html
<section class="bg-gray-900 min-h-screen flex items-center justify-center p-8">
    <div class="max-w-3xl mx-auto text-center">
        <h1 class="text-5xl md:text-6xl font-bold mb-6 bg-gradient-to-r from-purple-400 to-pink-400 bg-clip-text text-transparent">Your Page Title</h1>
        <p class="text-xl md:text-2xl text-gray-400 mb-10">Your subtitle goes here</p>
        <button class="bg-purple-600 hover:bg-purple-700 text-white text-lg font-semibold py-4 px-10 rounded-full transition-all transform hover:scale-105">Get Started</button>
    </div>
</section>
```

Describes support: hero sections, pricing tables, feature grids. Each generated with Tailwind CSS and a dark, modern aesthetic.

## Run locally

Open `code/index.html` in any browser. No build step, no dependencies.

## Tech stack

- **Single HTML file** — zero build pipeline, fully portable
- **Vanilla JS** — no framework overhead, ~250 lines of logic
- **Tailwind CSS CDN** — utility-first styling via CDN (no build step)
- **Template-based generation** — parses natural language into structured component templates

## Related projects

- [bolt.new](https://bolt.new) — AI-powered full-stack dev environment
- [Lovable](https://lovable.dev) — AI frontend builder with editor
- [Replit](https://replit.com) — browser IDE with AI features

## Live

[![Deploy with Vercel](https://img.shields.io/badge/Live%20Site-Vercel-black)](https://code-five-mu.vercel.app)