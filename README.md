```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  PIP-BOY 3000 Mk VI  ·  MINING INTERFACE  ·  VAULT-TEC CORP  ☢    ║
║                                                                      ║
║           C A P S T A S H   L I N U X   M I N E R                    ║
║                   v4.20.69.1  ·  WHIRLPOOL-512                       ║
║                                                                      ║
║  [ STATS ]   [ POOLS ]   [ INSTALL ]   [ DATA ]   [ RADIO ]          ║
╚══════════════════════════════════════════════════════════════════════╝
```

> *"The Pip-Boy never lies, Vault Dweller. Your hashrate is your survival."*
> — Vault-Tec Mining Division, 2161

**VAULT-TEC CERTIFIED** CPU miner for the CapStash network. Purpose-built for Linux x86_64. Unlike bloated multi-algorithm miners carrying dead code for 80+ algorithms, this unit runs **Whirlpool-512 only** — lean, fast, and optimized for the wasteland's most abundant hardware: the humble CPU rig.

For intel on CapStash, tokenomics, and the coin itself, tune your Pip-Boy to:
**[https://github.com/CapStash/CapStash-Core](https://github.com/CapStash/CapStash-Core)**

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  STATS  ·  v4.20.69.1 UPGRADE LOG                                ║
╚══════════════════════════════════════════════════════════════════════╝
```

| SYSTEM | STATUS | NOTES |
|--------|--------|-------|
| Whirlpool T0-only | ✅ ONLINE | 2KB table vs 16KB — fits L1 cache entirely |
| Midstate precompute | ✅ ONLINE | Block header hashed once per template, not per nonce |
| P-core affinity | ✅ ONLINE | Threads pinned to performance cores via sched_setaffinity |
| Stratum pool client | ✅ ONLINE | Full subscribe → authorize → notify → submit pipeline |
| Clean status display | ✅ ONLINE | Hashrate · accepted · rejected · diff · ETA · temp |
| Dev fee 0.5% | ✅ ONLINE | 1 in 200 shares · supports continued development |

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  INSTALL  ·  QUICK DEPLOYMENT PROTOCOL                           ║
╚══════════════════════════════════════════════════════════════════════╝
```

### STEP 1 — DEPLOY MINING UNIT

```bash
curl -O https://raw.githubusercontent.com/blackshirt-crypto/capstash-miner-linux/main/setup_capstash_miner_linux.sh && chmod +x setup_capstash_miner_linux.sh && ./setup_capstash_miner_linux.sh
```

### STEP 2 — CONFIGURE YOUR UNIT

The interactive setup will interrogate you for:

- **Mining mode** — Solo (direct RPC to your node) or Pool (stratum)
- **Pool selection** — Choose from known wasteland pools or enter manually
- **Reward address** — Your CapStash wallet (`cap1...`, `C...`, or `8...`)
- **Thread count** — Recommended: number of physical CPU cores

### STEP 3 — BEGIN OPERATIONS

```bash
cd ~/capstash-miner && ./start.sh
```

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  RADIO  ·  KNOWN WASTELAND MINING POOLS                          ║
╚══════════════════════════════════════════════════════════════════════╝
```

*Tune your Pip-Boy to one of the following verified signals. Pool operators
are fellow survivors — check their dashboards for current status and
difficulty settings before committing your hashrate.*

```
┌─────────────────────────────────────────────────────────────────────┐
│  STATION          SIGNAL                              TYPE           │
├─────────────────────────────────────────────────────────────────────┤
│  capspool.io      stratum+tcp://pplns.capspool.io:6333   PPLNS      │
│  papaspool.net    stratum+tcp://papaspool.net:7777        PPLNS      │
│  crypto-eire.com  stratum+tcp://stratum.crypto-eire.com:3340  PPLNS │
│  1miner.net       stratum+tcp://1miner.net:3690           PPLNS      │
└─────────────────────────────────────────────────────────────────────┘
```

> ⚠️ **SIGNAL ADVISORY:** Pool addresses and ports may shift as the wasteland evolves.
> Always verify connection details at the pool's dashboard before deploying.

**Worker format:** `cap1qYOURADDRESS.your-worker-name`
**Password:** `x`

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  DATA  ·  FIELD OPERATIONS MANUAL                                ║
╚══════════════════════════════════════════════════════════════════════╝
```

**Start primary pool:**
```bash
cd ~/capstash-miner && ./start.sh
```

**Start backup pool:**
```bash
cd ~/capstash-miner && ./start-backup.sh
```

**Reconfigure unit:**
```bash
cd ~/capstash-miner && ./reconfigure.sh
```

**Run in background (screen):**
```bash
screen -S miner
cd ~/capstash-miner && ./start.sh
# Detach: Ctrl+A then D
# Reattach: screen -r miner
```

**Run in background (nohup):**
```bash
cd ~/capstash-miner && nohup ./start.sh > miner.log 2>&1 &
tail -f miner.log
```

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  DATA  ·  SOLO MINING PROTOCOL                                   ║
╚══════════════════════════════════════════════════════════════════════╝
```

Connect directly to your own CapStash node. You keep **100% of the block reward** (1 CAP per block, ~60 second block times). Requires a synced node on your network or Tailscale VPN.

Your node's `CapStash.conf` must contain:

```
server=1
rpcuser=youruser
rpcpassword=yourpass
rpcbind=127.0.0.1
rpcallowip=127.0.0.1
rpcallowip=192.168.x.0/24  ← your local subnet
rpcport=8332
```

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  DATA  ·  NETWORK INTELLIGENCE — LOTTERY BLOCKS & HARDFORKS     ║
╚══════════════════════════════════════════════════════════════════════╝
```

**HEIGHT 55,000 — LOTTERY CONSENSUS v1**
Lottery blocks are cryptographically random — approximately 1 in 20 blocks is a lottery block. Unpredictable. Manipulation-resistant.

**HEIGHT 65,000 — LOTTERY CONSENSUS v2 (PERMANENT)**
Consecutive lottery blocks prohibited. Updated domain separator.

**WHAT THIS MEANS FOR YOUR UNIT:** Nothing changes. Same Whirlpool-512 PoW. Same 1 CAP reward. No firmware update required.

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  DATA  ·  TROUBLESHOOTING — FIELD DIAGNOSTICS                   ║
╚══════════════════════════════════════════════════════════════════════╝
```

**"Failed to start — check node connection"**
- Verify node IP and RPC port
- Test signal:
```bash
curl -s --user "user:pass" --data '{"method":"getblockcount","params":[],"id":1}' \
  -H 'Content-Type: application/json' http://NODE_IP:8332/
```

**Pool shares not registering**
- Some pools run high minimum difficulty — switch to a CPU-friendly pool
- Verify worker format: `cap1qYOURADDRESS.workername`

**"Address decode failed"**
- Address must start with `cap1`, `C`, or `8`
- `cap1` addresses must be fully lowercase

**Hashrate lower than expected**
- Reduce thread count to match physical core count
- Avoid hyperthreaded/virtual cores — use physical cores only

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  DATA  ·  INTELLIGENCE BRIEF — ABOUT CAPSTASH                   ║
╚══════════════════════════════════════════════════════════════════════╝
```

```
DESIGNATION:    CapStash (CAPS)
ALGORITHM:      Whirlpool-512 XOR/256
BLOCK TIME:     ~60 seconds
BLOCK REWARD:   1 CAP
RESISTANCE:     GPU-resistant · ASIC-resistant · CPU-optimized
MAX SUPPLY:     90,000,000,000 CAP
STATUS:         ACTIVE — chain height 65,000+
```

Full intelligence dossier, whitepaper, node firmware, and wallet downloads:
**[https://github.com/CapStash/CapStash-Core](https://github.com/CapStash/CapStash-Core)**

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  RADIO  ·  SUPPORT & RESOURCES                                    ║
╚══════════════════════════════════════════════════════════════════════╝
```

| STATION | FREQUENCY |
|---------|-----------|
| CapStash Official | [capstash.org](https://capstash.org) |
| CapStash Core | [github.com/CapStash/CapStash-Core](https://github.com/CapStash/CapStash-Core) |
| Explorer | [capstashmempool.codefalcon.dev](https://capstashmempool.codefalcon.dev/) |
| Discord | [discord.gg/zrzmkwAM7G](https://discord.gg/zrzmkwAM7G) |
| This Repo | [github.com/blackshirt-crypto/capstash-miner-linux](https://github.com/blackshirt-crypto/capstash-miner-linux) |
| Android Version | [github.com/blackshirt-crypto/capstash-miner-android](https://github.com/blackshirt-crypto/capstash-miner-android) |

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  DATA  ·  ACKNOWLEDGEMENTS                                        ║
╚══════════════════════════════════════════════════════════════════════╝
```

Special thanks to **1miner** (dankminer v3.0.0) — pool operator at 1miner.net and
the first outside contributor to this project. His stratum expertise, bug fixes,
and PR #1 were instrumental in getting shares accepted. If you're looking for a
CPU-friendly pool with solid support, point your Pip-Boy to `1miner.net:3690`.

---

```
╔══════════════════════════════════════════════════════════════════════╗
║  ☢  VAULT-TEC LEGAL DISCLAIMER                                       ║
╚══════════════════════════════════════════════════════════════════════╝
```

*Mining operations consume power reserves. Monitor unit temperature.
Vault-Tec Corporation accepts no liability for losses sustained in the wasteland.
This firmware is provided as-is. Mine responsibly. The wasteland is unforgiving.*

---

```
╔══════════════════════════════════════════════════════════════════════╗
║                                                                      ║
║   ☢  WALLET OF THE WASTELAND  ·  STAY VIGILANT  ·  STACK CAPS  ☢   ║
║                                                                      ║
║              War never changes. But hashrates do.                    ║
║                                                                      ║
╚══════════════════════════════════════════════════════════════════════╝
```
