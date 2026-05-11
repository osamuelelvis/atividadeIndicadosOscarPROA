## Nível 1: Primeiros Passos
Conhecendo a Base de Dados

1.1 Quantos registros existem na coleção de indicados ao Oscar?<br>
R: 10889 registros

```json
db.Indicados.countDocuments();
```

1.2 Quais são as diferentes categorias de premiação que existem no banco de dados? Liste todas as categorias únicas.<br>
R: 115 registros

```json
db.oscar_indicados.distinct("categoria");
```

1.3 Qual foi o primeiro ano de cerimônia do Oscar registrado na base?<br>

R: O primeiro ano registrado na base é de 1928

```json
{ id_registro: 1}
```

1.4 Qual foi o último ano de cerimônia registrado na base? <br>
R: O último ano de cerimônia registrado na base é o de 2024

```json
{ id_registro: 10889}
```

1.5 Quantas cerimônias do Oscar estão registradas no total?
R: Há 96 cerimônias registradas no total

```json
db.Indicados.distinct("cerimonia")
```

1.6 Atualize os registros da coleção com os dados do Oscar 2025 e 2026 (pesquise os vencedores e adicione-os).<br>
R: Está adicionado conforme o arquivo .json no repositório

## Nível 2: Explorando Categorias

**2.1** Quantas indicações existem para cada categoria? Agrupe por categoria e ordene da mais frequente para a menos frequente.<br>
```json
db.Indicados.aggregate([
  {
    $group: {
      _id: "$categoria",
      total_indicacoes: { $sum: 1 }
    }
  },
  {
    $sort: { total_indicacoes: -1 }
  }
])
```

**2.2** Qual categoria teve mais indicações ao longo da história do Oscar?<br>
R: A categoria "DIRECTING", tendo 469 indicações no total.

```json
db.Indicados.aggregate([
  {
    $group: {
      _id: "$categoria",
      total_indicacoes: { $sum: 1 }
    }
  },
  {
    $sort: { total_indicacoes: -1 }
  }
])
```

**2.3** Qual categoria teve menos indicações ao longo da história?<br>
R: Ao longo da história, as categorias **SPECIAL ACHIEVEMENT AWARD (Sound Effects)**, **Best Animated Feature Film**, **AWARD OF COMMENDATION**, **Best International Feature Film**, **SPECIAL ACHIEVEMENT AWARD (Sound Editing)** e **GORDON E. SAWYER AWARD** obtiveram apenas uma indicações em toda sua história.

```json
db.Indicados.aggregate([
  {
    $group: {
      _id: "$categoria",
      total_indicacoes: { $sum: 1 }
    }
  },
  {
    $sort: { total_indicacoes: +1 }
  }
])
```

**2.4** A partir de que ano a categoria "ACTRESS" deixou de existir? (Dica: procure a última cerimônia com essa categoria)<br>
R: A partir do ano de 1976, onde dali em diante, essa categoria deixou de existir.

```json
db.Indicados.find({	
  ano_cerimonia: 1976,
  categoria: "ACTRESS"
})
```

**2.5** Quais categorias existiam na primeira cerimônia (1928) e não existem mais hoje?<br>
R: Categorias como **ENGINEERING EFFECTS**, **UNIQUE AND ARTISTIC PICTURES** e **SPECIAL AWARD** já não existem mais nos dias de hoje.

```json
[
  'ACTOR',
  'ACTRESS',
  'ART DIRECTION',
  'CINEMATOGRAPHY',
  'DIRECTING (Comedy Picture)',
  'DIRECTING (Dramatic Picture)',
  'ENGINEERING EFFECTS',
  'OUTSTANDING PICTURE',
  'SPECIAL AWARD',
  'UNIQUE AND ARTISTIC PICTURE',
  'WRITING (Adaptation)',
  'WRITING (Original Story)',
  'WRITING (Title Writing)'
],
[
  'Best Actor in a Leading Role',
  'Best Actor in a Supporting Role',
  'Best Actress in a Leading Role',
  'Best Actress in a Supporting Role',
  'Best Director',
  'Best Picture'
]
```

**2.6** Liste todas as categorias que contêm a palavra "DIRECTING" no nome.<br>
R: Além da categoria **DIRECTING**, outras categorias são elas: **DIRECTING (Comedy Picture)**, **DIRECTING (Dramatic Picture)**

```json
db.Indicados.find({
  categoria: { $regex: "DIRECTING" }
})
```

## Nível 3: Atores e Atrizes Famosos
### Natalie Portman

**3.1** Quantas vezes Natalie Portman foi indicada ao Oscar?<br>
R: Ela foi indicada três vezes conforme mostra o registro na base de dados
```json
{ nome_do_indicado: { $regex: "Natalie Portman" }}
```

**3.2** Quantos Oscars Natalie Portman ganhou?<br>
R: Ela ganhou a estatueta uma vez
```json
{ nome_do_indicado: { $regex: "Natalie Portman" }, vencedor: 1}
```

