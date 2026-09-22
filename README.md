<p align="center">
  <img src="assets/logo.png" alt="Ledger" width="180">
</p>

<h1 align="center">Ledger</h1>

<p align="center">
  <em>A living economy bot for Discord.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-in%20development-orange?style=flat-square" alt="Status">
  <img src="https://img.shields.io/badge/source-private-lightgrey?style=flat-square" alt="Source">
  <img src="https://img.shields.io/badge/license-undecided-lightgrey?style=flat-square" alt="License">
</p>

---

### 🏛️ What is Ledger?

Most economy bots are casinos with a city skin. Ledger is a **persistent simulation** where every action is recorded and every record has consequences.

### ⚙️ Systems

- 🆔 **DBN** — Permanent identity. Jobs, records, and family ties attach to it forever.
- 🏦 **Bank & Cards** — Card number is your username. PIN protects you.
- 💼 **Jobs & Clock** — Apply, get hired, show up for shifts. Miss too many, you're fired.
- ⚖️ **Crime & Records** — Theft, hacking, fraud. Get caught, it follows you forever.
- 🔒 **Jail** — Served in in-game time. Bank freezes, job at risk.
- 🎟️ **Lottery** — Weekly scratch tickets and a live drawing.
- 👨‍👩‍👧 **Family** — Adoption only. Build a tree. Inherit assets.

### 🧠 Philosophy

Your record affects your job. Your job affects your money. Your money makes you a target. Getting caught affects your record.

**Every action is written down.**

### 🛠️ Under the Hood

```python
@bot.tree.command(name="balance", description="check your bank balance")
async def balance(interaction: discord.Interaction):
    user = db.get_user(interaction.user.id)
    if not user:
        await interaction.response.send_message("you dont have an account yet, run /bank open")
        return

    embed = discord.Embed(title="Ledger Bank", color=0x1a2b4a)
    embed.add_field(name="account", value=user.dbn)
    embed.add_field(name="balance", value=f"{user.balance:,} coins")
    embed.set_footer(text="the economy remembers")

    await interaction.response.send_message(embed=embed)