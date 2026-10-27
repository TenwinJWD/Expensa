# Signing setup (one time)

Release builds are signed by [SignPath Foundation](https://signpath.org) for open-source projects. This is what you do once.

1. Make the repository public (see the checklist at the end of this file).
2. Apply at <https://signpath.org/apply.html>. They check the license (Apache-2.0), that the project is public and released, and that it builds from source in CI.
3. After approval, in SignPath create the project and a signing policy. Add the two artifact configurations from `.signpath/artifact-configurations` (slugs `exe` and `msi`), and install the SignPath GitHub App on the repository.
4. In GitHub, **Settings > Secrets and variables > Actions**:
   - Secret `SIGNPATH_API_TOKEN`: an API token for a user allowed to submit to that policy.
   - Variables `SIGNPATH_ORGANIZATION_ID`, `SIGNPATH_PROJECT_SLUG`, `SIGNPATH_POLICY_SLUG`.
5. Push a tag such as `v1.0.1`. The workflow tests, builds, signs the program, both MSI files and the setup program, then uploads them with `SHA256SUMS.txt`.

`Build/1.0/build.ps1` and `Build/1.0/installer/sign.ps1` are for local test builds signed with a self-signed certificate. They are not used for releases.

## Before the repository goes public

- Run `git log --all --stat` and check that no client material remains in any commit. Removing files from the latest commit leaves them in history; to remove them, rewrite history or publish from a fresh repository.
- Confirm the license text and copyright line (`LICENSE`, `Build/1.0/installer/License.rtf`).
