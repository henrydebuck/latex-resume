# latex-resume

A clean, modular LaTeX template for generating a professional one-or-two-page CV.  
See [`example/cv_sample.pdf`](example/cv_sample.pdf) for a compiled preview.

---

## Project structure

```
latex-resume/
├── main.tex                  # Entry point — assembles the CV
├── style/
│   └── cv.sty                # All styling and custom commands
├── sections/
│   ├── projects.tex
│   ├── skills.tex
│   ├── experience.tex
│   ├── education.tex
│   ├── certifications.tex
│   └── languages.tex
├── data/
│   └── template.tex          # Personal data — rename & fill in
├── example/
│   └── cv_sample.pdf         # Pre-compiled example
└── .gitignore
```

---

## Quick start

### 1. Prerequisites

Install a LaTeX distribution that includes `fontawesome5`:

| OS | Recommended |
|---|---|
| Linux | TeX Live (`texlive-full`) |
| macOS | MacTeX |
| Windows | MiKTeX |

### 2. Set up your personal data

```bash
cp data/template.tex data/mydata.tex
```

Open `data/mydata.tex` and fill in your details:

```latex
\newcommand{\cvName}{First Last}
\newcommand{\cvEmail}{you@example.com}
\newcommand{\cvPhone}{+32 XXX XX XX XX}
\newcommand{\cvPostalCode}{1000}
\newcommand{\cvCity}{Brussels}

\newcommand{\cvWebsite}{https://yoursite.com}
\newcommand{\cvWebsiteLabel}{yoursite.com}
\newcommand{\cvLinkedin}{yourhandle}   % handle only, not full URL
\newcommand{\cvGithub}{yourhandle}
```

> Leave `\cvWebsite{}`, `\cvLinkedin{}` or `\cvGithub{}` **empty** to hide them.

### 3. Edit the sections

Each file in `sections/` corresponds to one CV section.  
Edit them directly with your own content using the commands below.

### 4. Point `main.tex` to your data

Open `main.tex` and change:

```latex
\input{data/template}   >>>   \input{data/mydata}
```

### 5. Compile

```bash
pdflatex main.tex
```

Run twice if the page count changes (footer needs two passes).

---

## Available commands

### Header

Automatically built from your `data/*.tex` variables — no changes needed in `main.tex`.

### `\cvproject{title}{year}{summary}{technologies}`

| Argument | Required | Notes |
|---|---|---|
| `title` | ✅ | Project name |
| `year` | ❌ | Pass `{}` to omit |
| `summary` | ✅ | One or two sentences |
| `technologies` | ✅ | Comma-separated list |

```latex
\cvproject
  {My Project}
  {2024}
  {A short description of what the project does and its impact.}
  {Python, FastAPI, PostgreSQL}
```

### `\cvskill{name}{description}`

| Argument | Required | Notes |
|---|---|---|
| `name` | ✅ | Displayed in bold |
| `description` | ❌ | Pass `{}` to omit |

Wrap multiple `\cvskill` calls in `\begin{cvlist} ... \end{cvlist}`.

```latex
\begin{cvlist}
  \cvskill{Python}{pandas, numpy, scikit-learn}
  \cvskill{DevOps}{Docker, Kubernetes, GitLab CI}
\end{cvlist}
```

### `\cvexperience{title}{company, location}{start}{end}{description}`

```latex
\cvexperience
  {Software Engineer}
  {Acme Corp, Brussels (Belgium)}
  {March 2023}
  {Present}
  {Description of responsibilities and achievements.}
```

### `\cveducation{name}{date}{description}`

| Argument | Required | Notes |
|---|---|---|
| `name` | ✅ | Institution or degree |
| `date` | ✅ | e.g. `September 2020 – June 2023` |
| `description` | ❌ | Pass `{}` to omit |

```latex
\cveducation
  {University of Liège, Liège (Belgium)}
  {September 2020 – June 2023}
  {Bachelor's degree in Computer Science}
```

### `\cvcertification{name}{issuer, date}{description}`

```latex
\cvcertification
  {AWS Solutions Architect}
  {Amazon, January 2024}
  {}
```

### `\cvlanguage{language}{level}`

Wrap multiple `\cvlanguage` calls in `\begin{cvlist} ... \end{cvlist}`.

```latex
\begin{cvlist}
  \cvlanguage{French}{Native}
  \cvlanguage{English}{Advanced}
\end{cvlist}
```

---

## Customisation tips

- **Section order** — reorder or comment out `\input{sections/...}` lines in `main.tex`.
- **Hide a section** — comment out its `\input` line.
- **Margins** — adjust `geometry` in `style/cv.sty`.
- **Accent colour** — change `cvgray` / `cvrule` in `style/cv.sty`.

---

## License

MIT — free to use, adapt, and share.
