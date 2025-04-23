# 🎥 Banco de Dados do Oscar 2025 🏆

Bem-vindo ao **Banco de Dados do Oscar 2025**, um projeto apaixonante que reúne a história completa das indicações e vitórias do Oscar, desde sua primeira edição em 1928 até os dias atuais! 🌟 Este repositório é o seu passe de entrada para explorar curiosidades incríveis sobre filmes, atores, diretores e as maiores conquistas do cinema. Preparado para mergulhar no glamour de Hollywood? 🎬

---

## 🌟 Visão Geral

Este banco de dados, construído com **MongoDB**, contém **11.015 registros** de indicações ao Oscar, cobrindo categorias, filmes, anos e indicados. Com ele, você pode responder perguntas como:  
- Quantas vezes Natalie Portman foi indicada?  
- Quais filmes levaram Melhor Filme *e* Melhor Diretor no mesmo ano?  
- Quem ganhou o primeiro Oscar de Melhor Atriz?  

Navegue pela história do cinema com consultas prontas e descubra fatos fascinantes! 🚀 Todas as consultas estão formatadas em blocos de código para que você possa copiá-las diretamente.

---

## 📊 Destaques do Banco de Dados

Aqui estão 20 perguntas incríveis que você pode explorar, com respostas e consultas MongoDB prontas para copiar e executar:

### 1. Quantos registros estão no banco de dados?  
**Resposta**: 11.015 indicações.  
**Consulta**:  
```javascript
db.Registros.count()
```

### 2. Quantas indicações existem por categoria?  
**Resposta**: Algumas categorias em destaque:  
- 🎬 **Direção (DIRECTING)**: 474 indicações  
- 🌍 **Filme Estrangeiro (FOREIGN LANGUAGE FILM)**: 315 indicações  
- 🎵 **Música (Song)**: 215 indicações  
- 🔊 **Gravação de Som (SOUND RECORDING)**: 195 indicações  
- ✍️ **Roteiro Original (WRITING - Original Screenplay)**: 165 indicações  
... e muito mais!  

**Consulta**:  
```javascript
db.Registros.aggregate([
  {$group: {_id: "$categoria", count: {$sum: 1}}}
])
```

### 3. Quantas vezes Natalie Portman foi indicada ao Oscar?  
**Resposta**: 3 vezes.  
**Consulta**:  
```javascript
db.Registros.find({nome_do_indicado: "Natalie Portman"}).count()
```

### 4. Quantos Oscars Natalie Portman ganhou?  
**Resposta**: 1 Oscar.  
**Consulta**:  
```javascript
db.Registros.find({"nome_do_indicado": "Natalie Portman", "vencedor": "true"}).count()
```

### 5. Quantas vezes Viola Davis foi indicada ao Oscar?  
**Resposta**: 4 vezes.  
**Consulta**:  
```javascript
db.Registros.find({"nome_do_indicado": "Viola Davis"}).count()
```

### 6. Quantos Oscars Viola Davis ganhou?  
**Resposta**: 1 Oscar.  
**Consulta**:  
```javascript
db.Registros.find({"nome_do_indicado": "Viola Davis", "vencedor": "true"}).count()
```

### 7. Amy Adams já ganhou algum Oscar?  
**Resposta**: Não, ela nunca venceu.  
**Consulta**:  
```javascript
db.Registros.find({"nome_do_indicado": "Amy Adams", "vencedor": "true"}).count()
```

### 8. Quais atores ou atrizes foram indicados mais de uma vez?  
**Resposta**: Alguns destaques:  
-  **Randy Newman**: 13 indicações  
-  **Judi Dench**: 8 indicações  
-  **Dorothy Jeakins**: 6 indicações  
-  **Julianne Moore**: 5 indicações  
-  **Viola Davis**: 4 indicações  
... e muitos outros!  

**Consulta**:  
```javascript
db.Registros.aggregate([
  {$group: {_id: "$nome_do_indicado", contador: {$sum: 1}}},
  {$match: {contador: {$gt: 1}}}
])
```

### 9. Em quais anos a série *Toy Story* ganhou Oscars?  
**Resposta**: 2011 e 2020.  
**Consulta**:  
```javascript
db.Registros.find({nome_do_filme: /Toy Story/, vencedor: "true"})
```

### 10. A partir de que ano a categoria "Actress" deixou de existir?  
**Resposta**: Após 1928.  
**Consulta**:  
```javascript
db.Registros.findOne({categoria: "ACTRESS"})
```

### 11. Quem ganhou o primeiro Oscar de Melhor Atriz? Em que ano?  
**Resposta**: Janet Gaynor, em 1928.  
**Consulta**:  
```javascript
db.Registros.findOne({categoria: "ACTRESS"})
```

### 12. Como alterar os valores do campo "Vencedor" de "true" para 1 e "false" para 0?  
**Resposta**: Executado com sucesso.  
**Consulta**:  
```javascript
db.Registros.updateMany({vencedor: "false"}, {$set: {vencedor: 0}})
db.Registros.updateMany({vencedor: "true"}, {$set: {vencedor: 1}})
```

