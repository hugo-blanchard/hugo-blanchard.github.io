# hugo-blanchard.github.io

Personal resume site, served by GitHub Pages.

- `index.html` — resume (public).
- `projects.html` — side-project write-up (Polyfast), AES-256-encrypted with
  [StatiCrypt](https://github.com/robinmoisson/staticrypt); decrypts in the browser with a
  password shared privately. The plaintext source `projects_src.html` is **gitignored** —
  it lives only on the local machine.
- `style.css` — shared g3doc-like stylesheet (print-friendly: Ctrl+P on the resume yields a
  clean PDF).

## Rebuilding the encrypted page

After editing `projects_src.html` locally:

```powershell
npx -y staticrypt@3.5.4 projects_src.html -p "<the password>" -d enc -t password_template.html `
  --template-title "Side project - restricted" `
  --template-instructions "Enter the access password Hugo shared with you." --short
Move-Item -Force enc/projects_src.html projects.html
```

`password_template.html` is the site-themed StatiCrypt gate template (derived from
staticrypt 3.5.4's `lib/password_template.html` — keep its placeholders, element ids, and
script intact when editing the styling).

Then commit and push `projects.html`.
