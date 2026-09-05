# CTF Writeup — Flag 02

| | |
|---|---|
| **Category** | Steganography / Forensics |
| **Difficulty** | Easy |
| **Flag** | `FIAP{welcome_to_the_red_team_ops}` |
| **Files** | `nothing.png` |

---

## 🇬🇧 English

### Challenge Description
> An infiltrated agent sent us a seemingly ordinary image. We suspect there's a secret message hidden inside it. Can you find the flag?

### Analysis
The provided image (`nothing.png`) displayed only the text "Nothing suspicious here..." on a plain background — a deliberate misdirection. Standard visual inspection revealed nothing out of the ordinary, which suggested the payload was not embedded visually but rather appended to or hidden within the file's raw data.

### Solution
Opening the image file directly as plain text (e.g. via a text editor or `cat`/`strings` on the binary content) exposed readable ASCII text appended after the image data, containing the flag in plain sight:

```
FIAP{welcome_to_the_red_team_ops}
```

No decoding, extraction tools (steghide, zsteg, exiftool), or brute-forcing were required — the flag was stored as plain text directly within the file, appended after the PNG binary structure.

### Key Takeaway
Always inspect a file's raw bytes, not just its rendered content. A quick `strings <file>` or opening the file as `.txt` is often the fastest way to catch flags hidden in plain sight, appended after valid file headers/structures — a common and low-effort steganography technique in CTFs.

---

## 🇧🇷 Português

### Descrição do Desafio
> Um agente infiltrado nos enviou uma imagem aparentemente comum. Suspeitamos que há uma mensagem secreta escondida dentro dela. Você consegue encontrar a flag?

### Análise
A imagem fornecida (`nothing.png`) exibia apenas o texto "Nada suspeito aqui..." sobre um fundo simples — uma distração proposital. A inspeção visual padrão não revelou nada fora do comum, o que sugeriu que o payload não estava embutido visualmente, mas sim anexado ou oculto nos dados brutos do arquivo.

### Solução
Ao abrir o arquivo de imagem diretamente como texto puro (por exemplo, via editor de texto ou `cat`/`strings` no conteúdo binário), foi exposto um texto ASCII legível logo após os dados da imagem, contendo a flag à vista:

```
FIAP{welcome_to_the_red_team_ops}
```

Nenhuma ferramenta de extração ou decodificação (steghide, zsteg, exiftool) ou força bruta foi necessária — a flag estava armazenada como texto puro diretamente no arquivo, anexada após a estrutura binária do PNG.

### Principal Aprendizado
Sempre inspecione os bytes brutos de um arquivo, não apenas seu conteúdo renderizado. Um simples `strings <arquivo>` ou abrir o arquivo como `.txt` costuma ser a forma mais rápida de encontrar flags escondidas à vista, anexadas após cabeçalhos/estruturas válidas de arquivo — uma técnica de esteganografia comum e de baixo esforço em CTFs.