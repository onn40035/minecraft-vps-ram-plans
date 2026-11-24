# Minecraft VPS: How Much RAM You Actually Need, Which Evoxt Plan Fits 2–20 Players, and What the Low Monthly Price Leaves Out (Full Plan Table)

A survival server for a few friends starts at **$5.99/month** on Evoxt's VM-1: one core, 2 GB RAM, 20 GB storage, 500 GB of monthly transfer. If you plan to run a modpack like All the Mods or Feed the Beast, the realistic floor is **VM-4 at $23.99** for 8 GB. Anything below 4 GB with a heavy pack will disappoint you within a week, and the reason has less to do with core count than most hosting pages admit.

This article works through the RAM math by player count, the one hardware spec that decides whether your server holds a steady 20 TPS, the full Evoxt plan table with prices, and the parts of a Minecraft VPS purchase that listicles usually skip: transfer caps, disk sizes that run out faster than you expect, and what a cheap first-year price turns into at renewal elsewhere.

> **Quick pick:** for vanilla survival with 2–10 friends, Evoxt VM-1 at $5.99/month is enough server for the job. Running a modpack or a plugin-heavy Paper world with 20+ players, go to VM-4 (8 GB, $23.99). Both are plain Linux VMs with root access, so you install Java and the server jar yourself.
> 👉 [See the VM-1 plan and current pricing](https://bit.ly/EvoXt)

## Every Evoxt plan, side by side

Evoxt sells one family of cloud VMs (VM-0.5 through VM-16) rather than a separate "game hosting" product line, so the plan you pick for Minecraft is the same plan someone uses for a web app. All of them list CPU frequencies up to 6.0 GHz, weekly offsite backups at no extra cost, and a monthly transfer allowance that scales with the plan.

| Plan | vCPU / RAM | Storage / Transfer | Price (monthly) | Order |
| --- | --- | --- | --- | --- |
| VM-0.5 | 1 core / 512 MB | 5 GB / 250 GB | $2.99 | [Deploy VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 core / 1 GB | 10 GB / 250 GB | $4.99 | [Deploy VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 core / 2 GB | 20 GB / 500 GB | $5.99 | [Deploy VM-1](https://bit.ly/EvoXt) |
| VM-1.5 | 2 cores / 2 GB | 20 GB / 500 GB | $6.95 | [Deploy VM-1.5](https://bit.ly/EvoXt) |
| VM-2 | 2 cores / 4 GB | 30 GB / 1,000 GB | $11.99 | [Deploy VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 cores / 4 GB | 30 GB / 1,000 GB | $14.99 | [Deploy VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 cores / 8 GB | 60 GB / 2,000 GB | $23.99 | [Deploy VM-4](https://bit.ly/EvoXt) |
| VM-6 | 8 cores / 8 GB | 60 GB / 2,000 GB | $29.99 | [Deploy VM-6](https://bit.ly/EvoXt) |
| VM-8 | 8 cores / 16 GB | 80 GB / 3,000 GB | $47.99 | [Deploy VM-8](https://bit.ly/EvoXt) |
| VM-12 | 16 cores / 16 GB | 80 GB / 3,000 GB | $60.95 | [Deploy VM-12](https://bit.ly/EvoXt) |
| VM-16 | 16 cores / 32 GB | 100 GB / 5,000 GB | $95.99 | [Deploy VM-16](https://bit.ly/EvoXt) |

Prices are the monthly rates Evoxt lists for these plans. Billing can run from monthly up to a three-year prepay, and you can top up account credit and let the system apply it to future invoices.

## How much RAM does a Minecraft server need for 2, 10 or 30 players?

Published recommendations disagree, and the disagreement is worth understanding before you buy.

Cloudzy's guide puts vanilla survival for a few friends at **2 GB**, modpacks (FTB, ATM, Create-heavy) at **4–8 GB**, and busy Spigot/Paper networks at **8–16 GB**. Liquid Web's setup guide recommends a **4 GB minimum** with 6–8 GB for modded servers, plus a dual-core 3.0 GHz+ CPU. Neither is wrong: 2 GB is the smallest amount that will boot and play vanilla, while 4 GB is where a server stops being fragile the moment someone loads a redstone contraption or a chunk loads with forty mobs in it.

Cloudzy also maps plans to headcount, which is the most useful framing for a buyer: 2 GB for 5–10 players, 4 GB for 10–20, 8 GB for 20–40 with heavy mods, 12 GB for a large community or a plugin-dense server. Treat those as ceilings for vanilla-plus-light-plugins, not guarantees.

For Evoxt specifically, the mapping looks like this:

| What you're running | RAM | Evoxt plan | Monthly |
| --- | --- | --- | --- |
| Vanilla survival, 2–6 friends | 2 GB | VM-1 | $5.99 |
| Vanilla or light plugins, 10–20 players | 4 GB | VM-2 | $11.99 |
| Paper with plugins, 20–40 players | 8 GB | VM-4 | $23.99 |
| ATM / FTB / Create-heavy pack, 5–15 players | 8 GB | VM-4 | $23.99 |
| Public network with BungeeCord or Velocity | 16 GB | VM-8 + extra IPs | $47.99 |

Two things in that table cost people money. First, a heavily modded pack with five players needs more RAM than a vanilla server with twenty, because the pack's mob AI, world generation and machine tick loops all run inside the same JVM heap. Second, chunk-loaded farms and large render distances push memory use up regardless of how many people are online. If your world already exists and is a few gigabytes of region files, do not buy the 2 GB plan and hope.

👉 [Check the VM-4 plan for modded servers](https://bit.ly/EvoXt)

## The spec that decides whether your server stutters

Minecraft's main game loop runs on a single thread. Cloudzy states it plainly in its own FAQ: single-thread performance matters more than vCPU count. Liquid Web frames the same problem from the other side, warning that redstone machines and mob spawners cause TPS drops on shared hosting because the CPU gets saturated.

That has a direct consequence for how you read the Evoxt plan table. VM-1.5 gives you a second core for $0.96 more than VM-1, and VM-3 gives you four cores and 4 GB for $3 more than VM-2's two cores and 4 GB. For a single Minecraft world, those extra cores mostly sit idle while the main tick thread does all the work. The money is better spent on RAM, or on the clock speed of the core you do get.

Evoxt's pitch is exactly that clock speed: VMs listed at up to 6.0 GHz turbo, with a 3.5 GHz+ base, and the option to ask for a different node if your assigned one is slower than that. For a game server that lives and dies on single-thread speed, a high-frequency core paired with adequate RAM is a better shape than a 4-core box with 2 GB.

Where extra cores do earn their keep: running a Velocity or BungeeCord proxy in front of several Paper backends, running Dynmap's render thread alongside the game, or pre-generating chunks with Chunky before you open the server to players. Those are the cases where VM-3 or VM-6 makes sense.

## What the $5.99 includes, and where the limits are

Evoxt's plans come with weekly offsite backups at no extra charge, a control-panel firewall you can configure without SSHing into the box, VM cloning, and IP reassignment between servers. That last one matters if you ever rebuild a server and want to keep the address your players have saved.

A few limits to price in before you order:

**Disk size.** VM-1 ships 20 GB. A vanilla world plus a couple of backups fits. A large modpack, its configs, the world and rotating backups do not fit comfortably, and world size grows with exploration. VM-4's 60 GB is the safer floor for anything modded.

**Transfer allowance.** The monthly caps run from 250 GB on VM-0.5 and VM-0.75 up to 5 TB on VM-16, with VM-1 at 500 GB and VM-2 at 1 TB. A private server for friends will not come close. A public server streaming Dynmap tiles, hosting a voice mod or bridging Bedrock players through Geyser will chew through 500 GB faster than you'd think. The plan table doesn't spell out what happens when you exceed the cap, so ask support before you commit if you expect public traffic.

**Location tiers.** Evoxt's locations cover North America, Europe and Asia-Pacific (including Tokyo, Osaka, Hong Kong, Malaysia, Indonesia, South Korea and Australia). Hong Kong, Osaka and the Malaysia premium network are reported to carry lower transfer allowances at the same price, so check the allowance attached to the specific location you pick rather than assuming the plan's headline number.

**Extra IPs** cost $3/month each. Worth it if you run a proxy plus backends on one machine, or want a stable address for SRV records while you rebuild.

Payment options include credit and debit cards, PayPal, Bitcoin and USDt Tron.

## The renewal question nobody puts in the headline

Evoxt's $5.99 is a monthly rate, not a first-invoice discount that resets upward later. That is unusual enough in this market to be worth spelling out with competitors' numbers.

Hostinger's Game Panel 1 advertises $6.99/month, but that price requires paying **$167.76 upfront for 24 months**, and the plan **renews at $11.99/month** for the same term. That's roughly a 71% step up from the advertised rate when the first term ends. Game Panel 2 runs $9.49/month on the same 24-month prepay ($227.76 total) and renews at $14.99. Cloudzy's entry price of about $7.48/month is a 50% discount off a $14.95 list price, and its page doesn't state what happens after the promotional period.

If you intend to keep a server running for years, a $5.99 monthly rate that stays $5.99 is cheaper than a $6.99 rate that becomes $11.99. If you're testing whether a modpack will even run for your group, monthly billing is the right call regardless of provider, because you're not locked into a two-year prepay on an experiment.

| Provider | Entry plan | Advertised price | What to know |
| --- | --- | --- | --- |
| Evoxt | VM-1: 1 core / 2 GB / 20 GB | $5.99/mo | Monthly rate; billing up to 3 years optional; weekly offsite backup included |
| Cloudzy | 2 GB / 1 vCPU / 60 GB | ~$7.48/mo | 50% off a $14.95 list price; 14-day money-back; 13 regions |
| Hostinger | Game Panel 1: 1 vCPU / 4 GB / 50 GB | $6.99/mo | Requires $167.76 prepaid for 24 months; renews at $11.99/mo; game panel with one-click modpacks |
| Liquid Web | Wood: 1 vCPU / 2 GB / 60 GB | $11/mo | Page pricing dated November 2024; Iron (4 GB) $17, Netherite (8 GB) $45 |

The honest split: Hostinger's game panel is easier if you want modpack installs from a dashboard and no command line. Evoxt gives you a plain VM with root, a high-clock CPU and a flat monthly price, which suits anyone comfortable with SSH. Liquid Web's published prices are the oldest of this group, so treat them as indicative rather than current.

Community write-ups of Evoxt note that its abuse detection can be aggressive toward unusual traffic patterns such as proxies and port scanning. A Minecraft server is a conventional workload, but if you plan to run something exotic on the same box, start with a monthly term.

## Getting the server running

Evoxt doesn't sell a preconfigured Minecraft image, so the setup is the standard Linux path. Pick Ubuntu when you deploy, then:

1. SSH in as root.
2. `sudo apt update && sudo apt upgrade`
3. Install Java 17 or newer, for example `sudo apt install openjdk-17-jre`, or `openjdk-21-jre-headless` for 1.20.5 and later.
4. `mkdir minecraft` and move into it.
5. Download the server jar for your chosen server type (Paper for performance, Fabric or Forge for modpacks, the official Mojang jar for vanilla).
6. Start it once with `java -Xmx2G -Xms2G -jar server.jar nogui`, adjusting `-Xmx` to roughly the RAM you bought.
7. Open `eula.txt`, set `eula=true`, save.
8. Edit `server.properties` for view distance, difficulty, player slots and online mode.
9. Open **25565/TCP** for Java Edition in the firewall. Bedrock's dedicated server uses **19132/UDP**, a different port and a different protocol.
10. Restart the server and connect from the client.
11. Schedule backups, even with Evoxt's weekly offsite backups in place, since those won't save you from a bad plugin install ten minutes ago.

If you want Java and Bedrock players on one world, run a Java server and put GeyserMC in front of it. A successful start looks like this in your console: the version line, then `Done, listening on *:25565`.

Running the jar inside `screen` or `tmux` keeps it alive after you disconnect. 👉 [Start with a monthly VM-2 to test your modpack](https://bit.ly/EvoXt)

## Questions people ask before ordering

**Can 2 GB run a modded server?** Not a big pack. Vanilla with a handful of plugins, yes. All the Mods or a Create-heavy pack on 2 GB will stutter or crash on world load. Buy VM-4.

**Java and Bedrock at the same time?** Only with a bridge. Java listens on 25565/TCP, Bedrock on 19132/UDP, and Geyser translates between them. Both need to be reachable.

**Do I need more than one IP?** Only if you're running a proxy in front of multiple backend servers, or you want to keep an address stable while rebuilding. Extra IPs are $3/month.

**Can I upgrade RAM or disk later?** Evoxt lets you add individual resources without switching to a different plan, which is the cheaper path when a world outgrows VM-2 but hasn't outgrown the next tier's price. Confirm the resize process with support before you buy if a same-day migration matters to you.

**What happens if I go over the transfer allowance?** The plan table lists caps but not overage handling. Ask before you buy if you expect public Dynmap or a Bedrock bridge with steady traffic.

**Is there a refund window?** Not stated on the plan pages, so check with Evoxt directly before paying for a long term.

## Picking the right plan

Three rules cover most buyers.

Playing vanilla survival with friends: **VM-1, $5.99/month**. Don't pay for cores you won't use, and don't prepay three years for a world that might last two months.

Running ATM, FTB or a Create-heavy pack: **VM-4, $23.99/month**. 8 GB plus 60 GB of disk is where modpacks stop being a gamble. Starting on VM-2 at $11.99 to test whether the pack even loads for your group is a reasonable first month.

Opening a public server with plugins: **VM-8, $47.99/month**, plus $3/month for each extra IP if you split proxy and backends. At that player count, the 16 GB and the 3 TB transfer allowance both matter.

Before you pay, confirm three things: the transfer allowance for the specific location you chose (premium network regions differ), whether your existing world's region files will fit the disk you're buying, and the current term options, since Evoxt bills monthly through three-year prepay and the discount structure isn't the same at every length.

👉 [Pick a plan and deploy in the Evoxt console](https://bit.ly/EvoXt)