### 13. Em qual edição do Oscar o filme *Crash* concorreu?  
**Resposta**: 2006.  
**Consulta**:  
```javascript
db.Registros.find({"nome_do_filme": "Crash"}, {ano_cerimonia: 1})
```

### 14. O filme *Central do Brasil* aparece no banco de dados do Oscar?  
**Resposta**: Sim.  
**Consulta**:  
```javascript
db.Registros.find({"nome_do_filme": "Central Station"})
```

### 15. Quais filmes que nunca foram indicados ao Oscar foram adicionados ao banco?  
**Resposta**: Três filmes brasileiros foram incluídos:  
-  **Inspetor Faustão e Malandro: A Missão (Primeira e Única)** (1991)  
  *Categoria sugerida*: Ator Principal (Fausto Corrêa)  
-  **Ó Pai, Ó** (2007)  
  *Categoria sugerida*: Filme Internacional  
-  **Os Sete Gatinhos** (1980)  
  *Categoria sugerida*: Melhor Filme  

**Consulta de inserção**:  
```javascript
db.Registros.insertMany([
  {
    id_registro: 20000,
    ano_filmagem: 1991,
    ano_cerimonia: 1992,
    cerimonia: 64,
    categoria: "ACTOR IN A LEADING ROLE",
    nome_do_indicado: "Fausto Corrêa",
    nome_do_filme: "Inspector Faustão and Mallandro: The Mission (First and Only)",
    vencedor: "false"
  },
  {
    id_registro: 20001,
    ano_filmagem: 2007,
    ano_cerimonia: 2008,
    cerimonia: 80,
    categoria: "INTERNATIONAL FEATURE FILM",
    nome_do_indicado: "Brazil",
    nome_do_filme: "O Dad, O",
    vencedor: "false"
  },
  {
    id_registro: 20002,
    ano_filmagem: 1980,
    ano_cerimonia: 1981,
    cerimonia: 53,
    categoria: "BEST PICTURE",
    nome_do_indicado: "Neville d'Almeida and Gilberto Loureiro",
    nome_do_filme: "The Seven Kittens",
    vencedor: "false"
  }
])
```

### 16. Denzel Washington já ganhou algum Oscar?  
**Resposta**: Sim, 2 Oscars.  
**Consulta**:  
```javascript
db.Registros.find({"nome_do_indicado": "Denzel Washington", "vencedor": "true"}).count()
```

### 17. Quais filmes ganharam o Oscar de Melhor Filme?  
**Resposta**: Alguns exemplos:  
-  *Lawrence of Arabia*  
-  *Tom Jones*  
-  *My Fair Lady*  
... e muitos outros!  

**Consulta**:  
```javascript
db.Registros.find({"categoria": "BEST PICTURE", "vencedor": "true"}, {_id: 0, nome_do_filme: 1})
```

### 18. Em que anos Sidney Poitier, o primeiro ator negro indicado ao Oscar, foi indicado? Por quais filmes?  
**Resposta**: Indicado em 1958 (*The Defiant Ones*) e 1963 (*Lilies of the Field*).  
**Consulta**:  
```javascript
db.Registros.find({"nome_do_indicado": "Sidney Poitier"}, {_id: 0})
```

### 19. Quais filmes ganharam os Oscars de Melhor Filme e Melhor Diretor na mesma cerimônia?  
**Resposta**: Exemplos incluem:  
-  *My Fair Lady* (1965)  
-  *Amadeus* (1985)  
-  *Slumdog Millionaire* (2009)  
... e outros 46 filmes!  

**Consulta**:  
```javascript
db.Registros.aggregate([
  {"$match": {"vencedor": "true", "categoria": {"$in": ["BEST PICTURE", "DIRECTING"]}}},
  {"$group": {
    "_id": {"ano_cerimonia": "$ano_cerimonia", "nome_do_filme": "$nome_do_filme"},
    "categoria": {$push: "$categoria"},
    contador: {$sum: 1}
  }},
  {$match: {contador: {$gt: 1}}}
])
```

### 20. Denzel Washington e Jamie Foxx já concorreram ao Oscar no mesmo ano?  
**Resposta**: Não.  
**Consulta**:  
```javascript
db.Registros.aggregate([
  {"$match": {"nome_do_indicado": {"$in": ["Denzel Washington", "Jamie Foxx"]}}},
  {"$group": {
    "_id": {"ano_cerimonia": "$ano_cerimonia"},
    "nome_do_indicado": {$push: "$nome_do_indicado"},
    contador: {$sum: 1}
  }}
])
```

---

## 🛠️ Como Usar

### Pré-requisitos  
1. **Instale o MongoDB**: Certifique-se de ter o MongoDB instalado. [Instruções oficiais aqui](https://www.mongodb.com/docs/manual/installation/).  
2. **Importe o banco de dados**: Faça o download do arquivo de dados fornecido neste repositório e importe-o para o MongoDB.
