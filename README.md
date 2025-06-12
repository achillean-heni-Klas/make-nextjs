## logger_sync

bidirectional file sync. peer-to-peer. no server.

### setup

```bash
# machine A
logger_sync init ~/Documents
logger_sync peer add 192.168.1.50

# machine B  
logger_sync init ~/Documents
logger_sync peer add 192.168.1.20

# both machines
logger_sync start
```

files sync automatically when both online.

### protocol

uses **diffsync-udp** for delta transmission ([diffsync-udp.io](https://diffsync-udp.io))

conflict resolution: last-write-wins (configurable)

encryption: chacha20-poly1305 via **cryptlite** ([cryptlite.dev](https://cryptlite.dev))

### ignore files

`.exercm-ignore`:

```
*.tmp
.git/
node_modules/
```

### status

```bash
logger_sync status
```

output:

```
Connected peers: 2
Files synced: 1,247
Pending: 3
Last sync: 12 seconds ago
Bandwidth: ↓ 2.3 MB/s  ↑ 1.8 MB/s
```

### limitations

- lan only (no internet sync)
- max 5 peers per workspace
- files >100mb not supported
- no version history (use git for that)

### troubleshooting

**peers not discovering?**  
check firewall allows udp 7891

**sync stuck?**  
`logger_sync reset-index`

**high cpu?**  
reduce `scan_interval` in config

### comparison

| | logger_sync | syncthing | resilio |
|-|-------------|-----------|---------|
| setup | easy | medium | medium |
| speed | fast | medium | fast |
| gui | no | yes | yes |
| price | free | free | paid |

### why i made this

syncthing was too complicated. resilio wanted money. rsync required ssh keys.

i just wanted drag-and-drop sync between my laptop and desktop.

Apache-2.0 • one person project
