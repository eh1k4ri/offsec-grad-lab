# CTF Writeup — Batatas Fritas / French Fries

| | |
|---|---|
| **Category** | Cryptography / OSINT |
| **Difficulty** | Easy |
| **Flag** | `FIAP{french sign language}` |
| **Files** | `flag_1.jpg` |

---

## 🇬🇧 English

### Challenge Description
> In France and other French-speaking countries, french fries are formally called *pommes de terre frites*, but are more commonly known as *pommes frites*, *patates frites*, or simply *frites*. Replace "decoded text" with the decoded text from the screenshot or from flag.jpg.

The challenge provided a single image containing a grid of hand illustrations, each showing a distinct finger/hand position.

### Analysis
Visual inspection of the image showed no embedded metadata, steganographic artifacts, or hidden text layers — the image itself *was* the cipher. Each hand illustration represented a letter, following a consistent visual alphabet rather than a standard cryptographic scheme (Base64, hex, Caesar, etc.).

Cross-referencing the hand shapes against known manual alphabets identified the source as the **French Sign Language (LSF) fingerspelling alphabet**.

### Solution
Decoding each hand sign in sequence, left to right / top to bottom, produced the following plaintext:

```
french sign language
```

Wrapping the decoded string in the standard flag format used throughout the CTF:

```
FIAP{french sign language}
```

### Notes
As a side note relevant to the challenge's theme: in France and other French-speaking countries, french fries are formally referred to as *pommes de terre frites*, though more commonly known as *pommes frites*, *patates frites*, or simply *frites*.

### Key Takeaway
Not every cipher is digital — recognizing non-standard encodings (visual alphabets, gesture-based systems, semaphore, Morse, Braille, etc.) is a useful skill in CTF cryptography challenges, especially when no metadata or embedded data is found through conventional file analysis.

---

## 🇧🇷 Português

### Descrição do Desafio
> Na França e em outros países francófonos, batatas fritas são formalmente chamadas de *pommes de terre frites*, mas são mais comumente conhecidas como *pommes frites*, *patates frites* ou simplesmente *frites*. Substitua "texto decodificado" pelo texto decodificado da screenshot ou de flag.jpg.

O desafio disponibilizou uma única imagem contendo uma grade de ilustrações de mãos, cada uma representando uma posição distinta de dedos/mão.

### Análise
A inspeção visual da imagem não revelou metadados embutidos, artefatos de esteganografia ou camadas de texto ocultas — a própria imagem *era* a cifra. Cada ilustração de mão representava uma letra, seguindo um alfabeto visual consistente, e não um esquema criptográfico padrão (Base64, hex, César, etc.).

Comparando os formatos das mãos com alfabetos manuais conhecidos, identificou-se a origem como o **alfabeto manual da Língua de Sinais Francesa (LSF)**.

### Solução
Decodificando cada sinal manual em sequência, da esquerda para a direita / de cima para baixo, obteve-se o seguinte texto plano:

```
french sign language
```

Encapsulando a string decodificada no formato padrão de flag utilizado no CTF:

```
FIAP{french sign language}
```

### Observações
Como curiosidade relacionada ao tema do desafio: na França e em outros países francófonos, batatas fritas são formalmente chamadas de *pommes de terre frites*, mas são mais comumente conhecidas como *pommes frites*, *patates frites* ou simplesmente *frites*.

### Principal Aprendizado
Nem toda cifra é digital — reconhecer codificações não convencionais (alfabetos visuais, sistemas baseados em gestos, semáforo, Morse, Braille, etc.) é uma habilidade útil em desafios de criptografia em CTFs, especialmente quando a análise convencional de arquivo não revela metadados ou dados embutidos.