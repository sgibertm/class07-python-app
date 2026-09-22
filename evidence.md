# Class 07: repository, trigger and image evidence

Use actual output. Replace each blank; do not copy the acceptance text as a result.

## Step 1 — Create the repository and pipeline

- Repository URL: [https://github.com/sgibertm/class07-python-app](https://github.com/sgibertm/class07-python-app)

- Workflow path: `.github/workflows/ci.yml`

- First passing run URL and source commit: [https://github.com/sgibertm/class07-python-app/actions/runs/35758152622](https://github.com/sgibertm/class07-python-app/actions/runs/35758152622); commit `bf0fc569fdbc8c0abf7f239bb292d3d327abf281`

- Actual unit-test result: GitHub Actions run completed successfully. The `test` job passed and the unit tests completed with `OK`.

## Step 2 — Run only on pushes to main

- Commit/run that installed the main-only trigger: Commit `40e9155a35608babb0c7085313182fef548aab17`; run [https://github.com/sgibertm/class07-python-app/actions/runs/35759566602](https://github.com/sgibertm/class07-python-app/actions/runs/35759566602)

- `trigger-check` branch commit SHA: `1a07cfd320f2d7fc2ca64c42164ae79f85374e47`

- What the Actions page showed for that branch/SHA: No workflow run was created for commit `1a07cfd` while it was pushed to `trigger-check`. The Actions page showed only the runs for the pushes to `main`.

- Run URL after the same commit was pushed to `main`: [https://github.com/sgibertm/class07-python-app/actions/runs/35760013299](https://github.com/sgibertm/class07-python-app/actions/runs/35760013299)

- Explain why a local commit alone does not start GitHub Actions: A local commit only changes the local Git repository. On the other hand, GitHub Actions runs are triggered by events received by GitHub, such as a push to a branch that matches the workflow trigger. Therefore, creating a commit locally does not start a GitHub Actions run until the commit is pushed to GitHub.

## Step 3 — Publish and retrieve the Python image

- Package page URL (GHCR, linked to this repository): [https://github.com/sgibertm/class07-python-app/pkgs/container/class07-python-app](https://github.com/sgibertm/class07-python-app/pkgs/container/class07-python-app)

- Source commit, run URL and attempt: Commit `c55068ebc7d12f6b6fd526bbac1b1e8533968c5e`; run [https://github.com/sgibertm/class07-python-app/actions/runs/35761987918](https://github.com/sgibertm/class07-python-app/actions/runs/35761987918); attempt `1`

- Actual source-test and packaged HTTP test results: The package job completed successfully. The package job summary reported `checks=source unit tests + packaged HTTP smoke test passed before publish`.

- Complete registry reference (`repository@sha256:` plus 64 hexadecimal digits): `ghcr.io/sgibertm/class07-python-app@sha256:0872e6c04a5bda74addf63c6de1b1715e716007212fa532ac500091d25ce0b37`

- Platform: `linux/amd64`

- Exact pull command:

`docker pull --platform linux/amd64 ghcr.io/sgibertm/class07-python-app@sha256:0872e6c04a5bda74addf63c6de1b1715e716007212fa532ac500091d25ce0b37`

- Actual pulled-image HTTP test output:

`PASS: health + 3 HTTP scoring cases`

  The local verification also showed:

  - `GET /health` → `200`

  - `GET /score?value=0.2` → `200`

  - `GET /score?value=0.5` → `200`

  - `GET /score?value=0.9` → `200`

  The digest reported by `docker pull` matched the published digest:

`sha256:0872e6c04a5bda74addf63c6de1b1715e716007212fa532ac500091d25ce0b37`

## Limits and explanation

- One thing these tests do not establish: These tests do not establish that the application is secure, production-ready, or correct for inputs and use cases that are not covered by the provided unit tests and HTTP smoke tests.

- Explain the difference between the Git repository and its linked image package: The Git repository stores the application's source code, tests, Dockerfile, workflow and other project files. The linked GHCR image package stores a built Docker image that can be pulled and run independently of the source repository. The image is produced from a particular source commit and is identified by its immutable digest.

- AI assistance used (tool, task, verification): ChatGPT was used as a support tool to clarify GitHub Actions and Docker concepts, explain some command outputs, and help resolve a few configuration issues. The workflow and commands were implemented and tested by the student, who verified the GitHub Actions run, GHCR publication, image pull, and HTTP tests.

## Optional failure-and-repair extension

- Failed commit/run, useful assertion and skipped package job: Not performed.

- Repaired commit/run and recovered digest: Not applicable.

Save the successful package job summary, or paste its release record above.

If using a fallback, explicitly mark the uncompleted hosted checks and local simulation results. Do not invent a repository, run URL or successful GHCR push.
