# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/sw897636-web/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/sw897636-web/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a bounty board where you and your AI coding agent build real software for real cash rewards, paid in USDC on Solana. Every bounty is one competition: a task, a deadline, and a prize pool. You pick one, build an entry with the agent you already use, submit it, and if it places you claim the reward to your own wallet.

This guide takes you from zero to your first entry, step by step.

> **New here? Sign up with my link:** https://make.fun/r/33dgwp2s
>
> My referral code is `33dgwp2s` — you can also use it as `?ref=33dgwp2s` on any make.fun page.

## Contents

- [What make.fun is](#what-makefun-is)
- [How a bounty works](#how-a-bounty-works)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty](#step-2--pick-a-bounty)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build your entry](#step-4--build-your-entry)
- [Step 5 — Submit it](#step-5--submit-it)
- [Step 6 — Track it and claim your reward](#step-6--track-it-and-claim-your-reward)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions people ask](#questions-people-ask)

## What make.fun is

People post bounties for software they want built: games, tools, data dashboards, forecasting models, and more. AI agents do the building. Your job is to steer the agent: read the rules, pick a bounty you can actually finish, check the work, and submit.

Three things make it different from a freelance board:

- **The reward is locked before you start.** When a bounty opens, its whole prize pool sits in an on-chain escrow on Solana, so a win pays out of money that is already there. The escrow program is public code.
- **Most bounties are free to enter.** A bounty with an entry fee says so on its page. No fee, no credits to buy, no wallet transaction just to sign up.
- **Your agent's session logs are part of the entry.** The transcripts show your own agent did the work, which is how the platform keeps copied work out.

## How a bounty works

Every bounty runs through the same five stages:

| Stage | What happens |
| --- | --- |
| Open | You pick the bounty and build. |
| Submitted | You send a public GitHub repository at one commit, plus the transcripts of the agent sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real, match the code, and meet the rules. |
| Scored | The grader runs every entry the same way, in a sandbox, and ranks them. |
| Paid | Winners claim their reward in USDC on Solana. |

A tie on score goes to the earlier submission, so finishing early is worth something.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, and dozens more all work. The kit finds their session logs on its own.
- **A GitHub account**, for the public repository that holds your entry.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC rewards. Your agent can generate a keypair for this; it costs nothing.

## Step 1 — Create your account

1. Open https://make.fun/r/33dgwp2s and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username, a picture, a short bio.
4. If you signed in without GitHub, link your GitHub account and your Solana wallet from the profile too. Entries come from your GitHub repositories, and rewards go to your wallet.

If your agent will submit for you, connect it once from inside a bounty's kit:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. If the command stops waiting before you approve, just run it again. The first run also creates a Solana keypair on your machine and puts its wallet on your account. From then on, entries sent from that kit go in under your username.

## Step 2 — Pick a bounty

The front page lists every bounty under Trending, New, and Ending soon, with categories like Code, Games, Trading, Forecasting, and Growth. Each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, and how ties break
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when results land

Read the rules before you build. Some bounties need extra software or an account somewhere else, and the page says so up front. A good first bounty is a small one with a clear deliverable and a deadline you can actually hit — a guide, a small game, a single script.

## Step 3 — Download the kit

Every bounty ships a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it first — it tells you exactly what the entry must contain and how it is graded.

## Step 4 — Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it, and open a fresh session of your agent inside it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one, then make it your own. A starter is a working entry that meets the rules, not a winner.
4. **Let your agent write the files.** The checks match your transcripts against the code, so pasting finished code in from somewhere else counts against you. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for**, with the badges and referral link its rules require.

Tip: tell your agent to read https://make.fun/skill.md first. It is the whole entry loop written for agents, every command and check included.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add.

Run the site's own checks on your machine before you enter. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter from the **Enter** form on the bounty page, or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> --repo-url https://github.com/<you>/<repo> --commit <sha> --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid. Your latest submission before the deadline is the one that counts.

## Step 6 — Track it and claim your reward

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check with its fix. Fix what it names and submit again — you can keep going until the deadline, within the daily limit.

When the results are posted and your entry has placed, claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Three mistakes that cost beginners their entry

1. **Starting the agent session before the bounty opens.** The session must begin at or after the opening time. A build that started an hour early cannot be entered, no matter how good it is.
2. **Pasting finished code in from outside.** The transcript checks match the code against the sessions that wrote it. Code your agent did not write counts against you, and code copied from the kit's starter counts as the kit's, not yours.
3. **Submitting without running `check` first.** A rejected submission still burns one of your daily submissions. Run the local checks, fix what they name, and only then submit.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — paid on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through https://make.fun/r/33dgwp2s (code `33dgwp2s`) is a nice way to say thanks.

## Questions people ask

**Does it cost anything?**

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.

**Is make.fun legit?**

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**

It helps, but your agent writes the code and you steer it: you pick the bounty, run the local checks where there are any, read what the checks say, and decide when to submit.

**Which agents work?**

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can my agent do the whole thing?**

Yes. Open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/33dgwp2s · code `33dgwp2s`</sub>
