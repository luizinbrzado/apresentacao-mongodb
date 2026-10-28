# Roteiro — MongoDB ao Vivo

Roteiro pra quem vai apresentar. Não precisa decorar: lê o que tá entre aspas pra pegar a ideia e fala do seu jeito.

---

## Antes de começar

**Link:** https://luizinbrzado.github.io/apresentacao-mongodb/
(também funciona abrindo o `mongodb.html` direto, sem internet — só a fonte muda)

**Teclas que importam:**

| Tecla | Pra quê |
|---|---|
| **→**, **Espaço** ou clique | avança (mostra o próximo pedaço ou roda o próximo comando) |
| **←** | volta (o simulador volta junto) |
| **F** | tela cheia (aperta isso antes de começar) |
| **O** | mapa das cenas — pra pular direto pra sua parte |
| **T** | cronômetro (só aparece se apertar; aperta de novo pra esconder) |
| **☰** no canto inferior esquerdo | abre os botões de voltar/avançar, se precisar do mouse |

**Coisas boas de saber:**

- Cada clique mostra **uma coisa só**. Fala, e só depois clica.
- Quando aparece um comando sendo digitado, **espera ele terminar**. Se clicar no meio, ele só pula a animação, não perde nada.
- A caixa verde no terminal é **a resposta do MongoDB**. A vermelha é **erro**. Sempre aponta pra ela.
- Na tabela/coleção do lado direito, **verde piscando = mudou**, **riscado em vermelho = apagou**.
- Se der F5 sem querer, ele volta pra mesma cena.

**Divisão:**

| Parte | Cenas | Assunto | Tempo |
|---|---|---|---|
| **1** | 1 – 20 | Abertura, conceitos e Inserção | ~14 min |
| **2** | 21 – 43 | Alteração | ~13 min |
| **3** | 44 – 67 | Schemas, cola, erros, playground e Kahoot | ~10 min (+ playground) |

Na hora de trocar, quem sai fala a frase de passagem que tá no fim da parte dele.

---

## Parte 1 — Abertura, conceitos e Inserção

### 1 · Capa
> "Boa noite, pessoal. Nosso tema é o 4: MongoDB, manipulação de dados. A gente vai ver como inserir, como alterar e como colocar regra nos dados."

### 2 · O cenário
> "Pra não ficar naquele exemplo de 'aluno e nota', a gente vai fingir uma coisa: **vocês são os programadores de uma loja online**. Tem cliente, produto, carrinho, pedido, pagamento… e a Black Friday é sexta-feira. Tudo que a gente mostrar aqui é problema que acontece de verdade em loja online."

### 3 · Agenda
> "Vai ser assim: primeiro inserção, depois alteração, depois schemas, que são as regras. No fim tem uma cola com tudo e os erros que todo mundo comete. E fechando, Kahoot."

### 4 · Hierarquia
Vai clicando e deixa cada caixa aparecer.
> "Antes de tudo, onde o dado mora? De fora pra dentro: tem o **servidor**, que é o MongoDB rodando. Dentro dele, vários **bancos** — o nosso se chama `loja`. Dentro do banco ficam as **collections**: clientes, produtos, pedidos. E dentro de cada collection, os **documentos**, que são os registros."

No último clique:
> "E no código é isso: `use loja` escolhe o banco, `db.clientes` é a collection, e o `.find()` traz os documentos."

### 5 · Anatomia do documento
Cada clique acende **uma parte** do documento. Aponta pra parte colorida.
> 1. "Tudo entre chaves é **um documento**. É tipo uma linha da tabela, só que com estrutura dentro."
> 2. "O `_id` é a chave primária. Todo documento tem, e não pode repetir."
> 3. "O nome antes dos dois-pontos é o **campo**. É a 'coluna'."
> 4. "O que vem depois é o **valor**."
> 5. "E cada valor tem **tipo**: texto, número inteiro, verdadeiro/falso, data… Guardem isso, vai voltar."
> 6. "Isso aqui é um **subdocumento**: um documento dentro do outro. Pra acessar, usa ponto: `endereco.cidade`."
> 7. "Isso é um **array**, uma lista."
> 8. "E isso é uma **lista de documentos**. Os pedidos tão guardados dentro do cliente."
> 9. "Tudo junto. Duas regrinhas: no máximo **16 MB** por documento, e o próximo cliente pode ter **campos diferentes** desse."

