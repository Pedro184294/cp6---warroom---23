# FICHA DE DECISÕES · War Room FiapBank (CP6 · 3 aulas)

> Este arquivo é o **README.md do repositório do grupo** (`cp6-warroom-23`).
> Vale **5,0 pontos** (rodadas 0,5 · relâmpagos 0,3), e a nota é pela
> **justificativa**, não pela letra. Preencham após cada aula e commitem até
> **23h59 do mesmo dia** (regras completas na seção 5 do enunciado).
>
> **Os incidentes da madrugada são revelados só em aula.** O título de cada registro
> será **ditado pelo professor na hora**; ninguém se antecipe.

**Grupo (nome da equipe plantonista):** Grupo 23

**Turma:** 2CCPG 

**Repo:** [`cp6---warroom---23`](https://github.com/Pedro184294/cp6---warroom---23)

**Integrantes (nome + RM):**

| Nome | RM |
|---|---|
| Pedro Luis Tofoli | 564441 |
| Fabricio Cardoso de Oliveira | 561827 |
| Vinicius Barbosa Gomes | 564854 |
| Leonardo Luster Gomes | 564448 |
| Nelson Troccoli Santos Neto | 562815 |
| Raphael Talarico Nascimento Silva | 565219 |

## 0. Setup do repositório (antes da 1ª aula; podem apagar esta seção depois)

1. O repositório do grupo deve ser **público** no GitHub.
2. Substituam o conteúdo do `README.md` pela ficha preenchida.
3. Registrem as decisões com commits separados, seguindo a convenção definida pelo professor.
4. Postem o **link no Teams** (o mesmo link para todo o grupo).

**Convenção de commits** (1 commit por rodada; relâmpagos podem ir junto com a rodada seguinte):

```bash
decisao: R1 - opcao C (corrige saldo e adiciona teste)
decisao: R2 - opcao A (PreparedStatement com parametros vinculados)
decisao: R3 - opcao A (corrige Singleton do gerador de contas)
decisao: R4 - opcao A (corrige novos extratos)
decisao: R5 - opcao A (excecao para tipo de conta invalido)
decisao: Evento Relampago B - opcao A (fecha recursos JDBC)
decisao: Evento Relampago C - opcao B (Builder com valores padrao)
decisao: Evento Relampago D - opcao A (adiciona assert ao teste)
pos-mortem: relatorio de incidente da madrugada
```

---

## 📁 Dossiê técnico do FiapBank (MVP em produção)

**Stack:** Java 17 + Spring Boot + Spring Data JPA + Oracle. API com endpoints em
`/api/contas` e `/api/transferencias` (cenário visto desde a Aula 13).

**Contrato e regras de negócio que o banco prometeu aos clientes e aos reguladores:**

| Regra | Como deve ser |
|---|---|
| Transferência **PIX** | taxa **R$ 0,00** |
| Transferência **TED** | taxa fixa **R$ 5,00** |
| Saldo | **nunca fica negativo**: transferência/saque sem saldo é recusado com erro claro |
| Número de conta | **sequencial e único** (1001, 1002, 1003...), gerado pelo sistema |
| Extrato de transferência | grava **quem pagou** e **quem recebeu**, na ordem certa |
| CPF | **dado sensível**: nunca aparece nas respostas da API |
| Consultas ao banco | sempre parametrizadas, e cada operação **usa e libera** a conexão |
| Suíte de testes | roda antes de todo deploy; **verde** é pré-requisito pra subir |

**Como escrever a justificativa:** nomeie o **mecanismo técnico** em jogo (o conceito das Aulas 11 a 15 que explica o incidente) e o **trade-off** (velocidade × segurança × faturamento × dívida). "Porque é mais seguro" não é justificativa.

---

# 📝 REGISTRO DE DECISÕES

> A cada incidente, o professor dita o título. Registrem a decisão tomada pelo grupo,
> incluindo a justificativa técnica e o placar após a consequência.
>
> **Eventos relâmpago:** registrem apenas se o grupo for **afetado** e chamado pelo professor.

*(Placar inicial: 🔥 7 · 💰 R$ 0 mil · 🧹 2)*

---

## R1 — O saldo que virou negativo

**Tipo:** rodada · **Voto:** C

**Justificativa:**

Escolhemos corrigir a validação do saldo e adicionar um teste com `assertThrows` para verificar se a operação sem saldo suficiente é recusada. Corrigir a causa do problema junto com um teste automatizado reduz o risco de regressão e protege a regra de negócio, mesmo exigindo esforço adicional no desenvolvimento.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

---

## R2 — A injeção que derreteu o banco

**Tipo:** rodada · **Voto:** A

**Justificativa:**

Escolhemos utilizar `PreparedStatement` com parâmetros vinculados para evitar que dados informados pelo usuário sejam interpretados como parte do comando SQL. Essa abordagem reduz o risco de SQL Injection e protege a integridade dos dados, priorizando a segurança em vez de manter uma implementação vulnerável por conveniência.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

---

## ⚡ EVENTO RELÂMPAGO B — As conexões se fecham

**Tipo:** relâmpago · **Voto:** A

**Justificativa:**

Escolhemos utilizar `try-with-resources` para garantir o fechamento automático dos recursos JDBC ao final da operação, inclusive quando ocorre uma exceção. A correção resolve a causa do vazamento de conexões, enquanto apenas aumentar o tamanho do pool poderia esconder temporariamente o problema.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

---

## R3 — A noite das contas gêmeas

**Tipo:** rodada · **Voto:** A

**Justificativa:**

Escolhemos corrigir o método `getInstancia()` do Singleton, que estava criando uma nova instância de `GeradorNumeroConta` a cada chamada. A correção permite compartilhar a instância prevista pelo padrão, reduzindo a possibilidade de inconsistências na geração dos números. Como limitação, a unicidade entre múltiplas instâncias da aplicação também deve considerar o controle no banco de dados.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 40 mil · 🧹 1

---

## R4 — O comprovante que aponta pra pessoa errada

**Tipo:** rodada · **Voto:** A

**Justificativa:**

Escolhemos corrigir a ordem dos parâmetros da transferência para que pagador e recebedor sejam registrados corretamente nos novos comprovantes. A mudança evita que novas operações apresentem informações trocadas, embora os registros históricos incorretos permaneçam como um problema que precisa ser avaliado separadamente.

**Placar do grupo após esta decisão:** 🔥 10 · 💰 R$ 55 mil · 🧹 2

---

## R5 — A fábrica que devolveu null

**Tipo:** rodada · **Voto:** A

**Justificativa:**

Escolhemos lançar uma exceção quando o tipo de conta informado for inválido, em vez de retornar `null`. Essa decisão torna a falha explícita e facilita identificar o erro no ponto em que ocorre, reduzindo o risco de uma `NullPointerException` aparecer posteriormente em outra parte da aplicação. O trade-off é que a chamada passa a exigir tratamento adequado da exceção.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 2

---

## ⚡ EVENTO RELÂMPAGO C — O cadastro com metade dos campos

**Horário:** 02h20

**Tipo:** relâmpago · **Voto:** B

**Evidência:**

> Marketing: "a landing da madrugada vai cadastrar com SÓ nome e saldo, sem CPF, sem tipo. Faz ficar? O construtor atual exige tudo."

**Decisão:** Builder com valores padrão.

**Justificativa:**

Escolhemos utilizar o padrão Builder para permitir a criação da conta com apenas os campos necessários, concentrando os valores padrão e as validações no método `build()`. Essa abordagem evita aumentar a quantidade de construtores sobrecarregados e mantém a lógica de criação organizada. Também permite validar os dados antes de construir o objeto, reduzindo o risco de aceitar campos inválidos ou inconsistentes.

**Consequência técnica:** o Builder centraliza os valores padrão e as validações no momento da construção do objeto.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 2

---

## ⚡ EVENTO RELÂMPAGO D — O teste verde que não testa nada

**Horário:** 03h20

**Tipo:** relâmpago · **Voto:** A

**Evidência:**

O teste `depositoDeveCreditarValorInformado()` executava o método `depositar(50.0)`, mas não possuía nenhuma asserção para verificar o saldo resultante.

**Decisão:** adicionar o `assert` que falta.

**Justificativa:**

Escolhemos adicionar uma asserção ao teste para verificar se o depósito realmente credita o valor informado no saldo da conta. Um teste sem `assert` pode terminar com sucesso mesmo quando o comportamento esperado está incorreto, gerando falsa segurança antes do deploy. A correção exige pouco tempo, mas torna a suíte mais confiável e reduz o risco de regressões.

**Consequência técnica:** a suíte passa a verificar o comportamento esperado do depósito, em vez de apenas executar o método.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 1

---

## 📊 Resumo do placar atual

| Indicador | Placar |
|---|---:|
| 🔥 | 9 |
| 💰 | R$ 55 mil |
| 🧹 | 1 |

*O placar será atualizado após cada nova rodada ou evento relâmpago aplicável ao grupo.*

---

## 🔎 O caminho do MEU grupo (preencher na 3ª aula, quando o mapa for revelado)

Uma linha por decisão registrada acima (usem os títulos ditados em aula):

| # | Decisão | Nossa letra | Consequência que ELA teria tido |
|---|---|---|---|
| 1 | R1 — O saldo que virou negativo | C | Corrige a validação do saldo e adiciona teste automatizado. |
| 2 | R2 — A injeção que derreteu o banco | A | Utiliza `PreparedStatement` com parâmetros vinculados. |
| 3 | Evento Relâmpago B — As conexões se fecham | A | Fecha os recursos JDBC automaticamente com `try-with-resources`. |
| 4 | R3 — A noite das contas gêmeas | A | Corrige o Singleton do gerador de números de conta. |
| 5 | R4 — O comprovante que aponta pra pessoa errada | A | Corrige a ordem dos dados nos novos comprovantes. |
| 6 | R5 — A fábrica que devolveu null | A | Lança exceção para tipo de conta inválido. |
| 7 | Evento Relâmpago C — O cadastro com metade dos campos | B | Utiliza Builder com valores padrão e validação no `build()`. |
| 8 | Evento Relâmpago D — O teste verde que não testa nada | A | Adiciona uma asserção para verificar o resultado do depósito. |

*(Adicionem linhas conforme as decisões da madrugada.)*

---

# 📋 PÓS-MORTEM · relatório de incidente (montar em sala na 3ª aula)

> Rascunho em aula e commit final `pos-mortem:` até 23h59 do dia da 3ª aula.

## 1. Linha do tempo da madrugada

_______________________________________________________________________________________

_______________________________________________________________________________________

_______________________________________________________________________________________

## 2. Causa raiz de 2 incidentes (aula + mecanismo técnico)

**Incidente 1:** _______________________________________________

Aula/mecanismo:

_______________________________________________________________________________________

**Incidente 2:** _______________________________________________

Aula/mecanismo:

_______________________________________________________________________________________

## 3. O que faríamos diferente (2 rodadas + por quê)

_______________________________________________________________________________________

_______________________________________________________________________________________

## 4. A maior lição da equipe

_______________________________________________________________________________________
