# Banco-de-Dados-do-Oscar-2025
Qual o total de registros na tabela indicados?
R: 11015

Q:db.Registros.count()

Qual o número de indicações por categoria agrupadas por categoria?
R:
'MUSIC (Original Song Score and Its Adaptation -or- Adaptation Score)',
 count: 6
 
 'WRITING (Screenplay Written Directly for the Screen)',
  count: 120
 
 'HONORARY AWARD',
  count: 135
  
  'CINEMATOGRAPHY (Color)',
  count: 135
  
  'SPECIAL ACHIEVEMENT AWARD (Sound Editing)',
  count: 1
  
  'DIRECTING',
  count: 474
  
  'WRITING (Original Screenplay)',
  count: 165
  
  'WRITING (Adaptation)',
  count: 17
  
  'MUSIC (Song)',
  count: 215
  
  'SHORT SUBJECT (Comedy)',
  count: 13
  
  'DIRECTING (Dramatic Picture)',
  count: 3
  
  'WRITING (Screenplay)',
  count: 104
  
  'WRITING (Adapted Screenplay)',
  count: 115
  
  'WRITING (Screenplay Adapted from Other Material)',
  count: 10
  
  'DOCUMENTARY FEATURE FILM',
  count: 15
  
  'AWARD OF COMMENDATION',
  count: 1
  
  'WRITING (Story and Screenplay--written directly for the screen)',
  count: 60
  
  'SOUND RECORDING',
  count: 195
  
  'MUSIC (Original Score--for a motion picture [not a musical])',
  count: 10
  
  'FOREIGN LANGUAGE FILM',
  count: 315
  e mais

Q: db.Registros.aggregate([{$group:{_id: "$categoria",count:{$sum:1}}}])
Quantas vezes Natalie Portman foi indicada ao Oscar?
R: 3 vezes

Q:  db.Registros.find({nome_do_indicado : "Natalie Portman"}).count()

Quantos Oscars Natalie Portman ganhou?
R: 1 vez

Q:db.Registros.find({"nome_do_indicado":"Natalie Portman","vencedor":"true"}).count()


Quantas vezes Viola Davis foi indicada ao Oscar?
R: 4 vezes

Q:db.Registros.find({"nome_do_indicado":"Viola Davis"}).count()


Quantos Oscars Viola Davis ganhou?
R: 1 vez

Q:db.Registros.find({"nome_do_indicado":"Viola Davis","vencedor":"true"}).count()


Amy Adams já ganhou algum Oscar?
R: Não

Q:db.Registros.find({"nome_do_indicado":"Amy Adams"}).count()

Quais os atores/atrizes que foram indicados mais de uma vez?
R:
'Music and Lyric by Randy Newman',
contador: 13
  
'Judi Dench',
contador: 8

'Dorothy Jeakins',
contador: 6

'Julianne Moore',
contador: 5

'Viola Davis',
contador: 4

'Consolata Boyle',
contador: 3
  
'Peter Lord',
contador: 3

'Sam Wood',
contador: 3

'Catherine Martin',
contador: 3
  
'Sam Rockwell',
contador: 2

'Metro-Goldwyn-Mayer Studio Music Department, Nat W. Finston, head of department  (Score by Herbert Stothart)',
contador: 2
  
'Louis Brock, Producer',
contador: 2

'Lee J. Cobb',
contador: 2

'John Healy, Producer',
contador: 2

'Gordon Willis',
contador: 2

'Theodore Soderberg, Herman Lewis',
contador: 2

'Scarlett Johansson',
contador: 2

'William Ziegler',
 contador: 3
e mais
  
