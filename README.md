# Director’s Desk

A personal workspace for writing, directing, on-set take logs and editing.

## Use the app
Open `index.html` in a browser. The app has no build step or external JavaScript dependencies. Fonts fall back to system fonts when offline.

Logs save in that browser’s local storage. GitHub does **not** sync or back up film logs. Export JSON backups regularly; PDF is for reading and cannot restore a workspace. Before changing the file location or browser, export a backup and restore it in the new location.

## First GitHub setup
1. Create an **empty private repository** on GitHub named `directors-desk`. Leave README, license and .gitignore unchecked because this package includes its own files.
2. Extract this folder and open a terminal inside it.
3. Run the commands below, replacing `YOUR-USERNAME` with your GitHub username:

```sh
git init -b main
git add .
git commit -m "Add Director's Desk and automated checks"
git remote add origin https://github.com/YOUR-USERNAME/directors-desk.git
git push -u origin main
```

Authenticate through your usual GitHub login method. Never put tokens in app code. If you already have a repository, clone it and add these files on a new branch instead; do not force-push over existing work.

## Make an update
```sh
git switch main
git pull --ff-only
git switch -c fix/describe-the-change
# Edit index.html and add regression tests.
npm test
git add index.html tests
git commit -m "Describe the fix"
git push -u origin fix/describe-the-change
```

Open a pull request on GitHub. Review the changes, wait for **App checks** to pass, and test the app in a real browser before merging. The automated tests use a simulated DOM, so they do not verify actual clicks, layout or PDF pagination. Review the PR's data impact before merging changes to saving or backup formats.

After merging, download the updated index.html. Export your current workspace backup first. Check the new app before removing your previous copy.

## Tests
Install Node.js 22 or newer, then run `npm test`. No `npm install` is necessary. CI runs the same tests on pushes to main and on pull requests.

## Hosting and privacy
This package does not publish a website automatically. A private source repository does not by itself make a hosted website private. Choose hosting and access controls deliberately. Never commit exported logs, private scripts, JSON backups or credentials.

## Source layout
- `index.html`: complete app
- `tests/app.test.cjs`: regression checks
- `.github/workflows/checks.yml`: automatic checks
- `.github/ISSUE_TEMPLATE/bug_report.md`: bug report form
- `.github/pull_request_template.md`: review checklist
