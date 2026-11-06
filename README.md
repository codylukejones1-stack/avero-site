# AVERO public website

This repository contains the public website deployment workflow. Application
source stays in the separate private repository `codylukejones1-stack/avero.`. Only
compiled browser assets and intentionally published NFL data go onto `gh-pages`.
Backend source, fitted model files, source caches and the SQLite ledger are not
published here. Website visitors receive compiled JavaScript, as on other sites.

## One-time connection

1. Keep this deployment repository **public** and the application repository
   **private**. Never copy the application's folders or Git history here.
2. In your GitHub account settings, create a fine-grained personal access token
   restricted to **only** `codylukejones1-stack/avero.`. Grant repository **Contents: Read
   and write** so the workflow can read source and append durable private state.
   No account billing, administration, or workflow-write permission is needed.
   Store its value only in this repository's **Actions secrets**, named
   `AVERO_SOURCE_TOKEN`. Never put the token in a file, chat, issue, or public log.
   Track its expiry and replace the secret before it expires.
3. Run **Actions > Update AVERO website > Run workflow**. The first run saves
   website files on `gh-pages`. If its final Pages request fails before Pages
   setup, that is not confirmation of a live website.
4. Choose **Settings > Pages > Deploy from a branch > gh-pages > / (root)**,
   then rerun. Use the URL GitHub reports after a successful build.

## Updates and privacy

The private source repository is already set to `codylukejones1-stack/avero.`. To use
another source repository, set Actions repository variable
`AVERO_SOURCE_REPOSITORY`; no variable entry is needed for this prepared setup.

The scheduled public workflow checks approximately every 15 minutes and checks
out the private source repository's latest `main`. GitHub may delay or skip
scheduled runs. Browser Update fetches the latest published JSON; it does not
force an upstream source request. Source timestamps remain visible.

The source checkout's restricted token accesses only the private repository.
Its `avero-public-state` branch retains source/model caches and immutable
forecast history. The public checkout uses its own normal `GITHUB_TOKEN` to
save compiled site files and request Pages builds. These Git histories are never
merged. Do not add pull-request triggers or execute untrusted contributions with
the source secret. Private command diagnostics stay on the temporary runner and
are not uploaded. Do not enable debug logging or publish those logs.

## Free operation

This workflow uses only standard public-repository `ubuntu-latest` runners and
explicitly skips private deployment repositories. It does not use Actions
artifacts, Actions caches, larger runners, paid hosting, or paid data APIs. The
website and private state use ordinary Git branches. GitHub free product size,
bandwidth, build and abuse limits still apply; there is no automatic paid fallback.
Do not enable a paid plan or overage budget for this setup.

No site is live merely because these files exist. Repository creation, the
private-source connection, and Pages activation require actual account setup.