### 6 · Vocabulário
> "Se vocês vêm do SQL: tabela vira collection, linha vira document, coluna vira field, e o JOIN… existe, se chama `$lookup`, mas a gente quase não precisa. Já já vocês vão ver por quê."

### 7 · Por que documento?
> "Por que isso é bom? Olha o catálogo da loja: um notebook tem memória e processador. Uma camiseta tem tamanho e cor. Um livro tem autor. No SQL você ia ter uma tabela com um monte de coluna vazia. Aqui, cada produto tem só o que precisa."

### 8 · BSON
> "Uma curiosidade: o Mongo não guarda JSON, guarda **BSON**, que é um JSON binário. A diferença é que ele tem tipos que o JSON não tem: ObjectId, data, número decimal… Isso importa, porque lá na frente a validação vai cobrar o tipo certo."

### 9 · 0.1 + 0.2
> "Pergunta rápida: quanto dá 0.1 + 0.2?"
(espera alguém responder 0.3)
> "Pro computador, dá isso aqui: 0.30000000000000004. Número 'quebrado' comum não representa 0,1 certinho. Numa loja com um milhão de pedidos, isso vira dinheiro sumindo. Por isso, **dinheiro se guarda como Decimal128**, ou em centavos."

### 10 · Ato 1 · Inserção
> "Bora pra primeira parte: colocar dados no banco. Situação: alguém acabou de clicar em 'Criar conta'."

### 11 · insertOne · código
O código fica parado e cada clique explica uma linha. Lê a caixa de baixo com suas palavras.
> - "`db` é o banco, `clientes` é a collection. Se ela não existir, o Mongo cria sozinho."
> - "`insertOne` recebe **um** documento."
> - "Aqui são os campos. Não precisei criar tabela antes."
> - "`new Date()` grava uma data de verdade, não um texto."
> - "E o `_id`? Eu não mandei nenhum… vamos rodar pra ver."

### 12 · insertOne · ao vivo
Clica e deixa o comando ser digitado.
> "Olha a resposta do Mongo, ali na caixa verde: ele devolveu um `insertedId`. Eu não mandei `_id`, então **ele criou um pra mim**. Isso é um ObjectId… e ele não é aleatório."

### 13 · ObjectId
> "Esse número foi gerado agora, nesse computador. Ele tem três pedaços: os primeiros 4 bytes são **a data e a hora** em que foi criado — dá pra ver aqui. Depois um pedaço aleatório da máquina, e no fim um contador. Ou seja: dá pra saber quando um cliente se cadastrou **sem precisar de um campo de data**."

### 14 · insertMany · código
> "E se for a planilha do fornecedor, com 10 mil produtos? Não dá pra fazer 10 mil `insertOne`. Usa o `insertMany`, que recebe uma **lista**. Repara que aqui eu escolhi o `_id`: é o próprio código do produto, o SKU. E cada produto tem campos diferentes, sem problema."

### 15 · ordered: true
> "Agora o problema: a planilha tem um produto que **já existe**, o SKU-203. O que acontece?"
(roda)
> "Erro de chave duplicada. Olha a coleção: entrou o 201 e o 202, **parou no 203**, e o 204 e o 205 ficaram de fora. E atenção: o 201 e o 202 **não foram desfeitos**. Erro no meio não volta atrás."

### 16 · ordered: false
> "Mesma planilha, mas agora com `ordered: false`."
(roda)
> "Ele pulou o repetido e seguiu: entraram 4. O erro volta numa lista pra você tratar depois. Importação grande, onde você já espera erro? É `ordered: false`."

