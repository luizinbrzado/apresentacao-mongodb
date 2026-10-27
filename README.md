# MongoDB ao Vivo

Apresentação interativa sobre MongoDB: inserção, alteração e schemas, com casos reais de e-commerce e um simulador de mongosh rodando no próprio navegador.

**Abrir:** https://luizinbrzado.github.io/apresentacao-mongodb/

Não precisa instalar nada: é um único arquivo HTML, CSS e JS ([mongodb.html](mongodb.html)). Também funciona abrindo o arquivo direto no navegador.

## Atalhos

| Tecla | O que faz |
|---|---|
| → / Espaço / clique | avança (revela o próximo item ou roda o próximo comando) |
| ← | volta (o simulador volta junto) |
| O | mapa de cenas, com a parte de cada integrante |
| T | cronômetro da parte atual e do total |
| F | tela cheia |
| Home / End | início / fim |
| ? | ajuda |

O botão ☰ apagado no canto inferior esquerdo abre os controles. O endereço guarda a cena atual (`#cena.passo`), então recarregar a página não volta pro início.

## O que tem

- Estrutura do MongoDB (servidor, database, collection, document) e anatomia de um documento
- Inserção: `insertOne`, `insertMany`, `ordered`, validar cliente antes do pedido, índice `unique`
- Alteração: `$set`, `$inc`, `$push`/`$pull`/`$addToSet`, `$unset`, `upsert`, `findOneAndUpdate`, `bulkWrite` e transações
- Schemas: `$jsonSchema`, `validationLevel`, `validationAction`, `collMod`, embutir × referenciar
- Cola com os operadores, erros clássicos e um playground pra testar comandos

O simulador é uma implementação simplificada do MongoDB em JavaScript, feita para a apresentação. As respostas imitam o formato do mongosh, mas não é o banco de verdade.
