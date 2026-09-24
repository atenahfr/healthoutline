# HealthOutline

Free, plain-language health system navigation for Ontario.

HealthOutline helps people find their way through Ontario's healthcare system. That includes getting a health card (OHIP), finding a family doctor, understanding coverage, and reaching mental health support. We help people **find** care. We don't provide medical advice, diagnosis, or treatment.

Built with [Astro](https://astro.build).

## Getting started

Requires **Node.js 22.12+**.

```sh
npm install
npm run dev        # http://localhost:4321
```

| Command           | What it does                                  |
| :---------------- | :-------------------------------------------- |
| `npm run dev`     | Start the local dev server                    |
| `npm run build`   | Build the production site into `dist/`        |
| `npm run preview` | Preview the production build locally          |

## Project structure

```
src/
  pages/         One file per page (index.astro is the homepage)
  components/    Page sections: Header, Hero, Triage, Trust, Pillars, Programs, Footer
  styles/
    global.css   Shared colours, fonts, and base styles
public/          Logo, favicons, and other static files
```

## Contributing

Please read **[CONTRIBUTING.md](CONTRIBUTING.md)** before making changes. It covers branch names, commit messages, pull requests, code style, and content rules.

---

*HealthOutline does not provide medical advice. In an emergency, call 911.*
