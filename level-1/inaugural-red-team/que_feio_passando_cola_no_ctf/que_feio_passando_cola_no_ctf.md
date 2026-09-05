# CTF Writeup — Que Feio Passando Cola no CTF / How Awful to Cheat in a CTF

| | |
|---|---|
| **Category** | Network Forensics / Packet Analysis |
| **Difficulty** | Medium |
| **Flag** | `Hhj7kmT` |
| **Files** | `flag.pcap` |

---

## 🇬🇧 English

### Challenge Description
> There is a suspicion that two students (hooax and coridora) exchanged a flag during the CTF, but neither wants to confess. No problem: we have the crime scene evidence! Your mission is to find the flag they exchanged, contained in the pcap file below with a snippet of the communication between the two students.

### Analysis
The provided `.pcap` file was opened in **Wireshark**. Since one of the suspects' aliases was known in advance, the fastest path to the relevant traffic was a display filter targeting that string directly:

```
frame contains "hooax"
```

This immediately isolated the packets belonging to the suspicious conversation, cutting through the rest of the capture's background noise. From there, the matching packets were followed as a **TCP stream** to reconstruct the full conversation in order.

### Solution
Following the TCP stream between the two hosts (client `192.168.1.116` and server `192.168.1.5`, port `7777`) revealed a plaintext, netcat-style chat:

```
hooax:    fala hooax
hooax:    aqui é o coridora
hooax:    passa a flag logo
hooax:    antes que acabe o tempo
coridora: cara chato
coridora: a flag é Hhj7kmT
coridora: FUI
```

The flag was sent in plain text, in the middle of the conversation, as confirmed directly in the hex dump of the packet:

```
0040   59 34 e3 ec 61 20 66 6c 61 67 20 c3 a9 20 48 68   Y4..a flag .. Hh
0050   6a 37 6b 6d 54 0a                                 j7kmT.
```

### Key Takeaway
When a suspect's identity or handle is already known, filtering a packet capture directly by that string (`frame contains "..."`) is far faster than scrolling through the entire capture. Following the **TCP stream** afterward reconstructs the full conversation in a readable format, which is essential when the "smoking gun" is transmitted in plaintext over an unencrypted channel.

---

## 🇧🇷 Português

### Descrição do Desafio
> Há uma suspeita de que dois alunos (hooax e coridora) trocaram uma flag no CTF, porém nenhum dos dois quer confessar. Pois bem, sem problemas: temos a prova do crime! Sua missão é encontrar a flag que os dois trocaram no arquivo pcap abaixo, contendo o trecho da comunicação entre os dois alunos.

### Análise
O arquivo `.pcap` fornecido foi aberto no **Wireshark**. Como um dos apelidos dos suspeitos já era conhecido previamente, o caminho mais rápido até o tráfego relevante foi aplicar um filtro de exibição direto por essa string:

```
frame contains "hooax"
```

Isso isolou imediatamente os pacotes pertencentes à conversa suspeita, cortando o ruído do restante da captura. A partir daí, os pacotes correspondentes foram seguidos como um **fluxo TCP (Follow TCP Stream)** para reconstruir a conversa completa em ordem.

### Solução
Seguindo o fluxo TCP entre os dois hosts (cliente `192.168.1.116` e servidor `192.168.1.5`, porta `7777`), foi revelado um chat em texto puro, estilo netcat:

```
hooax:    fala hooax
hooax:    aqui é o coridora
hooax:    passa a flag logo
hooax:    antes que acabe o tempo
coridora: cara chato
coridora: a flag é Hhj7kmT
coridora: FUI
```

A flag foi enviada em texto puro, no meio da conversa, confirmada diretamente no hex dump do pacote:

```
0040   59 34 e3 ec 61 20 66 6c 61 67 20 c3 a9 20 48 68   Y4..a flag .. Hh
0050   6a 37 6b 6d 54 0a                                 j7kmT.
```

### Principal Aprendizado
Quando a identidade ou apelido de um suspeito já é conhecido, filtrar uma captura de pacotes diretamente por essa string (`frame contains "..."`) é muito mais rápido do que rolar a captura inteira manualmente. Seguir o **fluxo TCP** em seguida reconstrói a conversa completa em formato legível, essencial quando a "prova do crime" é transmitida em texto puro por um canal não criptografado.