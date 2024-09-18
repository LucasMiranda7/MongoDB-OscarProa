# Atividades para trabalhar com o Oscar

1- Quantas vezes Natalie Portman foi indicada ao Oscar? <br>
Foi indicada 3x.
```
> db.oscar.countDocuments({entity: /Natalie Portman/})
< 3
```

2- Quantos Oscars Natalie Portman ganhou? <br>
Ganhou 1 oscar.
```
> db.oscar.countDocuments({entity: /Natalie Portman/, winner: true})
< 1
```

3- Amy Adams já ganhou algum Oscar? <br>
Não ganhou oscar.
```
> db.oscar.countDocuments({entity: /Amy Adams/, winner: true})
< 0
```

4- A série de filmes Toy Story ganhou um Oscar em quais anos? <br>
Ganhou Oscar entre 1995 a 2010.
```
> db.oscar.find({entity: /Toy Story/, winner: true})
< {
  _id: ObjectId('66ea151c7099b8c447d22409'),
  category: 'SPECIAL ACHIEVEMENT AWARD',
  entity: 'To John Lasseter, for his inspired leadership of the Pixar Toy Story team, resulting in the first feature-length computer-animated film.',
  winner: true,
  year: 1995
}
{
  _id: ObjectId('66ea151c7099b8c447d22b62'),
  category: 'ANIMATED FEATURE FILM',
  entity: 'Toy Story 3',
  winner: true,
  year: 2010
}
{
  _id: ObjectId('66ea151c7099b8c447d22b96'),
  category: 'MUSIC (Original Song)',
  entity: 'Toy Story 3',
  winner: true,
  year: 2010
}
```

5- A partir de que ano que a categoria "Actress" deixa de existir? <br>
A partir do ano 1976.

```
db.oscar.find(
  { "category": "ACTRESS" }
).sort({ year: -1 }).limit(1)
{
  _id: ObjectId('66ea151c7099b8c447d21a36'),
  category: 'ACTRESS',
  entity: 'Isabelle Adjani',
  winner: false,
  year: 1975
}


db.oscar.find({"year": 1976}).sort({year: 1}).limit(1)
{
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
db.oscar.find({winner: true, category: "ACTRESS"}, {year: 1, entity: 1, _id: 0}).sort({year: 1}).limit(1)
{
  entity: 'Janet Gaynor',
  year: 1927
}
```

7- Na campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0. <br>

```
db.oscar.updateMany({winner: false}, {$set: {winner: 0}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 7841,
  modifiedCount: 7841,
  upsertedCount: 0
}

db.oscar.updateMany({winner: true}, {$set: {winner: 1}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 3217,
  modifiedCount: 3217,
  upsertedCount: 0
}
```

8- Em qual edição do Oscar "Crash" concorreu ao Oscar? <br>
A 78.ª edição do Oscar

```
db.oscar.find({entity: "Crash", winner: 1}).sort({year: -1})
{
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