### 17 · Sem FOREIGN KEY
> "Agora vou criar um pedido pro cliente 999. Detalhe: esse cliente **não existe**."
(roda)
> "Entrou. Sem erro nenhum. O MongoDB **não tem chave estrangeira**. Nem o schema resolve isso, porque ele só olha o próprio documento. Ficou um pedido órfão. Quem tem que conferir é **a aplicação**, o nosso código."

### 18 · Validar antes de criar · código
> - "Então, antes de criar o pedido, a gente pergunta pro banco: esse cliente existe? O `findOne` devolve o documento ou `null`."
> - "No filtro eu peço que exista **e esteja ativo** — conta bloqueada também não compra."
> - "Esse `{ _id: 1 }` diz: me traz só o `_id`. Não preciso do cadastro inteiro."
> - "Veio `null`? Para tudo e devolve erro."
> - "Só depois cria o pedido, usando o `_id` que **veio do banco**."
> - "Também dá pra usar `countDocuments`, que devolve 0 ou 1."

### 19 · Validar antes de criar · ao vivo
> - "Cliente 999: `null`. Não existe, não cria nada."
> - "Cliente 8, o Caio: ele existe, mas tá inativo. Também volta `null`. O filtro barrou."
> - "Cliente 7, a Marina: voltou o `_id` dela. Pode seguir."
> - "E aí sim o pedido é criado."

### 20 · Cadastro duplicado · unique
> "E se a pessoa clicar **duas vezes** em 'Criar conta'? Aqui a gente cria um índice `unique` no email: o próprio banco garante um cadastro por email."
(roda o segundo clique)
> "Barrado. E por que não fazer só um `findOne` antes? Porque os dois cliques chegam no mesmo milissegundo, e **os dois** passam no `findOne`. Quem garante de verdade é o índice."

**Passagem:** "Então é isso: colocar dados no banco. Agora o [nome] vai mostrar como mudar o que já tá lá."

---

## Parte 2 — Alteração

### 21 · Ato 2 · Alteração
> "Situação: o pagamento do pedido 1042 foi aprovado. Precisa mudar o status dele."

### 22 · Anatomia do update
> - "`updateOne` muda **no máximo um** documento."
> - "Todo update tem duas partes. A primeira é o **filtro**: quem vai mudar. É igual ao WHERE."
> - "A segunda é o **operador**: o que muda. O `$set` define o valor do campo."
> - "Se esquecer o operador, o Mongo recusa. Isso é um erro muito comum."

### 23 · updateOne · ao vivo
> "Rodei: `matchedCount: 1` quer dizer que **achou**, e `modifiedCount: 1` quer dizer que **mudou**. Olha o 1042 piscando na tabela."
(roda de novo)
> "O gateway avisou de novo. Achou, mas `modified` é 0: já tava 'pago', então nada foi regravado."

### 24 · updateMany · código
> - "Black Friday: 20% de desconto em **todos** os eletrônicos. O filtro pega todos, não só o primeiro."
> - "O `$mul` multiplica dentro do banco: preço vezes 0,8."
> - "E dá pra usar dois operadores juntos no mesmo update."

### 25 · Black Friday · ao vivo
> "Meia-noite, liga a Black Friday. Três produtos mudaram, olha os preços piscando. A camiseta ficou de fora, porque o filtro era só eletrônico."

### 26 · Bug do replaceOne
> "Agora um bug real. A tela 'Editar perfil' manda só nome e email. O programador usou `replaceOne`…"
(roda)
> "Olha o que aconteceu: cidade, telefone e **1.280 pontos de fidelidade** sumiram. O `replaceOne` troca o documento **inteiro**. Só o `_id` fica."

### 27 · $set resolve
> "Mesma tela, agora com `$set`. Só o nome mudou, o resto ficou intacto. Resumindo: `$set` é bisturi, `replaceOne` é demolição."

### 28 · Corrida pela última unidade
Vai clicando linha por linha da tabela.
> "Black Friday, meia-noite e um segundo. Sobrou **uma** Air Fryer. Dois clientes clicam em comprar ao mesmo tempo. O A lê o estoque: 1. O B lê o estoque: 1. O A grava 0. O B grava 0…"
> "Resultado: **vendeu duas, tinha uma**. Isso se chama condição de corrida. Acontece quando a aplicação lê, faz a conta e grava."