Q:db.Registros.aggregate({$group:{_id :"$nome_do_indicado", contador:{$sum:1}}},{$match:{contador:{$gt:1}}}

A série de filmes Toy Story ganhou Oscars em quais anos?
R: 2011 e 2020

Q: db.Registros.find({nome_do_filme:/Toy Story/,vencedor:"true"})

A partir de que ano que a categoria "Actress" deixa de existir?
R: 1928

Q:db.Registros.findOne({categoria:"ACTRESS"})

Quem ganhou o primeiro Oscar para Melhor Atriz? Em que ano?
R: Janet Gaynor, 1928

Q:db.Registros.findOne({categoria:"ACTRESS"})

Na campo "Vencedor", altere todos os valores com "true" para 1 e todos os valores "false" para 0.
R: Prontinhp

Q: db.Registros.updateMany({vencedor:"false"},{$set: {vencedor: 0}}), db.Registros.updateMany({vencedor:"true"},{$set: {vencedor: 1}})

Em qual edição do Oscar "Crash" concorreu ao Oscar?
R: 2006

Q:db.Registros.find({"nome_do_filme":"Crash"},{ano_cerimonia:1})

O filme Central do Brasil aparece no Oscar?
R: Sim

Q:db.Registros.find({"nome_do_filme":"Central Station"})

Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser.
R: Inspetor Faustão e Malandro: A  missão (primeira e única), Ó Pai, Ó e Os Sete Gatinhos

Q:
db.Registros.insertMany([{
id_registro: 20000,
  ano_filmagem: 1991,
  ano_cerimonia: 1992,
  cerimonia: 64,
  categoria: "ACTOR IN A LEADING ROLE",
  nome_do_indicado: "Fausto Corrêa",
  nome_do_filme: "Inspector Faustão and Mallandro: The Mission (First and Only)",
  vencedor: "false"
},{
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
  nome_do_indicado: "Neville d'Almeida and  Gilberto Loureiro",
  nome_do_filme: "The Seven Kittens",
  vencedor: "false"
}])
Denzel Washington já ganhou algum Oscar?
R: Sim, 2 vezes

Q:db.Registros.find({"nome_do_indicado":"Denzel Washington","vencedor":"true"})


Quais os filmes que ganharam o Oscar de Melhor Filme?
R:
 nome_do_filme: 'Lawrence of Arabia'
 
 nome_do_filme: 'Tom Jones'

 nome_do_filme: 'My Fair Lady'

e mais

Q:db.Registros.find({"categoria":"BEST PICTURE","vencedor":"true"},{_id:0,nome_do_filme:1})

Sidney Poitier foi o primeiro ator negro a ser indicado ao Oscar. Em que ano ele foi indicado? Por qual filme?
R: The Defiant Ones e Lilies of the Field, 1958 e 1963

Q:db.Registros.find({"nome_do_indicado":"Sidney Poitier"},{_id:0})

Quais os filmes que ganharam o Oscar de Melhor Filme e Melhor Diretor na mesma cerimonia?
R:
 _id: {
    ano_cerimonia: 1965,
    nome_do_filme: 'My Fair Lady'
  },
  categoria: [
    'DIRECTING',
    'BEST PICTURE'
  ],
  contador: 2
,

  _id: {
    ano_cerimonia: 1985,
    nome_do_filme: 'Amadeus'
  },
  categoria: [
    'DIRECTING',
    'BEST PICTURE'
  ],
  contador: 2
  ,
  _id: {
    ano_cerimonia: 2009,
    nome_do_filme: 'Slumdog Millionaire'
  },
  categoria: [
    'DIRECTING',
    'BEST PICTURE'
  ],
  contador: 2
  
  e mais 46 filmes
  


Q:db.Registros.aggregate([{"$match":{"vencedor":"true", "categoria": {"$in":["BEST PICTURE","DIRECTING"]}}},{
    "$group": {
      "_id": {
        "ano_cerimonia": "$ano_cerimonia",
        "nome_do_filme": "$nome_do_filme"
      },
      "categoria":{$push: "$categoria"}, contador : {$sum:1}
    }
  },{$match: {contador:{$gt:1}}}])

Denzel Washington e Jamie Foxx já concorreram ao Oscar no mesmo ano?
R: Não

Q:db.Registros.aggregate([{"$match":{ "nome_do_indicado": {"$in":["Denzel Washington", "Jamie Foxx"]}}},{
    "$group": {
      "_id": {
        "ano_cerimonia": "$ano_cerimonia"
      },
      "nome_do_indicado":{$push: "$nome_do_indicado"}, contador : {$sum:1}
    }
  }])o
