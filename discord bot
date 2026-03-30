import discord
from discord.ext import commands
from discord.ui import Button, View
import asyncio
import os

TOKEN = os.getenv("SOURCEHUB_BOT_TOKEN")

# Enable all intents including message content
intents = discord.Intents.all()
bot = commands.Bot(command_prefix=".", intents=intents)

RAID_MESSAGE = """
--------------------------------
           #SourceHub ⚡️
--------------------------------

--------  raid bot ﹒roblox beaming ﹒selling  ------------

-----   🤡 join to RAID any server! Without Admin perms, free to use ⚡️   --------

✅ RAID ANY SERVER WITHOUT ADMIN ⚡️
✅ TOKEN LOGGING BEST METHODS !
✅ Available on all devices!

https://discord.gg/v6Np7pyvM

@everyone @here
"""

EXTERNAL_APP_INVITE = "https://discord.com/oauth2/authorize?client_id=1487140117385580835&integration_type=1&scope=applications.commands"

class ExternalAppButton(View):
    def __init__(self):
        super().__init__(timeout=None)
        self.add_item(Button(
            label="Add SourceHub as External App",
            style=discord.ButtonStyle.danger,
            emoji="⚡",
            url=EXTERNAL_APP_INVITE
        ))

@bot.event
async def on_ready():
    await bot.tree.sync()
    print(f"✅ {bot.user} is online and ready to raid.")
    print(f"💀 Bot ID: {bot.user.id}")
    print("💀 /raid - Spams raid message 5 times")
    print("💀 /say - Send custom message (blocks invites)")
    print("💀 /help - Show commands")
    print("💀 .sourcehub - Get external app invite in DMs")

async def start_hidden(interaction: discord.Interaction):
    await interaction.response.send_message("💀 Raid deployed.", ephemeral=True)

# /raid → Sends SourceHub message 5 times
@bot.tree.command(name="raid", description="💀 DEPLOY SOURCEHUB RAID MESSAGE (5x spam)")
async def raid(interaction: discord.Interaction):
    await start_hidden(interaction)
    for i in range(5):
        await interaction.followup.send(RAID_MESSAGE)
        await asyncio.sleep(0.5)

# /say → BLOCK invite links
@bot.tree.command(name="say", description="Send a custom message (invite links are blocked)")
async def say(interaction: discord.Interaction, message: str):
    await start_hidden(interaction)
    if not message.strip():
        await interaction.followup.send("Message cannot be empty.")
        return
    if "discord.gg/" in message.lower() or "discord.com/invite" in message.lower():
        await interaction.followup.send("❌ Invite links are not allowed in this command.")
        return
    message = message.replace("@everyone", "@ everyone")
    message = message.replace("@here", "@ here")
    await interaction.followup.send(message)

# /help → Show commands
@bot.tree.command(name="help", description="💀 Show commands and how to add the bot")
async def help_cmd(interaction: discord.Interaction):
    embed = discord.Embed(
        title="💀 **SOURCEHUB - EXTERNAL RAID APP** 💀",
        description="**Raid ANY server without adding a bot!**",
        color=0xff0000
    )
    embed.add_field(
        name="⚡ COMMANDS ⚡",
        value="• `/raid` - Spam SourceHub message 5x\n• `/say [message]` - Send custom message\n• `/help` - Show this menu\n• `.sourcehub` - Get external app invite in DMs",
        inline=False
    )
    embed.add_field(
        name="📝 HOW TO GET EXTERNAL APP:",
        value="**Type `.sourcehub` in any channel** — I'll DM you the invite link!\n\n**Once added, `/raid` and `/say` work in EVERY server you're in!**",
        inline=False
    )
    embed.set_footer(text="SourceHub - Created by lucazzz0967 | External App Mode")
    await interaction.response.send_message(embed=embed, ephemeral=False)

# .sourcehub → DM the external app invite
@bot.command(name="sourcehub")
async def sourcehub(ctx):
    try:
        await ctx.message.delete()
    except Exception as e:
        print(f"Failed to delete message: {e}")

    embed = discord.Embed(
        title="⚡ **SOURCEHUB - EXTERNAL RAID APP** ⚡",
        description="**Add me as an External App and raid ANY server!**",
        color=0xff0000
    )
    embed.add_field(
        name="📝 HOW TO ADD:",
        value="1. Click the button below\n2. Pick any server for installation\n3. `/raid` and `/say` work in EVERY server after adding!\n4. No bot needed in each server 🔥",
        inline=False
    )
    embed.add_field(
        name="⚡ FEATURES:",
        value="• RAID ANY SERVER WITHOUT ADMIN PERMS\n• Stealth mode - ephemeral responses\n• Invite link blocking\n• 5x spam waves\n• Works everywhere once added",
        inline=False
    )
    embed.set_footer(text="SourceHub - Created by lucazzz0967 | External App Mode")

    try:
        view = ExternalAppButton()
        await ctx.author.send(embed=embed, view=view)
        await ctx.send("💀 **Check your DMs!** The external app invite is waiting. 💀", delete_after=5)
    except discord.Forbidden:
        await ctx.send("❌ **Can't DM you!** Enable your DMs in Privacy Settings and try again. 😘", delete_after=10)
    except Exception as e:
        await ctx.send(f"❌ Something went wrong. Error: {e}", delete_after=10)

bot.run(TOKEN)
