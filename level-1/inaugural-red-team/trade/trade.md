# CTF Writeup — Trade

| | |
|---|---|
| **Category** | Steganography / Encoding |
| **Difficulty** | Hard |
| **Flag** | `YOU-WINS!` |
| **Files** | `flag.png` (Trade Offer meme image) |

---

## 🇬🇧 English

### Challenge Description
> Can you find the flag?

### Analysis
The provided image was a "Trade Offer" meme (a person on camera, with a "You receive: image / I receive: flag" caption). Standard checks came back clean:

- No EXIF/metadata, no `tEXt`/`zTXt`/`iTXt` PNG chunks
- No data appended after the `IEND` chunk
- No embedded archive signatures (ZIP, RAR, 7z) anywhere in the file
- Manual bit-plane inspection (checking printable-ASCII ratio across all 8 bits × 3 channels) came back as pure noise

Since manual LSB analysis found nothing, the next step was to run **zsteg**, the standard tool for detecting PNG/BMP steganography across dozens of bit/channel/order combinations at once. Zsteg wasn't preinstalled, and RubyGems wasn't reachable in the environment, so its runtime dependencies (`zsteg`, `zpng`, `iostruct`, `rainbow`) were cloned directly from their GitHub repositories and loaded via Ruby's `-I` include-path flag instead of `gem install`.

### Solution
Running zsteg immediately flagged a suspicious string in the very first standard check — **bit 1, Red channel, LSB, row-major (xy) order** — a clean 64-character sequence isolated from the surrounding random pixel noise:

```
FUXC2LJAFUWS2IBOFYWSALJOFYXC4LJAFYWS2IBOFYQC2LRAFYXC4IBNFYWS4LJN
```

This string used only the character set `A-Z2-7`, the signature alphabet of **Base32**. Decoding it produced a second layer:

```
-.-- --- ..- -....- .-- .. -. ... -.-.--
```

This is **Morse code**. Decoding each token:

| Morse | Char |
|---|---|
| `-.--` | Y |
| `---` | O |
| `..-` | U |
| `-....-` | `-` |
| `.--` | W |
| `..` | I |
| `-.` | N |
| `...` | S |
| `-.-.--` | `!` |

Final plaintext:

```
YOU-WINS!
```

### Key Takeaway
When manual LSB checks turn up nothing, don't conclude the image is clean — try a purpose-built tool that automates the search across every bit position, channel, and scan order (`zsteg -a` for PNG/BMP, `steghide`/`stegsolve` for other cases) before ruling out steganography entirely. Also, hidden payloads are often **layered**: what looks like noise may actually be Base32/Base64, which in turn may decode to Morse, binary, or another cipher — always re-inspect each decoded layer before assuming you've reached the final answer.

### Alternative Tools
- **[dcode.fr](https://www.dcode.fr/)** was used to decode both layers (Base32 and Morse) — a handy all-in-one cipher identification and decoding site, useful when you don't want to script the decode by hand.
- **[aperisolve.com](https://www.aperisolve.com/)** is a free online alternative to running `zsteg` locally. It runs the same kind of bit-plane/LSB analysis (along with other stego checks) on an uploaded image and returns the results without needing Ruby or any local setup. Running the same image through Aperisolve reached the exact same conclusion as the local zsteg run — a good option when you can't install zsteg's dependencies in your environment.

---

## 🇧🇷 Português

### Descrição do Desafio
> Será que você consegue achar a flag?

### Análise
A imagem fornecida era um meme "Trade Offer" (uma pessoa na câmera, com a legenda "Você recebe: imagem / Eu recebo: flag"). As verificações padrão vieram limpas:

- Sem EXIF/metadados, sem chunks `tEXt`/`zTXt`/`iTXt` no PNG
- Sem dados anexados após o chunk `IEND`
- Sem assinaturas de arquivo embutido (ZIP, RAR, 7z) em nenhum ponto do arquivo
- Inspeção manual de bit-planes (checando a proporção de ASCII imprimível nos 8 bits × 3 canais) voltou como ruído puro

Como a análise manual de LSB não encontrou nada, o próximo passo foi rodar o **zsteg**, a ferramenta padrão para detectar esteganografia em PNG/BMP testando dezenas de combinações de bit/canal/ordem de uma vez só. O zsteg não vinha pré-instalado, e o RubyGems não estava acessível no ambiente, então suas dependências de runtime (`zsteg`, `zpng`, `iostruct`, `rainbow`) foram clonadas diretamente dos repositórios no GitHub e carregadas via a flag `-I` (include-path) do Ruby, em vez do `gem install`.

### Solução
Rodar o zsteg imediatamente sinalizou uma string suspeita já na primeira checagem padrão — **bit 1, canal Red, LSB, ordem row-major (xy)** — uma sequência limpa de 64 caracteres isolada do ruído aleatório dos pixels ao redor:

```
FUXC2LJAFUWS2IBOFYWSALJOFYXC4LJAFYWS2IBOFYQC2LRAFYXC4IBNFYWS4LJN
```

Essa string usava apenas o conjunto de caracteres `A-Z2-7`, o alfabeto característico do **Base32**. Decodificando, surgiu uma segunda camada:

```
-.-- --- ..- -....- .-- .. -. ... -.-.--
```

Isso é **Código Morse**. Decodificando cada token:

| Morse | Caractere |
|---|---|
| `-.--` | Y |
| `---` | O |
| `..-` | U |
| `-....-` | `-` |
| `.--` | W |
| `..` | I |
| `-.` | N |
| `...` | S |
| `-.-.--` | `!` |

Texto plano final:

```
YOU-WINS!
```

### Principal Aprendizado
Quando as checagens manuais de LSB não encontram nada, não conclua que a imagem está limpa — tente uma ferramenta especializada que automatiza a busca em todas as combinações de posição de bit, canal e ordem de varredura (`zsteg -a` para PNG/BMP, `steghide`/`stegsolve` para outros casos) antes de descartar completamente a esteganografia. Além disso, payloads escondidos costumam vir **em camadas**: o que parece ruído pode na verdade ser Base32/Base64, que por sua vez pode decodificar para Morse, binário ou outra cifra — sempre reinspecione cada camada decodificada antes de assumir que chegou na resposta final.

### Ferramentas Alternativas
- O **[dcode.fr](https://www.dcode.fr/)** foi usado para decodificar as duas camadas (Base32 e Morse) — um site completo de identificação e decodificação de cifras, útil quando você não quer escrever o código de decodificação na mão.
- O **[aperisolve.com](https://www.aperisolve.com/)** é uma alternativa online gratuita para rodar o `zsteg` sem precisar instalar nada localmente. Ele executa o mesmo tipo de análise de bit-planes/LSB (junto com outras checagens de esteganografia) em uma imagem enviada e retorna os resultados sem precisar de Ruby ou qualquer configuração local. Rodar a mesma imagem no Aperisolve chegou exatamente na mesma conclusão que a execução local do zsteg — uma boa opção para quando não é possível instalar as dependências do zsteg no seu ambiente.