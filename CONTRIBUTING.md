# Contributing to HealthOutline

Thanks for helping build HealthOutline, a free, plain-language guide to Ontario's healthcare system. This guide keeps everyone's work consistent. Please read it before your first change.

---

## 1. Getting set up

**You need:** Node.js **22.12 or newer** (`node -v` to check) and Git.

```sh
git clone https://github.com/atenahfr/healthoutline.git
cd healthoutline
npm install
npm run dev        # opens the site at http://localhost:4321
```

| Command           | What it does                                   |
| :---------------- | :--------------------------------------------- |
| `npm run dev`     | Live dev server; the page reloads as you edit  |
| `npm run build`   | Builds the final site into `dist/`             |
| `npm run preview` | Serves the `dist/` build locally for a check   |

**Editor:** VS Code is recommended. Accept the prompt to install the **Astro** extension (`astro-build.astro-vscode`).

---

## 2. How the project is organised

```
src/
  pages/        One file = one page. index.astro is the homepage (/).
  components/   One file = one section of a page (Header, Hero, Footer…).
  styles/
    global.css  Shared colours, fonts, and base styles for the whole site.
public/         Images and icons, served exactly as-is (e.g. /logo-icon.png).
```

- **New page?** Add it to `src/pages/`. The file name becomes the URL: `src/pages/coverage.astro` → `/coverage`. Nested folders work too: `src/pages/coverage/ohip.astro` → `/coverage/ohip`.
- **New section?** Add a component to `src/components/`, then import it into the page.
- **New image?** Put it in `public/` and reference it with a leading slash: `src="/my-image.png"`.

Don't commit `node_modules/`, `dist/`, `.astro/`, or `.env` files. `.gitignore` already covers them.

---

## 3. Branches

`main` is always the working, shareable version of the site. **Never commit directly to `main`.**

1. Update your copy first:
   ```sh
   git checkout main
   git pull
   ```
2. Create a branch for your change:
   ```sh
   git checkout -b <type>/<short-description>
   ```

| Type        | Use it for                           | Example                     |
| :---------- | :----------------------------------- | :-------------------------- |
| `feature/`  | A new page, section, or ability      | `feature/coverage-page`     |
| `fix/`      | Something broken or wrong            | `fix/footer-link-colour`    |
| `content/`  | Wording or copy changes only         | `content/ohip-faq-wording`  |
| `style/`    | Visual or design tweaks              | `style/hero-spacing-mobile` |
| `chore/`    | Setup, dependencies, config, docs    | `chore/update-astro`        |

Branch names are lowercase, with words joined by hyphens. Keep them short.

One branch = one topic. If you notice an unrelated problem, fix it on a separate branch.

---

## 4. Commit messages

We follow the style already used in this repo's history:

```
Add Canada flag badge to header
Redesign hero and triage sections with compass motif and hover interactions
Complete homepage: trust strip, pillars, programs teaser, and footer
```

### The rules

1. **Start with a capital-letter verb in the imperative form.** Write "Add", not "Added" or "Adds". A good test: *"If applied, this commit will ___."*
2. **Keep the first line to about 72 characters or fewer,** and don't end it with a period.
3. **Say what changed, and where.** "Fix footer link hover colour" is better than "Fix bug".
4. **Use a colon to list parts** when one commit touches several related things: `Complete homepage: trust strip, pillars, and footer`.
5. **Add a body when the *why* isn't obvious.** Leave a blank line after the first line, then explain.

### Common starting verbs

| Verb         | When                                    |
| :----------- | :-------------------------------------- |
| `Add`        | Something brand new                     |
| `Update`     | Change something that already exists    |
| `Fix`        | Correct a bug or mistake                |
| `Remove`     | Delete something                        |
| `Rename`     | Change a name without changing behaviour|
| `Redesign`   | Significant visual rework               |
| `Refactor`   | Restructure code, same result on screen |

### Examples

✅ Good

```
Add OHIP coverage page with eligibility checklist
Fix triage cards overflowing on small screens
Update footer disclaimer wording

Rename remaining HealthOrient references to HealthOutline

The browser tab title and package name still used the old name.
```

❌ Avoid

```
update stuff              ← vague, lowercase
Fixed the thing.          ← past tense, vague, period
WIP                       ← don't push work-in-progress commits to main
Add coverage page and fix header and change colours   ← three topics, split them
```

### Size

Make **small, focused commits**. Each commit should be one idea that still builds and runs. Several small commits are better than one giant commit.

---

## 5. Pull requests

1. Push your branch:
   ```sh
   git push -u origin <your-branch-name>
   ```
2. Open a Pull Request (PR) into `main` on GitHub.
3. **PR title:** same style as a commit message (e.g. `Add OHIP coverage page`).
4. **PR description:** fill in this template:

   ```markdown
   ## What changed
   - …

   ## Why
   - …

   ## How to check it
   - Run `npm run dev` and visit /…

   ## Screenshots
   (Before / after, for any visual change. Include a mobile width too.)
   ```

5. **At least one other collaborator reviews and approves** before merging.
6. After merging, delete the branch.

