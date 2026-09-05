# CTF Writeup — Base do Problema / Problem Base

| | |
|---|---|
| **Category** | Cryptography / Encoding |
| **Difficulty** | Easy |
| **Flag** | `FIAP{PosTechRedTeamOperationsFiapAlura2026}` |
| **Files** | N/A (message provided in challenge description) |

---

## 🇬🇧 English

### Challenge Description
> You intercepted the following message transmitted by a legacy system: `Vm14V2FrNVhWbk5YYTJoWFlsaENiMVZ0ZEhkak1XUnlWMnhPYVZKdGVGbFVWbHBEWVd4SmVGZHFWbGhXYldoVVdUQmtTbVZWTlZsalJrNXBWak5vZGxkVVFsZFNNazE1Vld4c1ZHSlhhRTlaVjNSSFRsWlNkRmw2YkZGVlZEQTU=`

### Analysis
The intercepted string was pure Base64-alphabet text (`A-Za-z0-9+/=`), a strong indicator of encoded — not encrypted — data. Decoding it once did not immediately produce readable plaintext; instead, it returned another valid Base64 string, revealing that the message had been **encoded multiple times in sequence**.

### Solution
Using CyberChef's **Magic Wand** (recipe auto-detection), the encoding chain was identified and unwound layer by layer:

```
Layer 1 (Base64) -> Layer 2 (Base64) -> Layer 3 (Base64) -> Plaintext
```

| Step | Output |
|---|---|
| Decode #1 | `VlVjNWVsWkhWbXBoUmtwc1drWlNiRmxYTVZCalIxWjVXVmhTY0dJeU5YcFNiV3hvWTBWR2MyUllTbWhOYWtGNVRtYzlQUT09` |
| Decode #2 | `VmxWak5XVnNXa2hXYlhCb1VtdHdjMWRyV2xOaVJteFlUVlpDYWxJeFdqVlhWbWhUWTBkSmVVNVljRk5pVjNodldUQldSMk15VWxsVGJXaE9ZV3RHTlZSdFl6bFFVVDA5` |
| Decode #3 (final) | `PosTechRedTeamOperationsFiapAlura2026` |

Wrapping the final plaintext in the standard flag format:

```
FIAP{PosTechRedTeamOperationsFiapAlura2026}
```

### Key Takeaway
Not all encoding is single-layer. When a decoded string still resembles valid Base64 (clean alphabet, `=` padding, length divisible by 4), always attempt to decode it again. Tools like CyberChef's Magic Wand automate this detection, but manually recognizing repeated Base64 patterns is a fundamental skill for encoding-based CTF challenges.

---

## 🇧🇷 Português

### Descrição do Desafio
> Você interceptou a seguinte mensagem transmitida por um sistema legado: `Vm14V2FrNVhWbk5YYTJoWFlsaENiMVZ0ZEhkak1XUnlWMnhPYVZKdGVGbFVWbHBEWVd4SmVGZHFWbGhXYldoVVdUQmtTbVZWTlZsalJrNXBWak5vZGxkVVFsZFNNazE1Vld4c1ZHSlhhRTlaVjNSSFRsWlNkRmw2YkZGVlZEQTU=`

### Análise
A string interceptada era composta puramente pelo alfabeto Base64 (`A-Za-z0-9+/=`), um forte indicativo de dados codificados — e não criptografados. Decodificá-la uma vez não resultou em texto legível imediatamente; em vez disso, retornou outra string Base64 válida, revelando que a mensagem havia sido **codificada múltiplas vezes em sequência**.

### Solução
Usando a **Magic Wand** do CyberChef (detecção automática de receita), a cadeia de codificação foi identificada e desfeita camada por camada:

```
Camada 1 (Base64) -> Camada 2 (Base64) -> Camada 3 (Base64) -> Texto plano
```

| Etapa | Saída |
|---|---|
| Decodificação #1 | `VlVjNWVsWkhWbXBoUmtwc1drWlNiRmxYTVZCalIxWjVXVmhTY0dJeU5YcFNiV3hvWTBWR2MyUllTbWhOYWtGNVRtYzlQUT09` |
| Decodificação #2 | `VmxWak5XVnNXa2hXYlhCb1VtdHdjMWRyV2xOaVJteFlUVlpDYWxJeFdqVlhWbWhUWTBkSmVVNVljRk5pVjNodldUQldSMk15VWxsVGJXaE9ZV3RHTlZSdFl6bFFVVDA5` |
| Decodificação #3 (final) | `PosTechRedTeamOperationsFiapAlura2026` |

Encapsulando o texto plano final no formato padrão de flag:

```
PosTechRedTeamOperationsFiapAlura2026
```

### Principal Aprendizado
Nem toda codificação é feita em camada única. Quando uma string decodificada ainda se parece com Base64 válido (alfabeto limpo, padding `=`, comprimento múltiplo de 4), sempre tente decodificá-la novamente. Ferramentas como a Magic Wand do CyberChef automatizam essa detecção, mas reconhecer manualmente padrões de Base64 repetidos é uma habilidade fundamental em desafios de codificação em CTFs.