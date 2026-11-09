# Updating Lidarr

## Determining the upstream version

Upstream is the LinuxServer image `lscr.io/linuxserver/lidarr`, pinned in `startos/manifest/index.ts`:

```typescript
source: { dockerTag: 'lscr.io/linuxserver/lidarr:3.1.6.5079-ls46' },
```

LinuxServer tags its stable builds `<lidarr version>-ls<build>`; its GitHub release marked Latest is the stable one (`develop-*` and `nightly-*` are not). The build number can restart, and `nightly-*` builds are newer than the stable one, so go by Latest, not by the highest number:

```bash
gh release view -R linuxserver/docker-lidarr --json tagName -q .tagName
```

Confirm the tag ships both architectures before pinning it:

```bash
docker manifest inspect lscr.io/linuxserver/lidarr:<tag> | jq -r '.manifests[].platform.architecture'
```

The **Check upstream** workflow runs this every Monday and opens an issue when LinuxServer's Latest release carries a newer Lidarr version, saying whether its image is on lscr.io for both architectures; a new `-ls` build of the pinned Lidarr version opens none. GitHub pauses scheduled workflows in a public repository after 60 days without activity; re-enable it from the repository's **Actions** tab.

## Applying the bump

1. Read Lidarr's release notes (`gh release view -R Lidarr/Lidarr v<version>`) between the old and new versions. A major version can change the host-config API or `config.xml` keys this package writes; check both against `startos/main.ts` and `startos/fileModels/config.xml.ts`.
2. Edit `dockerTag` in `startos/manifest/index.ts`.
3. Edit `startos/versions/current.ts`: the version is the Lidarr version without the `-ls` suffix (`'3.1.6.5079:0'`), with localized release notes. A new LinuxServer build of the same Lidarr version is a downstream revision bump (`:1`).
4. Install on a box and confirm the login still works and an old password is rejected after Reset Admin Password.
