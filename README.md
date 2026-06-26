# Portfolio med React, Vite og GitHub Pages

Denne guide hjælper dig med at lave en personlig portfolio, som kan ligge gratis online på GitHub Pages.

Du kommer til at bruge:

- React til komponenter og sider
- Vite til udvikling og build
- React Router til navigation
- GitHub Pages til hosting
- en simpel JSON-fil til dine projekter

Målet er ikke at lave den perfekte portfolio på første forsøg. Målet er at få en fungerende version online, som du derefter kan udvikle, designe og gøre personlig.

## Eksempler fra tidligere studerende

Her er eksempler på portfolioer, der bygger på samme type opsætning:

- [stinelock.github.io](https://stinelock.github.io/)
- [sofienholm.github.io](https://sofienholm.github.io/)
- [runedrummer81.github.io](https://runedrummer81.github.io/)

Kig på dem, før du designer din egen. Læg mærke til:

- hvordan forsiden præsenterer personen
- hvordan projekterne er organiseret
- hvordan navigationen fungerer
- hvor meget tekst der er på hvert projekt
- hvordan billeder, farver og typografi skaber en visuel identitet

Din portfolio skal ikke ligne de andres. Brug dem som inspiration til struktur, niveau og ambitionsretning.

## Før du starter

Guiden antager, at du allerede har:

- Node.js og `npm`
- VS Code
- en GitHub-konto

Du skal arbejde i terminalen, i VS Code og på GitHub undervejs.

## Overblik over processen

1. Opret et GitHub-repository med navnet `[dit-brugernavn].github.io`.
2. Klon repoet til din computer.
3. Opret et React-projekt med Vite.
4. Tilføj sider og navigation med React Router.
5. Tilføj dine projekter i en JSON-fil.
6. Byg projektet og deploy det til GitHub Pages.
7. Arbejd videre med design, indhold og detaljer.

## 1. Opret dit repository på GitHub

Opret et nyt repository på GitHub med navnet:

```text
[dit-brugernavn].github.io
```

Eksempel:

```text
cederdorff.github.io
```

Hvis dit GitHub-brugernavn er `sofieholm`, skal repoet altså hedde:

```text
sofieholm.github.io
```

Når repoet hedder præcis sådan, bliver din portfolio tilgængelig på:

```text
https://[dit-brugernavn].github.io
```

Eksempel:

```text
https://sofieholm.github.io
```

Vælg gerne:

- Public repository

## 2. Klon repoet og åbn det i VS Code

Kør i terminalen:

```bash
git clone https://github.com/[dit-brugernavn]/[dit-brugernavn].github.io.git
cd [dit-brugernavn].github.io
code .
```

Eksempel:

```bash
git clone https://github.com/sofieholm/sofieholm.github.io.git
cd sofieholm.github.io
code .
```

## 3. Opret React-projekt med Vite

Kør denne kommando inde i repo-mappen:

```bash
npm create vite@latest .
```

Vælg:

- Framework: `React`
- Variant: `JavaScript`

Hvis Vite spørger, hvad den skal gøre, fordi mappen ikke er tom:

- vælg at ignorere eksisterende filer og fortsætte

Installer derefter dependencies:

```bash
npm install
```

Start projektet:

```bash
npm run dev
```

Åbn den lokale URL i browseren. Den er typisk:

```text
http://localhost:5173
```

Checkpoint:

- Du kan se Vite/React-startsiden i browseren.
- Terminalen viser ingen fejl.
- Du kan stoppe serveren med `Ctrl + C`.

## 4. Ryd op i standardprojektet

Vite opretter lidt eksempelindhold, som du ikke behøver.

Du kan slette:

- `src/assets/react.svg`
- `public/vite.svg`

Du kan derefter forenkle:

- `src/App.jsx`
- `src/App.css`
- `src/index.css`

Det vigtigste er, at projektet stadig kan køre med:

```bash
npm run dev
```

## 5. Installer React Router

Installer React Router:

```bash
npm install react-router-dom
```

Opret en mappe til sider:

```bash
mkdir src/pages
```

Opret disse filer:

```text
src/pages/Home.jsx
src/pages/Projects.jsx
src/pages/ProjectDetail.jsx
src/pages/About.jsx
src/pages/Contact.jsx
```

## 6. Sæt routing op

GitHub Pages fungerer som statisk hosting. Derfor er `HashRouter` den nemmeste løsning til portfolios på GitHub Pages.

Med `HashRouter` får undersider adresser som:

```text
https://[dit-brugernavn].github.io/#/projects
https://[dit-brugernavn].github.io/#/projects/miniprojekt
```

Det ser lidt anderledes ud på grund af `#`, men det virker stabilt på GitHub Pages, også når man refresher siden eller deler et direkte link.

Opdater `src/main.jsx`:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import { HashRouter } from "react-router-dom";
import App from "./App";
import "./index.css";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <HashRouter>
      <App />
    </HashRouter>
  </StrictMode>
);
```

Opdater `src/App.jsx`:

```jsx
import { NavLink, Route, Routes } from "react-router-dom";
import Home from "./pages/Home";
import Projects from "./pages/Projects";
import ProjectDetail from "./pages/ProjectDetail";
import About from "./pages/About";
import Contact from "./pages/Contact";

function App() {
  return (
    <>
      <header className="site-header">
        <NavLink to="/" className="logo">
          Mit navn
        </NavLink>

        <nav className="site-nav">
          <NavLink to="/" end>
            Forside
          </NavLink>
          <NavLink to="/projects">Projekter</NavLink>
          <NavLink to="/about">Om mig</NavLink>
          <NavLink to="/contact">Kontakt</NavLink>
        </nav>
      </header>

      <main>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/projects" element={<Projects />} />
          <Route path="/projects/:id" element={<ProjectDetail />} />
          <Route path="/about" element={<About />} />
          <Route path="/contact" element={<Contact />} />
        </Routes>
      </main>
    </>
  );
}

export default App;
```

## 7. Lav de første sider

Start med en simpel version. Du kan altid gøre den pænere bagefter.

`src/pages/Home.jsx`:

```jsx
function Home() {
  return (
    <section className="page">
      <p className="eyebrow">Portfolio</p>
      <h1>Hej, jeg hedder Dit Navn.</h1>
      <p>
        Jeg arbejder med frontend, design og digitale produkter. Her kan du se nogle af de projekter, jeg har lavet.
      </p>
    </section>
  );
}

export default Home;
```

`src/pages/About.jsx`:

```jsx
function About() {
  return (
    <section className="page">
      <h1>Om mig</h1>
      <p>Skriv kort om, hvem du er, hvad du er nysgerrig på, og hvilke typer projekter du gerne vil arbejde med.</p>
    </section>
  );
}

export default About;
```

`src/pages/Contact.jsx`:

```jsx
function Contact() {
  return (
    <section className="page">
      <h1>Kontakt</h1>
      <p>Du kan kontakte mig på mail eller finde mig på GitHub og LinkedIn.</p>
      <ul>
        <li>
          <a href="mailto:dinmail@example.com">dinmail@example.com</a>
        </li>
        <li>
          <a href="https://github.com/[dit-brugernavn]">GitHub</a>
        </li>
      </ul>
    </section>
  );
}

export default Contact;
```

Checkpoint:

- Navigationen virker lokalt.
- Du kan gå til forsiden, projekter, om mig og kontakt.
- URL'en ændrer sig, når du klikker rundt.

## 8. Tilføj projektdata

Opret filen:

```text
public/projects.json
```

Indsæt eksempeldata:

```json
[
  {
    "id": "portfolio",
    "title": "Portfolio Website",
    "year": 2026,
    "description": "Min personlige portfolio bygget med React, Vite og GitHub Pages.",
    "details": "I dette projekt har jeg arbejdet med komponenter, routing, JSON-data, responsive layouts og deployment.",
    "tags": ["React", "Vite", "GitHub Pages"],
    "image": "img/portfolio.webp",
    "links": [
      {
        "url": "https://[dit-brugernavn].github.io",
        "text": "Live site"
      },
      {
        "url": "https://github.com/[dit-brugernavn]/[dit-brugernavn].github.io",
        "text": "GitHub repo"
      }
    ]
  }
]
```

Læg billeder i:

```text
public/img/
```

Brug korte filnavne uden mellemrum:

```text
portfolio.webp
todo-app.webp
weather-app.webp
```

God praksis:

- Brug `webp`, `jpg` eller `png`.
- Gør billederne mindre, før du lægger dem i projektet.
- Brug samme format og nogenlunde samme proportioner til projektbilleder.
- Undgå filnavne som `Skærmbillede 2026-01-21 kl. 14.03.22.png`.

## 9. Vis projekter fra JSON

Opdater `src/pages/Projects.jsx`:

```jsx
import { useEffect, useState } from "react";
import { Link } from "react-router-dom";

function Projects() {
  const [projects, setProjects] = useState([]);

  useEffect(() => {
    async function getProjects() {
      const response = await fetch(`${import.meta.env.BASE_URL}projects.json`);
      const data = await response.json();
      setProjects(data);
    }

    getProjects();
  }, []);

  return (
    <section className="page">
      <h1>Projekter</h1>

      <div className="project-grid">
        {projects.map((project) => (
          <article className="project-card" key={project.id}>
            <img src={`${import.meta.env.BASE_URL}${project.image}`} alt={`Screenshot af ${project.title}`} />
            <div>
              <p className="eyebrow">{project.year}</p>
              <h2>{project.title}</h2>
              <p>{project.description}</p>
              <Link to={`/projects/${project.id}`}>Se projekt</Link>
            </div>
          </article>
        ))}
      </div>
    </section>
  );
}

export default Projects;
```

Opdater `src/pages/ProjectDetail.jsx`:

```jsx
import { useEffect, useState } from "react";
import { Link, useParams } from "react-router-dom";

function ProjectDetail() {
  const { id } = useParams();
  const [project, setProject] = useState(null);

  useEffect(() => {
    async function getProject() {
      const response = await fetch(`${import.meta.env.BASE_URL}projects.json`);
      const data = await response.json();
      const selectedProject = data.find((item) => item.id === id);
      setProject(selectedProject);
    }

    getProject();
  }, [id]);

  if (!project) {
    return (
      <section className="page">
        <h1>Projektet blev ikke fundet</h1>
        <Link to="/projects">Tilbage til projekter</Link>
      </section>
    );
  }

  return (
    <section className="page project-detail">
      <Link to="/projects">Tilbage til projekter</Link>

      <img src={`${import.meta.env.BASE_URL}${project.image}`} alt={`Screenshot af ${project.title}`} />
      <p className="eyebrow">{project.year}</p>
      <h1>{project.title}</h1>
      <p>{project.details}</p>

      <ul className="tag-list">
        {project.tags.map((tag) => (
          <li key={tag}>{tag}</li>
        ))}
      </ul>

      <div className="project-links">
        {project.links.map((link) => (
          <a href={link.url} key={link.url}>
            {link.text}
          </a>
        ))}
      </div>
    </section>
  );
}

export default ProjectDetail;
```

Checkpoint:

- Projekterne vises på `/projects`.
- Hvert projekt linker til sin egen detaljeside.
- Billederne loader både lokalt og efter deploy.
- Hvis du ændrer `projects.json`, ændrer indholdet sig på sitet.

## 10. Tilføj en enkel CSS-start

Du kan starte med global CSS i `src/index.css`:

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family:
    system-ui,
    -apple-system,
    BlinkMacSystemFont,
    "Segoe UI",
    sans-serif;
  color: #1f2933;
  background: #f7f4ef;
}

a {
  color: inherit;
}

img {
  display: block;
  max-width: 100%;
}

.site-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  padding: 1rem clamp(1rem, 5vw, 4rem);
  border-bottom: 1px solid #ded8cf;
}

.logo {
  font-weight: 700;
  text-decoration: none;
}

.site-nav {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.site-nav a {
  text-decoration: none;
}

.site-nav a.active {
  text-decoration: underline;
  text-underline-offset: 0.35rem;
}

.page {
  width: min(100% - 2rem, 1100px);
  margin: 0 auto;
  padding: 4rem 0;
}

.eyebrow {
  margin: 0 0 0.5rem;
  color: #6b7280;
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
}

.project-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1.5rem;
}

.project-card {
  overflow: hidden;
  border: 1px solid #ded8cf;
  border-radius: 0.75rem;
  background: #fffaf3;
}

.project-card div {
  padding: 1rem;
}

.project-card img {
  width: 100%;
  aspect-ratio: 16 / 10;
  object-fit: cover;
}

.project-detail img {
  width: 100%;
  max-height: 520px;
  object-fit: cover;
  border-radius: 0.75rem;
  margin-bottom: 2rem;
}

.tag-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  padding: 0;
  list-style: none;
}

.tag-list li {
  padding: 0.35rem 0.7rem;
  border: 1px solid #ded8cf;
  border-radius: 999px;
  background: white;
}

.project-links {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}
```

Denne CSS er kun et udgangspunkt. Når setuppet virker, bør du ændre farver, typografi, spacing og layout, så portfolioen passer til dig.

## 11. Deploy til GitHub Pages

Installer deployment-pakken:

```bash
npm install -D gh-pages
```

Opdater `package.json`, så `scripts` indeholder:

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"
  }
}
```

Opdater `vite.config.js`:

```js
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  base: "/"
});
```

Når repoet hedder `[brugernavn].github.io`, skal `base` være:

```js
base: "/";
```

Hvis du senere deployer et andet projekt til et almindeligt repo, skal `base` typisk være:

```js
base: "/repo-navn/";
```

Byg projektet lokalt:

```bash
npm run build
```

Test buildet:

```bash
npm run preview
```

Hvis det virker, så commit og push din kildekode:

```bash
git add .
git commit -m "Add React portfolio"
git push origin main
```

Deploy derefter den byggede version:

```bash
npm run deploy
```

Gå derefter til GitHub:

```text
Repository -> Settings -> Pages
```

Vælg:

```text
Source: Deploy from a branch
Branch: gh-pages
Folder: / (root)
```

Når GitHub er færdig, ligger portfolioen på:

```text
https://[dit-brugernavn].github.io
```

Det kan tage et par minutter, før ændringerne er synlige.

## 12. Når du vil opdatere portfolioen

Hver gang du har lavet ændringer, som skal online:

```bash
npm run build
git add .
git commit -m "Update portfolio"
git push origin main
npm run deploy
```

`npm run deploy` bygger også projektet automatisk via `predeploy`, men det er en god vane at køre `npm run build` først, så du opdager fejl, før du deployer.

Kort sagt:

- `main` indeholder din kildekode.
- `gh-pages` indeholder den byggede version, som GitHub Pages viser online.

Du arbejder normalt kun i `main`. `gh-pages` bliver håndteret af `npm run deploy`.

## Typiske fejl og fixes

### Siden er blank efter deploy

Tjek:

- at `vite.config.js` har `base: "/"`
- at du har kørt `npm run deploy`
- at GitHub Pages bruger branch `gh-pages`
- at browserens console ikke viser fejl om manglende `.js`- eller `.css`-filer

### Billeder vises lokalt, men ikke online

Tjek:

- at billeder ligger i `public/img`
- at filnavne matcher præcist, inklusive store og små bogstaver
- at stier i JSON ikke starter med `/`

Brug:

```json
"image": "img/portfolio.webp"
```

Ikke:

```json
"image": "/img/portfolio.webp"
```

### Undersider giver 404 efter refresh

Brug `HashRouter` i `src/main.jsx`.

Hvis du bruger `BrowserRouter`, skal du lave ekstra fallback-opsætning til GitHub Pages. Det er ikke nødvendigt i denne guide.

### Ændringer kommer ikke online

Husk at:

```bash
npm run deploy
```

skal køres igen, hver gang en ny version skal publiceres.

### `npm run deploy` fejler

Prøv først:

```bash
npm run build
```

Hvis build fejler, skal fejlen rettes, før du kan deploye.

## Hvad en god portfolio bør indeholde

Minimum:

- en tydelig forside med navn og faglig retning
- en projektside med flere projekter
- en detaljeside for hvert projekt
- en kort om-mig-side
- kontaktoplysninger
- links til GitHub og eventuelt LinkedIn

Gode projektsider svarer ofte på:

- Hvad er projektet?
- Hvorfor lavede du det?
- Hvilke teknologier brugte du?
- Hvad var din rolle?
- Hvad lærte du?
- Hvad ville du forbedre næste gang?

## Forslag til videre arbejde

Når den første version virker, kan du arbejde videre med:

- bedre visuel identitet
- responsivt design til mobil
- dark mode
- filtrering af projekter efter tags
- animationer og mikrointeraktioner
- bedre billeder og projektbeskrivelser
- SEO med god titel og meta-description
- accessibility med semantisk HTML, alt-tekster og god kontrast

Start simpelt, få det online, og byg derefter videre. En portfolio bliver god gennem iteration.