### 29 · $inc atômico · código
> - "A correção: no filtro eu peço o produto **só se ainda tiver estoque**."
> - "E o `$inc` faz a conta **dentro do banco**: menos 1."
> - "Filtro e alteração acontecem juntos, de uma vez só."
> - "E o resultado diz quem ganhou: `modifiedCount` 1 vendeu, 0 é esgotado."

### 30 · $inc · ao vivo
> "Cliente A: `modifiedCount: 1`, levou. Estoque 0."
> "Cliente B, no mesmo segundo: `matchedCount: 0`. O filtro não achou nada, a tela mostra 'Esgotado'. O estoque **nunca fica negativo**."

### 31 · bulkWrite · código
> - "E se o carrinho tiver vários itens? O `bulkWrite` manda várias operações numa ida só ao banco."
> - "Cada item é um `updateOne` igualzinho ao que a gente viu."
> - "Com a mesma proteção de estoque."
> - "Dá pra misturar inserir, alterar e apagar."
> - "Mas atenção: ele **não é tudo ou nada**. Bora ver."

### 32 · bulkWrite · ao vivo
> "Carrinho: 2 fones e 2 Air Fryers. O fone baixou de 37 pra 35. A Air Fryer não, porque só tinha uma. O cliente **não vai levar** o carrinho, mas 2 fones já saíram do estoque. Meio checkout."

### 33 · Por que transação?
> "Um checkout de verdade mexe em 3 collections: baixa o estoque, cria o pedido, grava o pagamento. Se a API cair no meio, o estoque baixou e o pedido **não existe**."
> "Pra isso existe a **transação**: ou acontece tudo, ou não acontece nada. O Mongo tem isso desde a versão 4.0."

### 34 · Transação · código
> - "Abre uma **sessão**, que agrupa as operações."
> - "As collections são acessadas **pela sessão**, senão ficam de fora."
> - "`startTransaction`: daqui pra baixo, nada é definitivo."
> - "Baixa o estoque, com a mesma proteção."
> - "Esgotou? Lança um erro e pula pro `catch`."
> - "Cria o pedido, em outra collection, na mesma transação."
> - "`commitTransaction`: agora vale tudo junto."
> - "Deu erro? `abortTransaction` desfaz **tudo**."
> - "Transação custa mais. Usa quando várias escritas precisam andar juntas."

### 35 · Transação · ao vivo
> "Mesmo carrinho, agora com transação. Abre a transação. Baixa 2 fones: 35, por enquanto. Tenta 2 Air Fryers: esgotada. Aí a API desiste…"
(roda o abort)
> "Olha o fone: **voltou pra 37**. Nada ficou pela metade."

### 36 · Arrays
> "Agora listas. `$push` adiciona no fim, tipo 'adicionar ao carrinho'. `$pull` tira pelo valor, 'remover do carrinho'. E `$addToSet` só adiciona **se não existir ainda**."

### 37 · Carrinho · ao vivo
> - "`$push`: o produto entrou no fim do carrinho."
> - "`$pull`: tirei pelo valor, nem precisei saber a posição."
> - "Agora: toda vez que o app abre, ele manda o ID do celular pra receber notificação. Com `$addToSet`, se já tá lá, `modifiedCount` 0. Nada duplicou."
> - "E se fosse `$push`? Duplicou. Cinquenta aberturas, cinquenta cópias, **a mesma notificação 50 vezes**."

### 38 · LGPD · $unset
> "Pela LGPD, a cliente pediu pra apagar os dados pessoais. O `$unset` **remove o campo** — não deixa vazio, o campo deixa de existir. Mas olha: os pedidos dela continuam, porque o financeiro ainda precisa do histórico."

### 39 · Webhook duplicado
> "Mais um caso real: o gateway de pagamento avisa 'pagou'… duas vezes. Isso acontece direto: se ele não recebe resposta a tempo, ele reenvia. Se a gente usar `insertOne`, ficam dois pagamentos pro mesmo pedido."

