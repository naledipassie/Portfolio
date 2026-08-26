#Naledi K. Tsotetsi — Civil Engineering Portfolio

A modern, responsive, single-page personal portfolio for an N6 Civil Engineering graduate
(Johannesburg, South Africa). Sections: Hero, About, Skills, Projects, Education,
Certifications, Experience, Contact and Footer.

## Tech stack

| Layer      | Choice                                                    |
| ---------- | --------------------------------------------------------- |
| Framework  | React 19 + TanStack Start (file-based routing, SSR-ready) |
| Build tool | Vite                                                      |
| Styling    | Tailwind CSS v4 (CSS-first config in `src/styles.css`)     |
| UI atoms   | shadcn-style components in `src/components/ui`             |
| Icons      | lucide-react                                              |
| Language   | TypeScript                                                |

No animation or carousel libraries are used: the on-scroll fade-in/slide-up effect is a
small `IntersectionObserver` hook (`src/hooks/use-reveal.ts`) plus two CSS utilities, and
navigation uses native CSS `scroll-behavior: smooth`.

## Design decisions

- **Palette** — deep navy (`#0B2545`-equivalent) primary for blueprint/trust, warm off-white
  page background (drawing paper), muted gold accent for highlights, steel grey for secondary
  text, dark charcoal body text. All tokens are defined once in `src/styles.css` using `oklch`
  and consumed as Tailwind utilities (`bg-primary`, `text-accent`, `text-steel`, …).
- **Typography** — Poppins for headings (strong, geometric, industry-appropriate) and Inter for
  body copy (highly readable at small sizes).
- **Layout** — mobile-first. Content is a single column below `md`, two columns from `md`, and
  three-column grids for cards from `lg`. CSS Grid handles section layouts, Flexbox handles
  toolbars, nav rows and pill lists.
- **Blueprint feel** — squared corners, thin rules, a subtle grid background on alternating
  section bands, and numbered section kickers (`01 / About`).

## Project structure

```
src/
  routes/
    __root.tsx        # HTML shell, fonts, base metadata
    index.tsx         # the portfolio page (composes all sections)
  components/portfolio/
    Navbar.tsx        # fixed nav + hamburger menu + Download CV
    Hero.tsx          # name, title, tagline, CTAs, location badge
    Section.tsx       # shared section shell (kicker + heading + intro)
    About.tsx  Skills.tsx  Projects.tsx  Education.tsx
    Certifications.tsx  Experience.tsx  Contact.tsx  Footer.tsx
  data/portfolio.ts   # all portfolio text/content in one place
  hooks/use-reveal.ts # scroll-reveal animation
  assets/             # hero + project images
public/
  Naledi-Tsotetsi-CV.pdf  # placeholder CV — replace with the real export
```

## Run locally

```bash
bun install     # or: npm install
bun run dev     # or: npm run dev  → http://localhost:8080
bun run build   # production build
```

## Personalising it

1. **Text** — edit `src/data/portfolio.ts` (name, intro, skills, education, certifications,
   experience, contact links). Set the real GitHub URL in `profile.github` / `profile.githubLabel`.
2. **CV** — replace `public/Naledi-Tsotetsi-CV.pdf` with the real PDF (keep the filename, or
   update `profile.cvUrl`).
3. **Projects** — `src/components/portfolio/Projects.tsx` carries a REPLACE comment. Swap the
   imported images in `src/assets/` for real photos/drawings and update each title, description
   and skill list (e.g. work from the Miner Construction holiday programme).
4. **Phone number** — optional; uncomment `profile.phone` and add it to the Contact details list.
5. **Contact form** — currently opens the visitor's mail client via `mailto:`. To use
   [Formspree](https://formspree.io) instead, replace the `onSubmit` handler in `Contact.tsx`
   with `action="https://formspree.io/f/YOUR_FORM_ID" method="POST"` (fields already have `name`
   attributes).

## Accessibility

Single `h1`, one `h2` per section, descriptive `alt` text (decorative images use `alt=""`),
visible focus styles, a skip link, `aria-expanded`/`aria-controls` on the hamburger button,
Escape closes the mobile menu, and `prefers-reduced-motion` disables animation and smooth scroll.

## Deployment

This app is a TanStack Start (Vite) project and is deployed by Lovable — press **Publish** in
the Lovable editor to go live, and connect a custom domain from Project → Settings → Domains.

If you also want to host it yourself from GitHub:

- **Vercel** — import the GitHub repo, framework preset "Vite"; build `npm run build`.
- **Netlify** — new site from Git; build command `npm run build`.
- GitHub Pages is only suitable for purely static output, so Vercel or Netlify is the better
  fit for this stack.

Push the source to a public GitHub repo (Lovable → GitHub → Connect) so the code and this
README are visible alongside the live site.
