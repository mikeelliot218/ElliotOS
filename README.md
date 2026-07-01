<div align="center">

```
███████╗██╗     ██╗     ██╗ ██████╗ ████████╗ ██████╗ ███████╗
██╔════╝██║     ██║     ██║██╔═══██╗╚══██╔══╝██╔═══██╗██╔════╝
█████╗  ██║     ██║     ██║██║   ██║   ██║   ██║   ██║███████╗
██╔══╝  ██║     ██║     ██║██║   ██║   ██║   ██║   ██║╚════██║
███████╗███████╗███████╗██║╚██████╔╝   ██║   ╚██████╔╝███████║
╚══════╝╚══════╝╚══════╝╚═╝ ╚═════╝    ╚═╝    ╚═════╝ ╚══════╝
```

**O primeiro sistema de pentest nativo para Android — sem root, no bolso.**

[![Plataforma](https://img.shields.io/badge/Plataforma-Android%20%2F%20Termux-green?style=flat-square)](https://github.com/mikeelliot218/ElliotOS)
[![Root](https://img.shields.io/badge/Root-NÃO%20necessário-brightgreen?style=flat-square)](#)
[![Linguagem](https://img.shields.io/badge/Lua%205.4%20%2B%20C%20puro-blue?style=flat-square)](#)
[![Licença](https://img.shields.io/badge/Licença-MIT-lightgrey?style=flat-square)](#licença)
[![Gratuito](https://img.shields.io/badge/Gratuito-100%25-orange?style=flat-square)](#)

</div>

---

## O que é o ElliotOS?

O ElliotOS é um sistema operacional de segurança e pentest construído **dentro do Termux**, o emulador de terminal do Android. Desenvolvido por **Mike Elliot**, nasceu de uma necessidade real: não existia nenhum toolkit de pentest funcional para Android.

Kali Linux, Black Arch, Parrot OS — todos exigem PC. O ElliotOS roda no bolso, direto do celular, **sem root, sem VM, sem frescura**.

Tudo é compilado e instalado via um único script (`luascript.sh`), que constrói do zero:
- Um interpretador Lua 5.4 customizado com extensões de rede (`lua-net`)
- Uma biblioteca C com 23 módulos de segurança embutidos (`libnet.so`)
- Uma IA nativa chamada **CYN**, integrada diretamente ao binário
- Ferramentas próprias: `ms`, `lpm`, `xpm`, `cxx`, `ee`

---

## Instalação

> **Requisitos:** Android com [Termux](https://f-droid.org/packages/com.termux/) instalado via F-Droid. Sem root.

```bash
# 1. Instale o Termux pelo F-Droid (não use a versão da Play Store — está desatualizada)
# 2. No Termux:

pkg update -y && pkg install -y git wget curl

git clone https://github.com/mikeelliot218/ElliotOS.git
cd ElliotOS
bash luascript.sh
```

A instalação compila tudo do zero e leva cerca de **15 a 20 minutos** dependendo do dispositivo. Nenhuma etapa exige root.

---

## Ferramentas incluídas

### Binários nativos (compilados em C)

| Comando | Descrição |
|---------|-----------|
| `ms` | MoonStyle — REPL interativo Lua 5.4 com extensões de rede |
| `lua-net` | Interpretador Lua com 23 módulos de segurança embutidos |
| `luar` | Alias do lua-net para scripts avançados |
| `lpm` | Gerenciador de pacotes Lua (instala módulos .lua e exploits) |
| `xpm` | Gerenciador de ferramentas de pentest (instala ferramentas sem root) |
| `cxx` | Compilador C/C++ simplificado para o ambiente ElliotOS |
| `ee` | Editor de texto nativo em C, leve e rápido |

### CYN — IA nativa

```
ms -a
```

A CYN é a inteligência artificial integrada diretamente no ElliotOS. Ela conhece todos os módulos, flags, funções e a arquitetura do sistema. Responde sempre em português, é técnica, objetiva e focada em segurança.

Suporta múltiplos providers: **Gemini**, **OpenAI**, **Claude** e outros — configuráveis via `ms -a`.

### Módulos de segurança (`mod.*`)

Dentro do REPL (`ms`), você tem acesso a módulos de pentest nativos em Lua:

```lua
-- Reconhecimento
mod.recon.dns("alvo.com")
mod.recon.whois("alvo.com")
mod.recon.headers("https://alvo.com")

-- Scanning
mod.scan.ports("192.168.1.1", {22, 80, 443, 8080})
mod.scan.tcp("192.168.1.1", 80)

-- Web
mod.web.get("https://alvo.com")
mod.web.post("https://alvo.com/login", {user="admin", pass="teste"})

-- Crypto
mod.crypto.md5("texto")
mod.crypto.sha256("texto")
mod.crypto.base64_encode("texto")

-- SQLite integrado
local db = sqlite.open("resultados.db")
```

---

## XPM — Gerenciador de Pentest

O `xpm` instala ferramentas de segurança **sem usar o repositório do Termux** (que não tem ferramentas de pentest). Tudo é compilado do código-fonte ou instalado via pip/go/cargo diretamente.

```bash
# Ver todas as ferramentas disponíveis
xpm search list

# Buscar ferramenta específica
xpm search nmap

# Instalar uma ferramenta
xpm install sqlmap

# Instalar várias de uma vez
xpm install sqlmap nikto dirsearch nmap

# Ver o que está instalado
xpm list

# Atualizar uma ferramenta
xpm update sqlmap

# Remover
xpm remove sqlmap

# Diagnóstico geral
xpm doctor
```

### Ferramentas disponíveis no XPM

| Categoria | Ferramenta | Método de instalação |
|-----------|------------|----------------------|
| Scanner | nmap, rustscan, naabu | Compilado do fonte |
| Web | sqlmap, nikto, commix, whatweb, xsstrike | pip / fonte |
| Fuzzing | ffuf, gobuster, dirsearch, wfuzz | go / pip |
| Reconhecimento | amass, subfinder, assetfinder, dnsrecon | go / pip |
| OSINT | sherlock, maigret, holehe, sublist3r, theharvester | pip |
| Password | hydra, john | Compilado do fonte |
| Exploração | metasploit, sqlmap, searchsploit, slowloris | gem / pip / fonte |
| Engenharia Reversa | radare2, binwalk, ropper, androguard | fonte / pip |
| MITM | mitmproxy | pip |
| Malware | yara | Compilado do fonte |
| Eng. Social | zphisher | github |
| CTF / Binários | pwntools | pip |
| Wordlists | seclists | github |
| AD / Rede | impacket, nuclei | pip / go |

> **Nenhuma ferramenta exige root para ser instalada ou usada no Termux.**

---

## LPM — Gerenciador de Pacotes Lua

O `lpm` instala módulos Lua e scripts de exploit:

```bash
# Instalar módulo do LuaRocks
lpm install luasocket

# Buscar exploits no GitLab/PacketStorm/GitHub (cache 24h)
lpm --script eternalblue

# Instalar exploit por nome
lpm install --from exploit eternalblue

# Listar módulos instalados
lpm list
```

---

## Scripts de exemplo

O ElliotOS instala scripts prontos em `/usr/share/lua-scripts/`:

```bash
# Tutorial interativo do Lua no ElliotOS
ms -f /usr/share/lua-scripts/learn.lua

# Reconhecimento básico de um alvo
ms -f /usr/share/lua-scripts/recon.lua -- alvo.com

# Port scan via Lua nativo
ms -f /usr/share/lua-scripts/portscan.lua -- 192.168.1.1

# Verificação HTTP
ms -f /usr/share/lua-scripts/webcheck.lua -- https://alvo.com
```

---

## Interface Gráfica (opcional)

O ElliotOS suporta ambiente gráfico XFCE4 via Termux:X11:

```bash
# Requisito: instale o app Termux:X11 pelo F-Droid ou GitHub Releases

# Instala o ambiente gráfico automaticamente junto com o ElliotOS
# Se já estiver instalado, para iniciar:
elliot-gui

# Encerrar
elliot-gui --kill
```

---

## Estrutura do projeto

```
ElliotOS/
├── luascript.sh          # Script único de instalação (~104k linhas)
│   ├── libnet.c          # Biblioteca C com 23 módulos de segurança
│   ├── Lua 5.4 source    # Interpretador customizado
│   ├── lua-net binary    # Embutido como heredoc compilado na instalação
│   ├── xpm               # Gerenciador de pentest (Bash)
│   ├── lpm               # Gerenciador de pacotes Lua (Bash)
│   ├── cxx               # Compilador wrapper (Bash)
│   ├── ee                # Editor nativo (C, embutido)
│   └── scripts/          # learn.lua, recon.lua, portscan.lua, webcheck.lua
└── README.md
```

---

## Configurando a CYN (IA)

```bash
# Abre o chat com a CYN
ms -a

# Na primeira execução, ela pede a chave de API.
# Suporta: Gemini (gratuito), OpenAI, Claude (Anthropic), e outros.
```

Para obter uma chave gratuita do Gemini: [aistudio.google.com](https://aistudio.google.com)

---

## Requisitos de hardware

| Item | Mínimo |
|------|--------|
| Android | 7.0+ |
| RAM | 2 GB |
| Armazenamento livre | 2 GB (com ferramentas XPM, mais) |
| Root | **Não necessário** |
| Conexão | Necessária apenas na instalação |

---

## Autor

**Mike Elliot** — desenvolvedor independente, criador do ElliotOS.

- YouTube: [@Mikeelliotmkll12](https://youtube.com/@Mikeelliotmkll12)
- GitHub: [github.com/mikeelliot218](https://github.com/mikeelliot218)

---

## Licença

MIT — livre para usar, estudar, modificar e distribuir. Gratuito para sempre.

---

<div align="center">

*"Black Arch, Kali, Parrot — todos no PC. O ElliotOS fica no bolso."*

**⭐ Se o projeto te ajudou, deixa uma estrela no repositório.**

</div>
