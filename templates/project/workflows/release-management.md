# Release Management

> Project workflow — for preparing and publishing releases.

## Description

Prepare, test, and publish a new release version.

## Steps

1. **Ensure main branch is up to date**:
   ```bash
   git checkout main
   git pull origin main
   ```

2. **Verify all tests pass**:
   ```bash
   pnpm test
   ```

3. **Gather changes since last release**:
   - List merged PRs since last release tag: `git log --oneline $(git describe --tags --abbrev=0)..HEAD`
   - Categorize changes: features, bug fixes, breaking changes, other

4. **Determine version bump**:
   - **Major**: Breaking changes to public API
   - **Minor**: New features, backward-compatible
   - **Patch**: Bug fixes only

5. **Update version**:
   ```bash
   npm version <major|minor|patch>
   ```

6. **Update CHANGELOG.md**:
   - Add new version section with date
   - List all changes organized by category
   - Credit contributors

7. **Create release branch**:
   ```bash
   git checkout -b release/vX.Y.Z
   ```

8. **Create a pull request** for the release branch targeting main.

9. **After merge, tag the release**:
   ```bash
   git tag -a vX.Y.Z -m "Release vX.Y.Z"
   git push origin vX.Y.Z
   ```

10. **Deploy to staging** and verify.

11. **Deploy to production** after staging verification.

12. **Create GitHub release** with the changelog contents:
    ```bash
    gh release create vX.Y.Z --title "vX.Y.Z" --notes-file RELEASE_NOTES.md
    ```

13. **Notify the team** about the new release.
