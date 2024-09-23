# E o Oscar vai para...?

Exercícios usando MongoDB, com base no banco de dados passado pelo Professor.

## Quantas vezes Natalie Portman foi indicada ao Oscar?

R: Foi indicada 3 vezes.

db.registros.countDocuments({nome_do_indicado: "Natalie Portman"})

## Quantos Oscars Natalie Portman ganhou?

R: Ganhou 1 vez.

db.registros.countDocuments({nome_do_indicado: "Natalie Portman", vencedor: "true"})

## Amy Adams já ganhou algum Oscar?

R: Não.

db.registros.countDocuments({nome_do_indicado: "Amy Adams", vencedor: "true"})

## A série de filmes Toy Story ganhou um Oscar em quais anos?

R: 2 vezes em 2011 e 1 vez em 2020.

db.registros.find({nome_do_filme: /Toy Story/,vencedor: "true"})

## A partir de que ano que a categoria "Actress" deixa de existir? 

R: Ano de 1976.

db.registros.find({categoria: "ACTRESS"}, {ano_cerimonia: 1, _id: 0}).sort({ano_cerimonia: -1}).limit(1)

## O primeiro Oscar para melhor Atriz foi para quem? Em que ano?

R: Janet Gaynor em 1928.

db.registros.find({categoria: "ACTRESS", vencedor: "true"}, {nome_do_indicado: 1, ano_cerimonia: 1}).limit(1)

## No campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0.

db.registros.updateMany({vencedor: "true"}, {$set: {vencedor: 1} })

db.registros.updateMany({vencedor: "false"}, {$set: {vencedor: 0} })

## Em qual edição do Oscar "Crash" concorreu ao Oscar?

R: 2006.

db.registros.find({nome_do_filme: "Crash"}, {ano_cerimonia: 1}).limit(1)

## Bom... dê um Oscar para um filme que merece muito, mas não ganhou.

R: Clube da Luta merece demais.

db.registros.updateOne({nome_do_filme: /Fight Club/}, {$set: {vencedor: 1} })

## O filme Central do Brasil aparece no Oscar?

R: Sim, no ano de 1999.

db.registros.find({nome_do_filme: /Central/})

## Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser.

db.registros.insertMany([
    {
        "id_registro": 19831983,
        "ano_filmagem": 1983,
        "ano_cerimonia": 1984,
        "categoria": "BEST PICTURE",
        "nome_do_indicado": "Brian De Palma",
        "nome_do_filme": "Scarface",
        "vencedor": 1
    },
    {
        "id_registro": 20072007,
        "ano_filmagem": 2007,
        "ano_cerimonia": 2008,
        "categoria": "BEST PICTURE",
        "nome_do_indicado": "José Padilha",
        "nome_do_filme": "Tropa de Elite",
        "vencedor": 1
    },
    {
        "id_registro": 20082008,
        "ano_filmagem": 2008,
        "ano_cerimonia": 2009,
        "categoria": "ACTOR IN A LEADING ROLE",
        "nome_do_indicado": "Robert Downey Jr.",
        "nome_do_filme": "Homem de Ferro",
        "vencedor": 1
    }
]);


## Pensando no ano em que você nasceu: Qual foi o Oscar de melhor filme, Melhor Atriz e Melhor Diretor?

R: No ano de 2003 Chicago ganhou de melhor filme, Nicole Kidman ganhou de melhor atriz e Roman Polanski de melhor diretor.

db.registros.find({ano_cerimonia: 2003, vencedor: 1, categoria: "BEST PICTURE"})

db.registros.find({ano_cerimonia: 2003, vencedor: 1, categoria: "ACTRESS IN A LEADING ROLE"})

db.registros.find({ano_cerimonia: 2003, vencedor: 1, categoria: "DIRECTING"})
