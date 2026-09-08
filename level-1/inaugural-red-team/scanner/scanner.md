# CTF Writeup — Scanner

| | |
|---|---|
| **Category** | OSINT |
| **Difficulty** | Hard |
| **Flag** | `06/12/11` |
| **Files** | N/A (research/OSINT challenge) |

---

## 🇬🇧 English

### Challenge Description
> It was 2011, in mid-September, when Vinícius Vieira published on his old blog sejalivre.org about a Port Scanning tool for Windows and Linux, an alternative to NMAP. The company that developed this tool also created a scanner for NetBIOS sharing, which was little known. Can you figure out the release date of the last release of **that referred tool**? Accepted flag format: DD/MM/YY (including the slashes).

### Analysis
The key to this challenge was a wording trap: the question asks for the last release date of **"that referred tool"** — and the *most recently referred* tool in the description is not the port scanner (Pscan), but the **NetBIOS share scanner** mentioned right after it. Several attempts were spent chasing the port scanner's release history before recognizing this.

**Step 1 — Finding the original post via the author himself.** Searching for the blog name plus the author's name surfaced Vinícius Vieira's own LinkedIn profile, where he had shared a Wayback Machine link to his old blog. Filtering his posts for "nmap" led directly to the archived snapshot:
`web.archive.org/web/20150606.../sejalivre.org/pscan-uma-alternativa-ao-nmap/`

**Step 2 — Reading the archived post.** The post ("Pscan – Uma alternativa ao nmap", 24/09/2011) states the tool was created by the **Blue Collar Union** group, initially for Windows, with a Linux beta hosted on SourceForge under GPLv2.

**Step 3 — Confirming the group on SourceForge.** `sourceforge.net/projects/pscan/` confirms: *"developed by the Blue Collar Hacker's Union"*, GPLv2, registered in 2000.

**Step 4 — Linking the group to another tool (NetBIOS).** Searching "Blue Collar Union" + NetBIOS/share scanner leads to **SecPoint**, whose free-tools portfolio lists both a Port Scanner and a **NetBIOS Share Scanner** side by side — matching the "little known" sibling tool from the challenge description.

**Step 5 — Checking the changelog.** `secpoint.com/netbios-share-scanner.html` shows the tool's only release (version 1.0) dated **6 December 2011**.

### Solution
```
Tool referenced last in the description: NetBIOS Share Scanner (SecPoint)
Release: 1.0
Date: 6 December 2011
```

Flag:
```
06/12/11
```

### Key Takeaway
Read challenge descriptions literally, word by word — "that referred tool" ("dessa referida ferramenta") points grammatically to the last tool named in the text, not necessarily the one the challenge *opens* with. A misreading here cost several wrong submissions chasing the wrong tool's version history before the actual target (the NetBIOS scanner, not the port scanner) was identified.

---

## 🇧🇷 Português

### Descrição do Desafio
> Era 2011, em meados de setembro, quando o Vinícius Vieira publicou em seu antigo blog sejalivre.org sobre uma ferramenta de Port Scanning para Windows e Linux que era uma alternativa ao NMAP. A empresa desenvolvedora dessa ferramenta também criou um scanner para compartilhamento NetBIOS, o qual foi pouco conhecido. Será que você consegue descobrir qual a data da última release **dessa referida ferramenta**? O formato aceito para flag é DD/MM/AA (incluindo as barras).

### Análise
A chave desse desafio era uma pegadinha de interpretação de texto: a pergunta pede a data da última release **"dessa referida ferramenta"** — e a ferramenta *mais recentemente referida* no enunciado não é o port scanner (Pscan), e sim o **scanner de compartilhamento NetBIOS** citado logo depois. Várias tentativas foram gastas perseguindo o histórico de versões do port scanner antes de perceber isso.

**Passo 1 — Achar o post original via o próprio autor.** Pesquisando no Google o nome do blog + o nome do autor, chegamos ao próprio perfil do Vinícius Vieira no LinkedIn, onde ele compartilhou um link do Wayback Machine para o blog antigo. Filtrando os posts dele por "nmap", chega-se direto ao snapshot arquivado:
`web.archive.org/web/20150606.../sejalivre.org/pscan-uma-alternativa-ao-nmap/`

**Passo 2 — Ler o conteúdo do post arquivado.** O post ("Pscan – Uma alternativa ao nmap", 24/09/2011) revela que a ferramenta foi criada pelo grupo **Blue Collar Union**, inicialmente para Windows, com versão beta para Linux no SourceForge, licenciada GPLv2.

**Passo 3 — Confirmar o grupo no SourceForge.** `sourceforge.net/projects/pscan/` → confirma *"developed by the Blue Collar Hacker's Union"*, GPLv2, registrado em 2000.

**Passo 4 — Ligar o grupo a outra ferramenta (NetBIOS).** Busca por "Blue Collar Union" + NetBIOS/share scanner leva à **SecPoint**, que mantém no portfólio de ferramentas gratuitas tanto um Port Scanner quanto o **NetBIOS Share Scanner** lado a lado — batendo com a ferramenta "pouco conhecida" citada no desafio.

**Passo 5 — Changelog da ferramenta.** `secpoint.com/netbios-share-scanner.html` → única versão lançada (1.0), datada de **6 de dezembro de 2011**.

### Solução
```
Ferramenta referida por último no enunciado: NetBIOS Share Scanner (SecPoint)
Release: 1.0
Data: 6 de dezembro de 2011
```

Flag:
```
06/12/11
```

### Principal Aprendizado
Leia as descrições de desafios literalmente, palavra por palavra — "dessa referida ferramenta" aponta gramaticalmente para a última ferramenta citada no texto, não necessariamente para aquela com que o desafio *abre*. Uma leitura equivocada aqui custou várias submissões erradas perseguindo o histórico de versões da ferramenta errada, antes de identificar o alvo real (o scanner NetBIOS, não o port scanner).