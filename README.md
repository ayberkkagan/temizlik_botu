import discord
from discord.ext import commands
import asyncio
import os
import random
import requests

intents = discord.Intents.default()
intents.message_content = True
intents.members = True

bot = commands.Bot(command_prefix='$', intents=intents)

@bot.event
async def on_ready():
    print(f'{bot.user} olarak giriş yaptık')

@bot.event
async def on_member_join(member):
    channel = member.guild.system_channel  
    if channel:
        await channel.send(f'Hoş geldin {member.mention}! Sunucumuza katıldığın için teşekkürler!')

@bot.event
async def on_member_remove(member):
    channel = member.guild.system_channel  
    if channel:
        await channel.send(f'{member.name} sunucudan ayrıldı. Görüşmek üzere!')

@bot.command()
async def hello(ctx):
    await ctx.send(f'Merhaba! Ben {bot.user}, bir Discord sohbet botuyum!')

@bot.command()
async def heh(ctx, count_heh = 5):
    await ctx.send("he" * count_heh)

@bot.command()
async def cevrekirliligi(ctx):
    await ctx.send(f'Cevre kirliligi, doganin dengesini bozan en buyuk tehlikelerden biridir. Hava, su ve toprak kirlenmesi insan sagligini ve ekosistemi tehdit eder. Dogayi korumak icin geri donusum ve tasarruf bilinci sarttir. ')

@bot.command()
async def cevre_kirliligi_icin_ne_yapabilirim(ctx):
    await ctx.send('''evre kirliligini azaltmak icin:

Atiklarini geri donusume ayir.

-Plastik kullanimini azalt.

-Enerji ve su tasarrufu yap.

-Toplu tasima veya bisiklet kullan.

-Agac dik ve dogayi koru.

-Diger insanlari da bu konuda bilinclendir.''')
    


@bot.command()
async def orn_gorsel(ctx):


    with open('aa/OIP.webp', 'rb') as f:
   
        # Dönüştürülen Discord kütüphane dosyasını bu değişkende saklayalım!
        picture = discord.File(f)
   # Daha sonra bu dosyayı bir parametre olarak göndere biliriz!
    await ctx.send(file=picture)

    
@bot.command()
async def meme (ctx):
    files = os.listdir('images')
    selected_file = random.choice(files)

    with open(f'images/{selected_file}', 'rb') as f:
   
        # Dönüştürülen Discord kütüphane dosyasını bu değişkende saklayalım!
        picture = discord.File(f)
   # Daha sonra bu dosyayı bir parametre olarak gönderebiliriz!
    await ctx.send(file=picture)

def get_duck_image_url():    
    url = 'https://random-d.uk/api/random'
    res = requests.get(url)
    data = res.json()
    return data['url']


@bot.command('duck')
async def duck(ctx):
    '''duck komutunu çağırdığımızda, program ordek_resmi_urlsi_al fonksiyonunu çağırır.'''
    image_url = get_duck_image_url()
    await ctx.send(image_url)


bot.run("Botun Tokeni")

