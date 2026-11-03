# Lidarr

## Documentation

- [Lidarr Quick Start Guide](https://github.com/Servarr/Wiki/blob/master/lidarr/quick-start-guide.md) — the upstream walkthrough of first setup
- [Lidarr Settings](https://github.com/Servarr/Wiki/blob/master/lidarr/settings.md) — every settings page explained
- [Lidarr FAQ](https://github.com/Servarr/Wiki/blob/master/lidarr/faq.md) — common questions about searching, importing and quality
- [Lidarr Troubleshooting](https://github.com/Servarr/Wiki/blob/master/lidarr/troubleshooting.md) — diagnosing failed downloads and imports

## What you get on StartOS

- The Lidarr web interface, behind a login that is set up for you.
- qBittorrent on this server connected as Lidarr's download client, kept up to date for you.
- Your music library kept in FileBrowser Quantum or NextExplorer, where you can browse the files and where Jellyfin can read them.
- Lidarr's settings, history and library database in StartOS backups. The music files are backed up with FileBrowser Quantum or NextExplorer.

## Getting set up

1. Install FileBrowser Quantum or NextExplorer, if you have neither.
2. Run **Set Admin Password** and save the username and password it shows.
3. Run **Media Storage** and choose FileBrowser Quantum, NextExplorer, or both.
4. In qBittorrent, run **Set Download Location** and choose the same file manager. Lidarr can only import downloads it can see, and moves them fastest when they are on the same file manager as your library.
5. Run **Connect qBittorrent**.
6. Start Lidarr, open the Web UI, and sign in.
7. Add indexers under **Settings → Indexers**.
8. In your file manager, create a folder for your music, such as `music`.
9. In Lidarr, go to **Settings → Media Management → Root Folders → Add Root Folder** and set its path to that folder:
   - FileBrowser Quantum: `/mnt/filebrowser/music`
   - NextExplorer: `/mnt/nextexplorer/<location>/music`, where `<location>` is one of NextExplorer's locations, such as `Files`
10. Point a Jellyfin library at the same folder, then add artists in Lidarr with **Library → Add New**.

## Using Lidarr

- **Reset Admin Password** generates a new password and restarts Lidarr. The old password stops working.
- **Media Storage** changes which file managers Lidarr can use, and restarts Lidarr.
- **Connect qBittorrent** / **Disconnect qBittorrent** adds qBittorrent as a download client, or removes Lidarr's `qBittorrent (StartOS)` download client. The connection follows qBittorrent automatically; there is nothing to redo when qBittorrent's password changes.
- Lidarr's login is managed by StartOS: changing the username or authentication method in Lidarr's settings is undone on the next restart. Use **Reset Admin Password** instead.
