# CTF Writeup — OSINT (David Tofaneli)

| | |
|---|---|
| **Category** | OSINT / Breach Intelligence |
| **Difficulty** | 100 pts |
| **Flag** | `120693` |
| **Target** | David Tofaneli (`david.tofaneli@fiap.com.br`) |
| **Attacker** | Kali Linux / Web OSINT Tools |

---

## 🇬🇧 English

### Challenge
> David Tofaneli, a employee at FIAP, fell victim to a data breach on an e-commerce platform where he mistakenly reused his corporate credentials. Using your OSINT skills, can you discover the password for this credential? The password itself is the flag.

### 1. Target Reconnaissance
The corporate email address was identified following FIAP's standard naming convention:
```
david.tofaneli@fiap.com.br
```

### 2. Breach Data Lookup
Using leak lookup engines, the target email was found in historical breach lists (including LinkedIn and credential stuffing combo lists):
- **Identified SHA-1 Hash:** `1a3be3d2236196f0c428468552885d5e09ee1469`

### 3. Hash Cracking
The 40-character hexadecimal string was identified as an unsalted SHA-1 hash.

Using free online rainbow tables (such as CrackStation or HashCracker):
- **Input Hash:** `1a3be3d2236196f0c428468552885d5e09ee1469`
- **Algorithm:** SHA-1
- **Cracked Plaintext Result:** `120693`

Alternatively, offline via Kali Linux CLI:
```bash
echo "1a3be3d2236196f0c428468552885d5e09ee1469" > hash.txt
hashcat -m 100 hash.txt /usr/share/wordlists/rockyou.txt
```

### 4. Flag Validation
Submitting the cracked plaintext password confirmed the challenge completion:
```
120693
```

### Attack Chain
```
Identify Corporate Email (david.tofaneli@fiap.com.br)
   → Query Breach Intelligence Databases / OSINT Tools
   → Locate Leaked SHA-1 Hash (1a3be3d2236196f0c428468552885d5e09ee1469)
   → Revert SHA-1 Hash via Lookup Table / Cracking
   → Plaintext Password Recovered → FLAG: 120693
```

### Key Takeaways
- Password reuse between personal e-commerce platforms and corporate accounts exposes institutional credentials during third-party breaches.
- Unsalted SHA-1 hashes are weak and easily reversible using pre-computed lookup tables (rainbow tables).
- Multi-Factor Authentication (MFA) and Password Managers are essential mitigations against credential stuffing attacks.

---

## 🇧🇷 Português

### Desafio
> David Tofaneli, um dos colaboradores da FIAP, foi vítima de um vazamento de dados de uma plataforma de compras online, onde ele erroneamente reutilizou sua credencial da empresa para cadastrar sua conta e efetuar compras. Com os seus conhecimentos de OSINT, será que consegue descobrir a senha desta credencial? Caso consiga, ela será a sua flag ;)

### 1. Reconhecimento do Alvo
O e-mail corporativo do alvo foi identificado seguindo o padrão da instituição:
```
david.tofaneli@fiap.com.br
```

### 2. Consulta em Bases de Vazamentos
Utilizando motores de busca e inteligência de vazamentos (Breach Intelligence), o e-mail foi localizado em listas históricas de vazamentos (incluindo LinkedIn e bases de credential stuffing):
- **Hash SHA-1 Encontrado:** `1a3be3d2236196f0c428468552885d5e09ee1469`

### 3. Quebra do Hash
A string hexadecimal de 40 caracteres foi identificada como um hash SHA-1 sem salt.

Utilizando ferramentas de busca de hashes gratuitas (como CrackStation ou HashCracker):
- **Hash de Entrada:** `1a3be3d2236196f0c428468552885d5e09ee1469`
- **Algoritmo:** SHA-1
- **Resultado em Texto Claro:** `120693`

Alternativamente, via linha de comando no Kali Linux:
```bash
echo "1a3be3d2236196f0c428468552885d5e09ee1469" > hash.txt
hashcat -m 100 hash.txt /usr/share/wordlists/rockyou.txt
```

### 4. Validação da Flag
A submissão da senha em texto claro confirmou a resolução do desafio:
```
120693
```

### Cadeia de Ataque
```
Identificar E-mail Corporativo (david.tofaneli@fiap.com.br)
   → Consultar Bases de Breach Intelligence / OSINT
   → Localizar Hash SHA-1 Vazado (1a3be3d2236196f0c428468552885d5e09ee1469)
   → Reverter Hash SHA-1 via Tabela Pré-calculada / Cracking
   → Recuperar Senha em Texto Claro → FLAG: 120693
```

### Principais Aprendizados
- A reutilização de senhas entre serviços pessoais e contas corporativas expõe a infraestrutura da empresa em vazamentos de terceiros.
- Hashes SHA-1 sem salt são fracos e facilmente reversíveis utilizando tabelas pré-calculadas (rainbow tables).
- Autenticação de Múltiplos Fatores (MFA) e Gerenciadores de Senhas são controles vitais para mitigar ataques de Credential Stuffing.