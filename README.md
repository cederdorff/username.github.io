# React Portfolio Template

En simpel React + Vite portfolio-template, du kan bruge til at komme godt i gang med dit portfolioprojekt. Projektet deployes automatisk til GitHub Pages, når der pushes til `main`.

Templaten er lavet til repositories med navnet:

```text
[brugernavn].github.io
```

Det betyder, at portfolioen kommer til at ligge på:

```text
https://[brugernavn].github.io
```

## Hvad projektet indeholder

- React 19 + Vite 8
- React Router (`react-router`)
- Sider til forside, projekter, projektdetalje, om mig, kontakt og 404
- Projektdata i `src/data/projects.js`
- GitHub Actions deployment i `.github/workflows/deploy.yml`
- GitHub Pages fallback via `dist/404.html`

## Eksempler fra tidligere studerende

Når portfolioen er deployet, kommer den til at ligge på:

```text
https://[brugernavn].github.io
```

Her er eksempler på tidligere studerendes deployede portfolioer:

- [stinelock.github.io](https://stinelock.github.io/)
- [sofienholm.github.io](https://sofienholm.github.io/)
- [runedrummer81.github.io](https://runedrummer81.github.io/)

Eksemplerne viser, hvordan URL'en ser ud, når sitet er publiceret med GitHub Pages.

## Før du starter

Guiden antager, at du allerede har:

- Node.js og `npm`
- VS Code
- GitHub Desktop
- en GitHub-konto

## 1. Opret repository på GitHub

Opret et nyt repository på GitHub.

Repository-navnet skal være dit GitHub-brugernavn efterfulgt af `.github.io`:

```text
[brugernavn].github.io
```

Hvis dit GitHub-brugernavn er `sofieholm`, skal repository-navnet være:

```text
sofieholm.github.io
```

Vælg:

- `Public`

Klik derefter på `Create repository`.

## 2. Klon med GitHub Desktop

Når repositoryet er oprettet:

1. Gå ind på dit nye repository på GitHub.
2. Kontroller, at repository-navnet er fuldstændig magen til dit GitHub-brugernavn efterfulgt af `.github.io`.
3. Klik på den grønne `Code`-knap.
4. Vælg `Open with GitHub Desktop`.
5. Vælg, hvor projektmappen skal ligge på din computer.
6. Klik på `Clone`.
7. Klik på `Open in Visual Studio Code` i GitHub Desktop.

Eksempel:

```text
sofieholm.github.io
```

Hvis dit brugernavn er `sofieholm`, må repoet ikke hedde:

```text
portfolio
sofie-portfolio
sofieholm
sofieholm.github
```

Fra nu af arbejder du i VS Code. GitHub Desktop bruges til at committe og pushe ændringer.

## 3. Opret React-projekt med Vite

Åbn terminalen i VS Code:

```text
Terminal -> New Terminal
```

Kør denne kommando:

```bash
npm create vite@latest .
```

Vigtigt: punktummet til sidst skal med.

Punktummet betyder, at Vite skal oprette React-projektet i den mappe, du allerede står i. Hvis du glemmer punktummet, kan du komme til at oprette en ekstra mappe inde i portfolio-mappen.

Når Vite spørger, skal du vælge:

```text
Ok to proceed? y
Current directory is not empty: Ignore files and continue
Framework: React
Variant: JavaScript
Use ESLint instead of Oxlint? No (Oxlint)
Install with npm and start now? Yes
```

Hvis du vælger `Yes` til `Install with npm and start now?`, installerer Vite dependencies og starter udviklingsserveren automatisk.

Hvis du vælger `No`, skal du selv køre:

```bash
npm install
npm run dev
```

Åbn den lokale URL i browseren. Den er typisk:

```text
http://localhost:5173
```

Når du kan se Vite-startsiden, virker projektet.

Stop udviklingsserveren igen med:

```text
Ctrl + C
```

## 4. Installer React Router

Installer React Router:

```bash
npm install react-router
```

## 5. Ryd op i Vite-standardprojektet

Vite opretter en startside med demo-indhold. Det skal ryddes væk, så portfolioen starter simpelt.

Slet disse filer og mapper, hvis de findes:

```text
src/assets/
src/App.css
public/icons.svg
public/vite.svg
```

Behold disse filer, fordi de skal ændres senere:

```text
src/App.jsx
src/main.jsx
src/index.css
index.html
vite.config.js
package.json
```

## 6. Opret portfolio-strukturen

Opret disse mapper:

```text
.github/workflows/
src/components/
src/data/
src/pages/
```

Du kan oprette dem i VS Code ved at højreklikke i filoversigten og vælge `New Folder`.

Du kan også oprette dem i terminalen:

```bash
mkdir -p .github/workflows src/components src/data src/pages
```

## 7. Opret og erstat filer

Når du har ryddet op, skal projektet ende med filerne herunder.

Opret disse nye filer:

```text
.github/workflows/deploy.yml
public/portfolio-placeholder.svg
src/components/Navbar.jsx
src/data/projects.js
src/pages/HomePage.jsx
src/pages/ProjectsPage.jsx
src/pages/ProjectPage.jsx
src/pages/AboutPage.jsx
src/pages/ContactPage.jsx
src/pages/NotFoundPage.jsx
```

Erstat indholdet i disse eksisterende filer:

```text
src/App.jsx
src/main.jsx
src/index.css
index.html
vite.config.js
```

Vigtigt:

- `src/App.jsx` skal ikke længere importere `useState`, React-logoer eller `App.css`.
- `src/main.jsx` skal importere `BrowserRouter` fra `react-router`.
- `src/index.css` bliver den globale CSS-fil for hele portfolioen.
- `.github/workflows/deploy.yml` sørger for automatisk deployment til GitHub Pages.

## 8. Test projektet lokalt

Start udviklingsserveren:

```bash
npm run dev
```

Tjek disse sider i browseren:

```text
http://localhost:5173/
http://localhost:5173/projects
http://localhost:5173/projects/portfolio
http://localhost:5173/about
http://localhost:5173/contact
```

## Scripts

```bash
npm run dev      # start lokal udviklingsserver
npm run build    # lav production build
npm run preview  # test production build lokalt
npm run lint     # kør Oxlint
```

## Projektstruktur efter oprydning

```text
.github/
  workflows/
    deploy.yml
public/
  portfolio-placeholder.svg
src/
  components/
    Navbar.jsx
  data/
    projects.js
  pages/
    HomePage.jsx
    ProjectsPage.jsx
    ProjectPage.jsx
    AboutPage.jsx
    ContactPage.jsx
    NotFoundPage.jsx
  App.jsx
  main.jsx
  index.css
```

Hvis du stadig har `src/assets/`, `src/App.css` eller Vite-demoindhold i `src/App.jsx`, er oprydningen ikke færdig.

## Routing

Routes er defineret i `src/App.jsx`:

```text
/                  -> HomePage
/projects          -> ProjectsPage
/projects/:slug    -> ProjectPage
/about             -> AboutPage
/contact           -> ContactPage
*                  -> NotFoundPage
```

Portfolioen får URL'er som:

```text
https://[brugernavn].github.io/projects
https://[brugernavn].github.io/projects/portfolio
```

For at refresh og direkte links til undersider virker på GitHub Pages, kopierer workflowet automatisk `dist/index.html` til `dist/404.html` efter build.

## Projektdata

Projekterne ligger i:

```text
src/data/projects.js
```

Tilføj, fjern eller ret projekter i arrayet:

```js
{
  slug: "portfolio",
  title: "Portfolio",
  year: "2026",
  summary: "Kort tekst til projektkortet.",
  description: "Længere tekst til projektsiden.",
  tags: ["React", "Vite", "GitHub Pages"],
  image: `${import.meta.env.BASE_URL}portfolio-placeholder.svg`,
  links: [
    {
      label: "Live site",
      href: "https://brugernavn.github.io",
    },
  ],
}
```

`slug` bruges i URL'en. Hvis `slug` er `"portfolio"`, bliver projektets URL:

```text
/projects/portfolio
```

## Deployment til GitHub Pages

Deployment styres af:

```text
.github/workflows/deploy.yml
```

Workflowet kører automatisk, når der pushes til `main`.

Det gør fire ting:

1. Installerer dependencies med `npm ci`.
2. Bygger projektet med `npm run build`.
3. Kopierer `dist/index.html` til `dist/404.html`, så React Router virker på refresh.
4. Deployer `dist` til GitHub Pages.

Første gang skal GitHub Pages sættes til GitHub Actions:

```text
Repository -> Settings -> Pages -> Source -> GitHub Actions
```

Når det er gjort, deployer siden automatisk ved hvert push til `main`.

## Når du vil opdatere portfolioen

1. Ret indhold eller kode i VS Code.
2. Test lokalt med `npm run dev`.
3. Kør gerne `npm run build`, så du opdager fejl før push.
4. Commit og push ændringerne med GitHub Desktop.
5. GitHub Actions deployer automatisk til GitHub Pages.

## Tilpasning

Start her:

- Ret navn og navigation i `src/components/Navbar.jsx`.
- Ret forsidetekst i `src/pages/HomePage.jsx`.
- Ret projekter i `src/data/projects.js`.
- Ret farver, typografi og layout i `src/index.css`.
- Ret kontaktlinks i `src/pages/ContactPage.jsx`.

Hold første version simpel. Få den online, og byg derefter videre.
