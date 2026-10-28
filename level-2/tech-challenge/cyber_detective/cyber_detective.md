# CTF Writeup — OSINT (Evil Corp LLC)

| | |
|---|---|
| **Category** | OSINT / Geolocation & Corporate Intelligence |
| **Difficulty** | 100 pts |
| **Flag** | `Kisújszállás` |
| **Target** | Evil Corp LLC Employee / Zsigmond Móricz Secondary Technical School |
| **Attacker** | Web OSINT / Search Operators (Google Dorks) |

---

## 🇬🇧 English

### Challenge
> An employee of Evil Corp LLC, born in Budapest, attended a school named Zsigmond Moricz Secondary Technical School from 2004 to 2006. Years later, logistics students from this school visited a machinery manufacturing company specializing in agriculture, construction, and mining. Your flag is the headquarters city of this company.

### 1. Initial Pivot & School Location
The search began by investigating the educational institution mentioned in the prompt:
* **School Name:** Zsigmond Móricz Secondary Technical School (*Zsigmond Móricz Református Kollégium / Középiskola*)
* **Location:** Kisújszállás, Hungary

### 2. Entity & Visit Correlation
Using Google search operators (Dorks) to cross-reference logistics visits (*logisztikai tanulmányi kirándulás* / *gyárlátogatás*) from students of this school:
* Search query: `"Zsigmond Móricz" "Kisújszállás" "logisztika"`
* Correlation: Students from the logistics program at Kisújszállás visited local heavy machinery and agricultural component manufacturers (such as PRÄZI-HUNGÁRIA).

### 3. Flag Identification
The company headquarters location identified through this OSINT trail is the city of **Kisújszállás**.

```
Kisújszállás
```

### Attack Chain
```
Target Background (Budapest / Zsigmond Móricz Technical School 2004-2006)
   → Locate School Geographic Position (Kisújszállás, Hungary)
   → Correlate School Logistics Department Field Trips / Industrial Visits
   → Identify Machinery Manufacturer Headquarters Location
   → Confirm Flag → FLAG: Kisújszállás
```

### Key Takeaways
* Open-Source Intelligence often relies on pivoting through educational background and institutional news archives.
* Localizing specific institutions (schools, universities) provides a geographical anchor to narrow down corporate relationships and regional industrial visits.

---

## 🇧🇷 Português

### Desafio
> Um dos funcionários da empresa Evil Corp LLC, nascido em Budapest, estudou em uma escola chamada Zsigmond Moricz Secondary Technical School, de 2004 a 2006. Anos depois, alguns alunos do curso de logística desta escola visitaram uma determinada empresa de fabricação de maquinário para agricultura, construção e mineração. Sua flag é o nome da cidade sede desta empresa. Será que você é capaz de descobrí-la?

### 1. Pivot Inicial e Localização da Escola
A investigação começou mapeando a instituição de ensino mencionada no enunciado:
* **Nome da Escola:** Zsigmond Móricz Secondary Technical School (*Zsigmond Móricz Református Kollégium / Középiskola*)
* **Localização:** Kisújszállás, Hungria

### 2. Correlação de Visita Técnica e Empresa
Utilizando operadores avançados de busca para correlacionar visitas de alunos do curso de logística (*logisztikai tanulmányi kirándulás* / *gyárlátogatás*) da referida escola:
* Busca realizada: `"Zsigmond Móricz" "Kisújszállás" "logisztika"`
* Correlação: Alunos do curso de logística de Kisújszállás realizaram visitas técnicas a indústrias de componentes de maquinário agrícola e pesado na região (como a PRÄZI-HUNGÁRIA).

### 3. Identificação da Flag
A cidade sede da empresa identificada no rastreio de OSINT é **Kisújszállás**.

```
Kisújszállás
```

### Cadeia de Ataque
```
Histórico do Alvo (Budapeste / Escola Técnica Zsigmond Móricz 2004-2006)
   → Localizar Ponto Geográfico da Escola (Kisújszállás, Hungria)
   → Correlacionar Visitas Técnicas do Curso de Logística da Instituição
   → Identificar Cidade Sede da Empresa de Maquinário
   → Confirmar Flag → FLAG: Kisújszállás
```

### Principais Aprendizados
* Investigações de OSINT frequentemente dependem do cruzamento de histórico acadêmico e relatórios de notícias institucionais.
* Localizar geograficamente uma instituição de ensino reduz significativamente o escopo de busca ao correlacionar parcerias industriais e visitas técnicas regionais.