**3.3** Em quais anos e por quais filmes Natalie Portman foi indicada? <br>
R: Nos ano de **2005**, **2011** e **2017**, pelos filme **Closer**, **Black Swan** e **Jackie**, respectivamente
```json
{nome_do_indicado: { $regex: "Natalie Portman" }}
```

**3.4** Liste todas as indicações de Natalie Portman mostrando: ano, categoria, filme e se venceu.<br>
R: R: As indicações de Natalie Portman ao Oscar ocorreram conforme listado abaixo:

- 2005 — Filme: Closer — Categoria: Melhor Atriz Coadjuvante — Vencedor: Não
- 2011 — Filme: Black Swan — Categoria: Melhor Atriz — Vencedor: Sim
- 2017 — Filme: Jackie — Categoria: Melhor Atriz — Vencedor: Não

```json
{nome_do_indicado: { $regex: "Natalie Portman" }}
```
---
### Viola Davis

**3.5** Quantas vezes Viola Davis foi indicada ao Oscar?<br>
R: Ela foi indicada quatro vezes de acordo com os registros
```json
{nome_do_indicado: { $regex: "Viola Davis" }}
```

**3.6** Quantos Oscars Viola Davis ganhou?<br>
R: Ela ganhou a estatueta apenas uma vez
```json
{nome_do_indicado: { $regex: "Viola Davis" }, vencedor: 1}
```

**3.7** Por quais filmes Viola Davis foi indicada?<br>
R: Ela foi indicada pelos filmes: **Doubt (2009)**, **The Help (2012)**, **Fences (2017)** e **Ma Rainey's Black Bottom (2021)**
```json
{nome_do_indicado: { $regex: "Viola Davis" }}
```

---
### Amy Adams

**3.8** Amy Adams já ganhou algum Oscar?<br>
R: Infelizmente, não
```json
{nome_do_indicado: { $regex: "Amy Adams" }, vencedor: 1}
```

**3.9** Quantas vezes Amy Adams foi indicada sem ganhar?<br>
R: Ela foi indicada 6 vezes, sem ganhar
```json
{nome_do_indicado: { $regex: "Amy Adams" }}
```

---
### Denzel Washington

**3.10** Denzel Washington já ganhou algum Oscar?<br>
R: Sim, duas vezes
```json
{nome_do_indicado: { $regex: "Denzel Washington"}, vencedor: 1}
```

**3.11** Quantas vezes Denzel Washington foi indicado ao Oscar?<br>
R: Ele foi indicada 11 vezes ao Oscar
```json
{nome_do_indicado: { $regex: "Denzel Washington"}}
```

**3.12** Liste todos os Oscars que Denzel Washington ganhou (ano, categoria, filme).<br>
R: 
- Ano: 1990; Categoria: ACTOR IN A SUPPORTING ROLE; Filme: Glory
- Ano: 2002; Categoria: ACTOR IN A LEADING ROLE; Filme: Training Day

```json
{nome_do_indicado: { $regex: "Denzel Washington"}, vencedor: 1}
```

---
## Nível 6: Análise de Filmes
### Toy Story

6.1 A série de filmes Toy Story ganhou Oscars em quais anos?<br>
R: Nos anos de 2011 e em 2020
```json
{ nome_do_filme: { $regex: "^Toy Story" }, vencedor: 1}
```

6.2 Quantas indicações a franquia Toy Story recebeu no total?<br>
R: A franquia recebeu 11 indicações no total
```json
{ nome_do_filme: { $regex: "^Toy Story" }}
```

6.3 Em quais categorias os filmes Toy Story foram indicados?<br>
R: Nas categorias: **MUSIC (Original Musical or Comedy Score)**, **MUSIC (Original Song)**, **WRITING (Screenplay Written Directly for the Screen)**, **ANIMATED FEATURE FILM**, **MUSIC (Original Song)**, **BEST PICTURE**, **SOUND EDITING** e **WRITING (Adapted Screenplay)**.
```json
{ nome_do_filme: { $regex: "^Toy Story" }}
```
---
### Crash

6.4 Em qual edição do Oscar o filme "Crash" concorreu?<br>
R: Ele concorreu na edição de número 78 do Oscar
```json
{ nome_do_filme: { $regex: "^Crash"}}
```

6.5 Quantas indicações o filme "Crash" recebeu?<br>
R: O filme recebeu 6 indicações no total, conforme os registros retornados pela consulta
```json
{ nome_do_filme: { $regex: "^Crash"}}
```

6.6 "Crash" ganhou o Oscar de Melhor Filme?<br>
R: Sim, ganhou nas categorias de: **FILM EDITING**, **BEST PICTURE** e **WRITING (Original Screenplay)**
```json
{ nome_do_filme: { $regex: "^Crash"}}
```

---
### Central do Brasil

6.7 O filme "Central do Brasil" aparece no banco de dados?<br>
R: Sim, aparece, mas com outro nome
```json
{ nome_do_filme: { $regex: "^Central Station" }}
```

6.8 Se sim, quantas indicações "Central do Brasil" recebeu?<br>
R: Ele recebeu duas indicações, conforme os registros retornados pela consulta
```json
{ nome_do_filme: { $regex: "^Central Station" }}
```