### Before you open a PR, check:

- [ ] `npm run build` finishes without errors
- [ ] The page looks right on desktop **and** at phone width (~375px)
- [ ] Hover effects still work, and nothing moves when "reduce motion" is on
- [ ] Every link goes somewhere real, or to a planned page listed in §7
- [ ] Brand name is spelled **HealthOutline** everywhere
- [ ] No medical advice was added (see §8)

---

## 6. Code style

Match the code that is already there. The rules below describe the existing style.

### Components (`.astro` files)

- **File names:** PascalCase, named after the section: `Header.astro`, `Programs.astro`.
- **Structure:** frontmatter (`---`) at the top, then HTML, then one `<style>` block at the bottom.
- **Repeated items live in a data list** in the frontmatter, and the HTML loops over it with `.map()`. See `Triage.astro`, `Pillars.astro`, and `Programs.astro`. Don't copy-paste the same card markup over and over.
- **Styles are scoped.** A component's `<style>` only affects that component, so keep each component's styles inside it.
- **Indentation:** 2 spaces.

### CSS

- **Use the shared colour variables** from `src/styles/global.css`. Never hard-code a new colour:

  | Variable   | Colour  | Used for                    |
  | :--------- | :------ | :-------------------------- |
  | `--navy`   | #0F2438 | Text, dark sections         |
  | `--teal`   | #1B7A88 | Buttons, links, highlights  |
  | `--green`  | #2F8F5B | Secondary accent            |
  | `--paper`  | #F4F7F6 | Page background, light text |
  | `--line`   | #D7E1DF | Borders and dividers        |

  If you truly need a new colour, add it as a variable in `global.css` and mention it in your PR.
- **Fonts:** `'Fraunces', serif` for headings and display text. `'Public Sans', sans-serif` (the body default) for everything else. Don't add new fonts without team agreement.
- **Class names:** lowercase with hyphens (`hero-cta`, `program-card`).
- **Hover and motion:** keep transitions short (`0.15s ease`). Always add a `@media (prefers-reduced-motion: reduce)` block that turns off movement. The existing components show how.
- **Small eyebrow labels** above headings use the existing pattern: 12px, bold, uppercase, `letter-spacing: 0.08em`.

### Accessibility

- Decorative images and SVGs get `alt=""` or `aria-hidden="true"`.
- Meaningful images get a real `alt` description.
- Links must have clear text, like "See upcoming workshops". Avoid "Click here".
- Keep text readable: don't place light text on light backgrounds.

---

## 7. Planned pages (URL map)

The homepage already links to these URLs. When you build one, use **exactly** this path so the existing links keep working:

| URL                              | Page                       |
| :------------------------------- | :------------------------- |
| `/get-started`                   | Get started ✅ built       |
| `/navigate-care`                 | Navigate Care hub          |
| `/navigate-care/dental`          | Dental care                |
| `/navigate-care/medical`         | Medical care               |
| `/navigate-care/new-to-ontario`  | New to Ontario             |
| `/navigate-care/find-a-doctor`   | Find a doctor              |
| `/navigate-care/mental-health`   | Mental health support      |
| `/coverage`                      | Coverage hub               |
| `/coverage/ohip`                 | OHIP / health card         |
| `/health-library`                | Health Library             |
| `/programs`                      | Programs hub               |
| `/programs/workshops`            | Free workshops             |
| `/programs/care-team`            | Meet the care team         |
| `/about`                         | About / How it works       |
| `/about/volunteer`               | Volunteer or partner       |

When you change or add a URL, update this table in the same PR.

---

## 8. Content and voice rules

HealthOutline helps people **find** care. It does **not provide** care. All written content must follow these rules:

- **No medical advice, diagnosis, or treatment.** Point people to the right service instead.
- **Plain language.** Use short sentences and everyday words. Explain acronyms the first time they appear (e.g. "OHIP (Ontario Health Insurance Plan)").
- **Warm and calm.** Many readers feel lost or stressed, so write the way a helpful friend would talk.
- **Ontario-specific.** Check that facts apply to Ontario, and link to official sources (ontario.ca, etc.) where possible.
- **Emergencies:** any page about urgent health topics must tell readers to call **911** in an emergency.
- **Spelling:** Canadian English (colour, centre, program).
- **Brand name:** always **HealthOutline**: one word, with a capital H and a capital O. Use lowercase `healthoutline` only in code identifiers such as the package name.

---

## 9. Staying in sync and fixing conflicts

- Pull `main` often, and bring it into your branch before opening a PR:
  ```sh
  git checkout main
  git pull
  git checkout <your-branch>
  git merge main
  ```
- **If you get a merge conflict:** open the file and look for the `<<<<<<<` and `>>>>>>>` markers. Keep the correct version and delete the markers. Then run `git add <file>` and `git commit`. If you're unsure, ask the person who wrote the other change.
- Never use `git push --force` on `main`.

---

## 10. Questions?

Open a GitHub issue or ask in the team chat. If you're unsure, ask. That's always better than guessing.