### 40 · upsert · código
> - "A solução: o filtro usa o **id do evento** que o gateway manda."
> - "Achou? Atualiza."
> - "Com `upsert: true`: não achou? **Cria**."
> - "Resultado: chegando 1 aviso ou 10, o estado final é o mesmo. Isso se chama **idempotência**."

### 41 · upsert · ao vivo
> "Primeiro aviso: não existia, então criou. Agora o gateway reenvia… Já existia, só atualizou. Continua **um documento só**."

### 42 · findOneAndUpdate · código
> - "Último caso: gerar o número do próximo pedido. O `findOneAndUpdate` altera **e devolve** o documento numa operação só."
> - "Cada chamada soma 1, então dois pedidos nunca pegam o mesmo número."
> - "Com `returnDocument: 'after'` ele devolve o valor **novo**."
> - "Pegadinha: sem isso, ele devolve o valor **antigo**."

### 43 · Número do pedido · ao vivo
> "Sem o 'after': devolveu 1042, mas o banco já tá em 1043. Cuidado! Com o 'after': 1044, que é o número que o pedido vai usar de verdade."

**Passagem:** "Isso é como alterar dados. Mas e se o dado chegar errado? Pra isso tem o schema, e quem mostra é o [nome]."

---

## Parte 3 — Schemas, cola, erros e playground

### 44 · Ato 3 · Schemas
> "O Mongo tem schema flexível. Mas flexível **não quer dizer sem regra**."

### 45 · Bug do total em texto
> "O front-end mandou o total como texto, '59,90'."
(roda)
> "Entrou. Sem erro, sem aviso."
(roda o relatório)
> "No fim do mês, o relatório de faturamento… deveria dar 269,80. Deu 209,90. O `$sum` **ignora texto**. Sumiram 59,90 do relatório, e ninguém viu."

### 46 · $jsonSchema · código
> - "A correção: criar a collection **já com regra**."
> - "O `$jsonSchema` é onde a regra fica."
> - "`required`: se faltar um desses campos, nem entra."
> - "O total tem que ser **decimal**. Texto é barrado."
> - "`enum`: o status só pode ser um desses. 'Pago' com P maiúsculo não passa."
> - "Os itens não são obrigatórios, mas se vierem, têm que ser lista com pelo menos um."

### 47 · Validação · ao vivo
> - "Total em texto: barrado na porta."
> - "'Pago' com maiúsculo: o enum não aceita."
> - "Agora certo: entrou. O banco protegeu o relatório de amanhã."

### 48 · Level & action
> "E se a collection já tem 2 milhões de pedidos antigos fora da regra? Tem dois controles. O `validationAction`: com **error** ele bloqueia, com **warn** ele deixa entrar e só avisa no log. E o `validationLevel`: **strict** valida tudo, **moderate** não cobra de quem já era inválido. O padrão é strict + error."

### 49 · Apertando a regra no legado
> "Na vida real se faz em 3 passos: liga a regra com moderate + warn, nada quebra, e você lê o log. Depois corrige os dados antigos. E só aí muda pra strict + error."

### 50 · collMod · código
> - "Pra mudar a regra de uma collection que já existe, usa o `collMod`."
> - "A regra nova **substitui** a antiga inteira."
> - "Moderate: documento antigo inválido não trava."
> - "Warn: não bloqueia nada, só registra."

### 51 · moderate · ao vivo
> "O pedido 900 é antigo e tá fora da regra. Com moderate, o update **passa**. Mas um pedido que era válido **não pode virar** inválido: erro."

### 52 · Embutir ou referenciar
> "Pra fechar schemas: como você **lê** decide como você **guarda**. Se lê sempre junto, **embute**. Se é dado compartilhado ou cresce sem fim, **referencia** pelo `_id`."

