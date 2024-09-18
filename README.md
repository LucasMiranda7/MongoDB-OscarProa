# Atividades para trabalhar com o Oscar

1- Quantas vezes Natalie Portman foi indicada ao Oscar? <br>
Foi indicada 3x.
```
> db.oscar.countDocuments({nome_do_indicado: /Natalie Portman/})
< 3
```

2- Quantos Oscars Natalie Portman ganhou? <br>
Ganhou 1 oscar.
```
> db.oscar.countDocuments({nome_do_indicado: /Natalie Portman/, vencedor: "true"})
< 1
```

3- Amy Adams já ganhou algum Oscar? <br>
Não ganhou oscar.
```
> db.oscar.countDocuments({nome_do_indicado: /Amy Adams/, vencedor: "true"})
< 0
```

4- A série de filmes Toy Story ganhou um Oscar em quais anos? <br>
Ganhou Oscar entre 1995 a 2010.
```
> db.oscar.find({nome_do_filme: /Toy Story/, vencedor: "true"})
< {
  _id: ObjectId('66ead38c6c024a36e96bfa15'),
  id_registro: 9165,
  ano_filmagem: 2010,
  ano_cerimonia: 2011,
  cerimonia: 83,
  categoria: 'ANIMATED FEATURE FILM',
  nome_do_indicado: 'Lee Unkrich',
  nome_do_filme: 'Toy Story 3',
  vencedor: 'true'
}
{
  _id: ObjectId('66ead38c6c024a36e96bfa49'),
  id_registro: 9217,
  ano_filmagem: 2010,
  ano_cerimonia: 2011,
  cerimonia: 83,
  categoria: 'MUSIC (Original Song)',
  nome_do_indicado: 'Music and Lyric by Randy Newman',
  nome_do_filme: 'Toy Story 3',
  vencedor: 'true'
}
{
  _id: ObjectId('66ead38c6c024a36e96bfe7c'),
  id_registro: 10292,
  ano_filmagem: 2019,
  ano_cerimonia: 2020,
  cerimonia: 92,
  categoria: 'ANIMATED FEATURE FILM',
  nome_do_indicado: 'Josh Cooley, Mark Nielsen and Jonas Rivera',
  nome_do_filme: 'Toy Story 4',
  vencedor: 'true'
}
```

5- A partir de que ano que a categoria "Actress" deixa de existir? <br>
A partir do ano 1976.

```
> db.oscar.find(
< { "category": "ACTRESS" }
).sort({ year: -1 }).limit(1)
{
  _id: ObjectId('66ea151c7099b8c447d21a36'),
  category: 'ACTRESS',
  entity: 'Isabelle Adjani',
  winner: false,
  year: 1975
}


> db.oscar.find({"year": 1976}).sort({year: 1}).limit(1)
< {
  _id: ObjectId('66ea151c7099b8c447d21aa0'),
  category: 'ACTOR IN A LEADING ROLE',
  entity: 'Robert De Niro',
  winner: false,
  year: 1976
}

```


6- O primeiro Oscar para melhor Atriz foi para quem? Em que ano? <br>
Foi para Janet Gaynor. Ano de 1927
```
> db.oscar.find({vencedor:"true", categoria: "ACTRESS"}, {ano_filmagem: 1, nome_do_indicado: 1, _id: 0}).sort({ano_filmagem: 1}).limit(1)
< {
  ano_filmagem: 1927,
  nome_do_indicado: 'Janet Gaynor'
}
}
```

7- Na campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0. <br>

```
> db.oscar.updateMany({vencedor: "true"}, {$set: {vencedor: 1}})
< {
  acknowledged: true,
  insertedId: null,
  matchedCount: 2464,
  modifiedCount: 2464,
  upsertedCount: 0
}

> db.oscar.updateMany({vencedor: "false"}, {$set: {vencedor: 0}})
< {
  acknowledged: true,
  insertedId: null,
  matchedCount: 8423,
  modifiedCount: 8423,
  upsertedCount: 0
}
```

8- Em qual edição do Oscar "Crash" concorreu ao Oscar? <br>
A 78.ª edição do Oscar

```
> db.oscar.find({entity: "Crash", winner: 1}).sort({year: -1})
< {
  _id: ObjectId('66ea151c7099b8c447d228fe'),
  category: 'FILM EDITING',
  entity: 'Crash',
  winner: 1,
  year: 2005
}

 {
  _id: ObjectId('66ea151c7099b8c447d22913'),
  category: 'BEST PICTURE',
  entity: 'Crash',
  winner: 1,
  year: 2005
}
 {
  _id: ObjectId('66ea151c7099b8c447d22930'),
  category: 'WRITING (Original Screenplay)',
  entity: 'Crash',
  winner: 1,
  year: 2005
}
```

9- Bom... dê um Oscar para um filme que merece muito, mas não ganhou.

10- O filme Central do Brasil aparece no Oscar?

11- Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser. 

14 - Pensando no ano em que você nasceu: Qual foi o Oscar de melhor filme, Melhor Atriz e Melhor Diretor?
