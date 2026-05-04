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