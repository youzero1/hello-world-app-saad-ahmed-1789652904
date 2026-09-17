---
status: pending
title: Minimal Hello World App
---

Context: the repository currently contains only `README.md`. No application scaffold exists yet, so the plan covers creating the project skeleton and then the single Hello World page. No backend, database, or external data at any step.

1. Create `package.json` declaring an ESM (`"type": "module"`) Vite + React + TypeScript app with npm scripts `dev`, `build`, `preview`, and `typecheck`. Dependencies: `react`, `react-dom`, `@tanstack/react-router`. Dev dependencies: `vite`, `@vitejs/plugin-react`, `typescript`, `@types/react`, `@types/react-dom`, `tailwindcss`, `@tailwindcss/vite`, `@tanstack/router-plugin`. Outcome: `npm install` succeeds and the toolchain is pinned.

2. Create `vite.config.ts` registering, in order, the TanStack Router plugin from `@tanstack/router-plugin/vite` (file-based routing, routes directory `src/routes`, generated tree at `src/routeTree.gen.ts`), the React plugin, and the Tailwind plugin from `@tailwindcss/vite`. Add a resolve alias mapping `@` to the `src` directory. Outcome: dev server starts, Tailwind classes compile, and the route tree is auto-generated.

3. Create `tsconfig.json` (and `tsconfig.node.json` if needed for the Vite config) targeting modern ES output with `strict: true`, `jsx: "react-jsx"`, bundler module resolution, and `paths` mapping `@/*` to `src/*` so it matches the Vite alias. Outcome: `npm run typecheck` passes and `@/` imports resolve in the editor.

4. Create `index.html` at the repository root with a `#root` mount node, a `lang="en"` html tag, a viewport meta tag for correct mobile scaling, a descriptive `<title>` such as "Hello World", and a module script tag pointing at `src/main.tsx`. Outcome: Vite has a valid entry document.

5. Create `src/styles/global.css` whose first line is exactly `@import "tailwindcss";`. Keep the file otherwise empty apart from, at most, a base layer rule ensuring `html`, `body`, and `#root` fill the viewport height. Outcome: a single stylesheet powering all styling; no CSS Modules and no inline style objects anywhere in the app.

6. Create `src/main.tsx` that imports `@/styles/global.css` exactly once, imports the generated route tree from `@/routeTree.gen`, creates the router, registers the router type for type safety, and renders `RouterProvider` into `#root` inside `React.StrictMode`. Outcome: the app boots at `/` with routing active.

7. Create `src/routes/__root.tsx` as a deliberately minimal shell: a root route whose component renders a full-height container (`min-h-screen`, flex column) wrapping only `<Outlet />`. No nav bar, header, footer, logos, or demo links. Outcome: page content can center itself against the full viewport with no competing chrome.

8. Create `src/routes/index.tsx` as the home route for `/`. Layout: a full-viewport section that centers its content both horizontally and vertically, with a subtle neutral-to-tinted background gradient (e.g. slate/zinc tones) and horizontal gutter padding plus a constrained max width so text never touches the screen edges. Outcome: visiting `/` shows a single centered block of text.

9. Inside `src/routes/index.tsx`, render a single `<h1>` reading "Hello World" with a responsive type scale (roughly 4xl on mobile, 6xl at the `sm`/`md` breakpoint, 7xl at `lg`), tight tracking, bold weight, and a high-contrast foreground colour. Directly beneath it render a short muted subtitle paragraph (e.g. "Your app is up and running.") at a smaller size, lighter colour, with modest top margin and balanced/centred text. Outcome: a clear visual hierarchy between heading and subtitle at every breakpoint.

10. Ensure no starter-template leftovers exist anywhere: no Vite or React logo assets, no counter demo, no `App.tsx`/`App.css`/`index.css` boilerplate, no default `public/vite.svg`, and no unused imports. Delete any such file if the scaffolding step generated it. Outcome: the source tree contains only the files listed in this plan.

11. Verify the result: run the dev server and confirm `/` renders the centered greeting with the browser console free of errors and warnings; check the layout at mobile (~375px), tablet (~768px), and desktop (~1440px) widths for correct centering and type scale; confirm the network tab shows no API or data requests. Then run the typecheck and production build to confirm both succeed. Outcome: a clean, responsive, fully static Hello World app.
