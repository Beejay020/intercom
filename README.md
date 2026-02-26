# BountyBoard — P2P Task Market on Intercom

> A fork of [Trac-Systems/intercom](https://github.com/Trac-Systems/intercom) that adds a decentralized, agent-native bounty board built on Intercom sidechannels.

**Trac Address:** `trac1p6dsun79n0wf7dmqw7vhlp73d9hzprp4r7txmdff0azurnrzj47q2ch7vw`  


---

## What is BountyBoard?

BountyBoard is a peer-to-peer task market where anyone can:

- **Post** tasks/bounties with TNK rewards
- **Apply** for bounties over Intercom sidechannels (fast, ephemeral P2P messaging)
- **Negotiate** terms directly peer-to-peer, without a centralized server
- **Settle** payments through Intercom's contract layer (deterministic escrow)

All coordination flows through Intercom's sidechain protocol — no custodians, no middlemen, no downtime.

---

## App Features

- 🟡 **Live bounty board** — browse, filter, and search open tasks
- ⚡ **Real-time feed** — P2P activity over Intercom sidechannels
- 🔒 **Escrow-backed rewards** — TNK locked in contract until delivery
- 🤖 **Agent-native** — fully described in SKILL.md for AI agent integration
- 📱 **Responsive UI** — works on desktop and mobile

---


---

## How It Works

```
Poster                  Intercom Sidechain           Applicant
  │                            │                         │
  ├─── postBounty(title,       │                         │
  │    reward, escrow) ────────►                         │
  │                            │◄── browseBounties() ────┤
  │                            │                         │
  │◄─────────── applyBounty(id, tracAddress) ────────────┤
  │                            │                         │
  ├─── acceptApplication() ───►│                         │
  │                            │──── notify() ──────────►│
  │                            │                         │
  │                 [work delivered]                      │
  │                            │                         │
  ├─── releaseEscrow(id) ──────►────── TNK payout ───────►
```

The **sidechannel** handles fast ephemeral negotiation. The **contract layer** handles the durable state (posted bounties, escrow, completions). Both are provided by the upstream Intercom stack.

---

## Quick Start

```bash
# Clone this fork
git clone https://github.com/YOUR_USERNAME/intercom-bountyboard
cd intercom-bountyboard

# Install Intercom dependencies
npm install

# Start Intercom node
node index.js

# Open the app UI
open app/index.html
```

---

## File Structure

```
intercom-bountyboard/
├── index.js              # Intercom node (upstream)
├── contract/             # Intercom contract layer (upstream)
├── features/             # Intercom features (upstream)
├── app/
│   ├── index.html        # BountyBoard UI (this app)
│   └── bountyboard.js    # App logic + Intercom integration
├── SKILL.md              # Agent instructions
├── README.md             # This file
└── package.json
```

---

## Integration with Intercom

BountyBoard uses the following Intercom primitives:

| Primitive | Usage |
|-----------|-------|
| `sidechannel.send()` | Broadcasting bounty applications |
| `sidechannel.subscribe()` | Listening for new bounties and updates |
| `contract.post()` | Writing bounty state on-chain |
| `contract.read()` | Reading active bounties |
| `msb.escrow()` | Locking TNK reward until completion |
| `msb.release()` | Releasing payment on confirmation |

---

## Competition Entry

This project is submitted for the **Intercom Vibe Competition** (IntercomSwap extension).

- Fork of: `Trac-Systems/intercom`
- App: BountyBoard — P2P Task Market
- **Trac Address for TNK Payout:** `trac1p6dsun79n0wf7dmqw7vhlp73d9hzprp4r7txmdff0azurnrzj47q2ch7vw`

---

## License

MIT — see LICENSE
