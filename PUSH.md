# Getting this onto GitHub from Terminal

One-time setup, then every future update is two commands.

Open **Terminal** (Cmd+Space, type "terminal") and go to the project. The path
has a space in it, so the quotes matter:

```bash
cd "$HOME/Vaults/Cowork Base/breakpoint-arcade"
```

Check you're in the right place — this should list `index.html`, `sw.js` and the rest:

```bash
ls
```

---

## 1. Commit what's waiting

I made the first commit already. One file was added afterwards, so:

```bash
git status
git add -A
git commit -m "Add gitignore"
```

If `git` makes macOS pop up a "command line developer tools" box, click
**Install**, wait for it to finish, and run the command again.

---

## 2. Log in to GitHub

The `gh` tool handles login through your browser, so there are no tokens to
copy around. Check whether you have Homebrew:

```bash
brew --version
```

**If that printed a version**, install `gh` and log in:

```bash
brew install gh
gh auth login
```

Answer the prompts: **GitHub.com** → **HTTPS** → **Y** (authenticate git) →
**Login with a web browser**. It shows an eight-character code, you press
Enter, your browser opens, you paste the code and click through. Done for good —
it remembers you from now on.

**If `brew` was not found**, you have two choices. Either install Homebrew
(paste the line from brew.sh, takes a few minutes) and come back, or skip `gh`
entirely and use the token route in the appendix at the bottom.

---

## 3. Create the repo and push

One command creates it on GitHub, wires it up and pushes:

```bash
gh repo create breakpoint-arcade --public --source=. --remote=origin --push
```

Reading that: `--public` because GitHub Pages needs public on a free plan,
`--source=.` means "this folder", `--push` sends the commits straight after
creating it.

It prints the URL of your new repo. Open it — your files should be there.

---

## 4. Turn Pages on

Easiest through the website: on your repo page, **Settings** → **Pages** in the
left menu → Source **Deploy from a branch** → branch **main**, folder
**/ (root)** → **Save**.

Or from Terminal, if you'd rather:

```bash
echo '{"source":{"branch":"main","path":"/"}}' | \
  gh api --method POST repos/zdthorman/breakpoint-arcade/pages --input -
```

Either way, wait a minute or two, then open:

**https://zdthorman.github.io/breakpoint-arcade/**

A 404 at first is normal. Give it another minute.

---

## 5. Put it on your phone

Open that URL in **Safari** on your iPhone (it has to be Safari, not Chrome),
tap the Share button, then **Add to Home Screen**.

---

## Every time you change something after this

```bash
git add -A
git commit -m "say what you changed"
git push
```

Pages redeploys in about a minute.

---

## When it goes wrong

**`xcrun: error: invalid active developer path`**
macOS hasn't installed its developer tools yet. Run `xcode-select --install`,
click through the installer, try again.

**`remote: Support for password authentication was removed`**
You typed your GitHub password where it wanted a token. Passwords haven't
worked for git since 2021. Use `gh auth login`, or a token — see below.

**`error: failed to push some refs`**
The repo on GitHub already has something in it (usually because you ticked "add
a README" when creating it). Pull their version in first, then push:

```bash
git pull --rebase origin main
git push
```

**`fatal: not a git repository`**
You're in the wrong folder. Run the `cd` command from the top again.

**`Unable to create '.git/index.lock': File exists`**
A previous command died holding a lock. Safe to remove it:

```bash
rm -f .git/index.lock
```

---

## Appendix: the token route, if you skipped `gh`

1. On github.com: **+** (top right) → **New repository** → name
   `breakpoint-arcade` → **Public** → don't tick anything else → **Create**.
2. Make a token: your avatar → **Settings** → scroll to **Developer settings**
   → **Personal access tokens** → **Tokens (classic)** → **Generate new token
   (classic)**. Tick the **repo** box. Generate, and copy it — you only get to
   see it once.
3. Back in Terminal:

```bash
git remote add origin https://github.com/zdthorman/breakpoint-arcade.git
git branch -M main
git push -u origin main
```

4. It asks for a username (`zdthorman`) and a password — **paste the token as
   the password**. macOS Keychain saves it, so you only do this once.

Then carry on from step 4 above.
