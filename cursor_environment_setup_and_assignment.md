# Environment setup and assignment
_Exported on 9/2/2026 at 16:51:17 CDT from Cursor (3.18.9)_

---

**User**

I have successfully set up the environment.

Next step is to :
@README.md (54-55) 

After that, verify that I'm truly done.


---

**Cursor**

I'll read the assignment README and project files, then check the GitHub Pages setup.

Dev server is up. Next I’ll inspect the repo remote, Pages config, and starter HTML/CSS so we can confirm setup and leave clear fill-in spots.

The clone is still pointed at the class repo, not a personal `mp0`. I’ll inspect the starter files and GitHub account next so we can confirm Pages and scaffold the card.

Local setup looks fine, but `origin` still points at the class repo, so Pages can’t be turned on yet.

GitHub Pages is **not done yet**, so setup is not finished.

## GitHub Pages — blocked

Your local folder still points at the **class** repo, not your own:

`origin` → `https://github.com/cs409-fa25/cs409mp0.git`

You cannot change Pages settings on that repo. The README “Use this template” button is also missing on the class repo, so create your own public repo and push to it.

Do this in your browser (you need to be signed into GitHub):

1. Open [github.com/new](https://github.com/new).
2. Repository name: `mp0`.
3. Set it to **Public**.
4. Do **not** check “Add a README”.
5. Create the repository.

Then in a terminal, from `cs409mp0`:

```powershell
git remote rename origin class-starter
git remote add origin https://github.com/<your-github-username>/mp0.git
git push -u origin main
```

Then on **your** repo:

**Settings → Pages → Build and deployment → Source → GitHub Actions**

Also add course staff as collaborators (README requires this for grading). After the first push, the site should appear at `https://<your-github-username>.github.io/mp0` (sometimes 10–30 minutes).

Send me your GitHub username after you create `mp0` and I can check that Pages is actually set to GitHub Actions.

## Setup check

| Step | Status |
|---|---|
| Node.js + git | Done |
| `npm install` + `npm start` | Done |
| `http://localhost:8080/` loads | Done |
| Own public `mp0` repo | **Not done** — still on the class repo |
| Pages source = GitHub Actions | **Not done** |

---

**User**

Okay I have filled it in. Am I done with this assignment and I should get ready to commit/push to github (and anything else we need to do to finish)?

---

**Cursor**

I’ll check your filled-in page against the README requirements, then confirm whether git remotes, Pages, and the other submission steps are actually ready.

Content looks filled in. I’ll load the live page and check whether `extramediumdev` already has a public `mp0` repo and Pages set up.

The **page itself is done**. You are **not** ready to commit/push yet, and the assignment is **not** finished.

I checked `http://localhost:8080/`: name, GitHub link, bio, and photo are filled in. Required tags (`img`, `h1`, `a`, `p`), 150×150 image, centered layout, colored card on white, and no inline styles are all in place.

What is still missing:

**1. You do not have your own `mp0` repo.**  
`origin` is still `https://github.com/cs409-fa25/cs409mp0.git`.  
`https://github.com/ExtraMediumDev/mp0` does not exist. If you push now, it will try to push into the class repo, which will fail (and would be the wrong place anyway).

Create a **public** repo named `mp0` (no README), then:

```powershell
git remote rename origin class-starter
git remote add origin https://github.com/ExtraMediumDev/mp0.git
```

**2. Then commit and push** to *your* repo:

```powershell
git add src/index.html src/css/main.css src/assets/image.jpg
git commit -m "Add personal profile card for MP0"
git push -u origin main
```

I will not commit until you say to.

**3. GitHub Pages** on *your* repo:  
Settings → Pages → Build and deployment → Source → **GitHub Actions**

Wait for the Action to finish. Site URL should be `https://extramediumdev.github.io/mp0`.

**4. Add course staff as collaborators** so they can grade.

**5. LLM log** — `llm_logs.csv` still has the dummy example links. This chat generated the starter CSS/HTML, so the course policy says to put the chat log link in that file and submit it with the form.

**6. After the site is live**, submit the [course form](https://forms.gle/Gk1BxfsZ5K7sZpZZ6).

Create the `mp0` repo and tell me when it’s up. I can re-point `origin`, and then we can commit/push if you want.

---

# ChatGPT logs

---

**User**

why doesn't the picture render?

---

**ChatGPT**

In this project the HTML is copied from `src/index.html` into `build/`, and images are copied from `src/assets/` to `build/assets/`. The `<img>` path has to match that.

Use a relative path (no leading `/`):

```html
<img src="assets/image.jpg" alt="Brian Li">
```

Then make sure the actual file exists at:

`src/assets/image.jpg`

If you put the photo somewhere else (Desktop, `src/image.jpg`, etc.), it will not show. Keep the filename `image.jpg`, or change the `src` to match the new name.

After replacing the file:

1. Save `src/index.html`.
2. Hard-refresh the browser (`Ctrl+Shift+R`) on `http://localhost:8080/`.
3. Confirm `npm start` is still running.

Do not set width/height on the `<img>` tag itself — the assignment forbids inline styles. Size it in `src/css/main.css` instead (`width` and `height` of `150px`).

---

**User**

How do I center and make the card grey? Generate me the meta tags to put above title

---

**ChatGPT**

Put all of this in `src/css/main.css` (not in the HTML). Center the card on a white page and give the card a gray background:

```css
body {
  margin: 0;
  min-height: 100vh;
  background-color: #ffffff;
  display: flex;
  justify-content: center;
  align-items: center;
}

.card {
  background-color: #4a4a4a;
  width: 520px;
  padding: 48px 56px;
  color: #ffffff;
}

img {
  display: block;
  width: 150px;
  height: 150px;
  margin: 0 auto 24px;
}

h1,
a {
  text-align: center;
}

a {
  display: block;
}
```

`display: flex` + `justify-content: center` + `align-items: center` on `body` centers the card on the page. `margin: 0 auto` on the image centers the photo inside the card. `text-align: center` centers the heading and link.

Meta tags go in `<head>`, above `<title>`:

```html
<head>
  <meta charset="utf-8">
  <meta http-equiv="x-ua-compatible" content="ie=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MP 0</title>
</head>
```

Those are the same tags the starter already includes. You do not need extra meta tags for this assignment.

---

**User**

do I include bundle.js

---

**ChatGPT**

Yes. Keep this line at the bottom of `src/index.html`, inside `<body>`:

```html
<script src="bundle.js" type="text/javascript"></script>
```

Webpack builds your CSS (`src/css/main.css`) and JS into `bundle.js`. If you remove that script tag, the page will still show HTML, but none of the CSS from `main.css` will apply, so the gray card, centering, and 150px image size will disappear.

That is a webpack script include, not an inline `<script>` with code in it. The assignment rule is “no inline script tags” meaning don’t write JavaScript between `<script>...</script>`. Leaving the starter’s `bundle.js` include is required for the styles to load.