### 53 · Um pedido de verdade
> - "O cliente é **referência**: ele é um só e tem vários pedidos."
> - "O endereço é **embutido**: é uma foto da hora da compra. Se a Marina se mudar, o pedido antigo não muda."
> - "Os itens com o **preço da época**. Se a Air Fryer subir de preço, a nota antiga continua certa."
> - "Uma leitura e você tem o pedido inteiro. Sem JOIN."

### 54 · Post viral · 16 MB
> "E quando **não** embutir? Um post viral com 300 mil comentários dentro dele estoura o limite de 16 MB. Coisa que cresce sem fim vai em outra collection, com referência."

### 55 a 61 · Cola (7 slides)
Passa rápido, uns 15 segundos cada.
> "Aqui é a cola de tudo que a gente viu, e um pouco mais: os métodos, os filtros, os operadores de update, as regras de schema e a transação. Não precisa ler tudo agora: o link vai ficar com vocês."

Se sobrar tempo, aponta um ou dois que a gente não mostrou ao vivo, tipo `$in`, `$exists` ou `$regex`.

### 62 · Erros clássicos 1/2
> "Agora os erros que **todo mundo** comete, e que aparecem direto no Stack Overflow:
> 1. update sem `$set` — o Mongo recusa;
> 2. buscar o `_id` como texto — volta vazio;
> 3. `$set` no subdocumento inteiro — apaga o resto;
> 4. `updateOne` com filtro vazio achando que muda todos — muda só um."

### 63 · Erros clássicos 2/2
> "5. repetir o campo no filtro — o JavaScript fica só com o último;
> 6. número entre aspas — texto só compara com texto;
> 7. `$push` com lista — vira lista dentro de lista;
> 8. procurar `null` — também traz quem nem tem o campo."

### 64 · Playground · abertura
> "Agora é com vocês. Tem um terminal aqui que roda comando de verdade no simulador."

### 65 · Playground
- Os botões **verdes** rodam exemplos prontos. Os **vermelhos** rodam os erros clássicos e mostram a explicação.
- Depois de um vermelho, aparece **🔧 Consertar**: ele desfaz o estrago e roda o comando certo.
- Pode digitar e apertar **Enter** ou **▶ Enviar**. Se o comando ficar grande, o terminal ganha barra de rolagem.
- Pede pra turma escolher: "Qual erro vocês querem ver?"
- Se o tempo tiver curto, pula essa.

### 66 a 68 · Final automático (Fontes → Kahoot → Equipe)
Daqui pra frente **não precisa apertar nada**. Chegou em Fontes avançando, o resto anda sozinho (~16 segundos):

1. **Fontes** se monta e fica 5 segundos.
   > "As fontes foram a documentação oficial do MongoDB, o Stack Overflow e o fórum da comunidade."
2. **Kahoot** fica 5 segundos.
   > "Já já tem Kahoot, então celular na mão: kahoot.it."
3. **Equipe** aparece: o comando, os nomes, a resposta do banco e o "Obrigado!".
   > "E pra fechar, a última inserção do dia: a nossa equipe. Três documentos, `insertedCount: 3`. Obrigado!"

Depois abre o Kahoot no outro computador ou aba e passa o código.

- Apertar **→** no meio adianta, e a sequência continua dali.
- Apertar **←** para a sequência. Pra retomar, é só apertar **→**.
- Se abrir direto numa dessas cenas (F5 ou mapa **O**), ela só começa quando apertar **→**.

---

## Se o tempo apertar

Dá pra pular sem perder a história:

- **Parte 1:** cena 9 (0.1 + 0.2) e cena 13 (ObjectId).
- **Parte 2:** cenas 31 e 32 (bulkWrite) — vai direto da 30 pra 33.
- **Parte 3:** cola (55–61) bem rápida e o playground (64–65).

Pra pular, aperta **O** e clica na cena.

## Se der algo errado

- **Apertou sem querer?** Seta pra esquerda volta, e o simulador volta junto.
- **A tela travou num comando?** Aperta → de novo, que ele termina a animação.
- **Sumiu da tela cheia?** Aperta **F**.
- **Perdeu a cena?** Aperta **O** e escolhe no mapa.
