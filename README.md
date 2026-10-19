# FICHA DE DECISÕES · War Room FiapBank (CP6 · 3 aulas)

> Este arquivo é o **README.md do repositório do grupo** (`cp6-warroom-<nome-do-grupo>`).
> Vale **5,0 pontos** (rodadas 0,5 · relâmpagos 0,3), e a nota é pela
> **justificativa**, não pela letra. Preencham após cada aula e commitem até
> **23h59 do mesmo dia** (regras completas na seção 5 do enunciado).
>
> **Os incidentes da madrugada são revelados só em aula.** O título de cada registro
> será **ditado pelo professor na hora**; ninguém se antecipe.

**Grupo (nome da equipe plantonista):** Grupo 23

**Turma:** 2CCPG **Repo:** `cp6---warroom---23`

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

1. Um integrante cria o repo **público** no GitHub: `cp6-warroom-<nome-do-grupo>`
   (ex.: `cp6-warroom-debugadores`), com um README qualquer.
2. Substituam o conteúdo do `README.md` por este template (no navegador, pelo próprio
   GitHub, ou clonando):

   ```bash
   git clone https://github.com/Pedro184294/cp6---warroom---23.git
   cd cp6---warroom---23
   git add README.md
   git commit -m "docs: atualiza ficha de decisoes do grupo"
   git push
   ```

3. Postem o **link no Teams** (o mesmo link para todo o grupo).

**Convenção de commits** (1 commit por rodada; relâmpagos podem ir junto com a
rodada seguinte):

```text
decisao: R1 - opcao C - corrige validacao de saldo
decisao: R2 - opcao A - parametriza consultas SQL
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

**Como escrever a justificativa:** nomeie o **mecanismo técnico** em jogo (o
conceito das Aulas 11 a 15 que explica o incidente) e o **trade-off** (velocidade ×
segurança × faturamento × dívida). "Porque é mais seguro" não é justificativa.

---

# 📝 REGISTRO DE DECISÕES

> A cada incidente, o professor dita o título (ex.: "Rodada 1"). **Copiem o modelo
> abaixo, colem no fim desta seção** e preencham com o rascunho feito em aula, junto
> com o **placar do grupo** após a consequência. Commitem 1 commit por rodada até
> 23h59 do dia.
>
> **Eventos relâmpago:** registrem apenas se o grupo for **afetado** (o professor
> chama quem for; não ser chamado é bom sinal).

*(Placar inicial: 🔥 7 · 💰 R$ 0 mil · 🧹 2)*

## Rodada 1 — O saldo que virou negativo

**Tipo:** rodada · **Voto:** C

**Decisão:** Corrigir a validação de saldo e adicionar um teste com `assertThrows`.

**Justificativa:**

A validação deve impedir que uma transferência deixe a conta com saldo negativo. O teste com `assertThrows` verifica se a operação sem saldo suficiente é recusada, protegendo a regra de negócio sem depender apenas de verificações manuais.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

## Rodada 2 — A injeção que derreteu o banco

**Tipo:** rodada · **Voto:** A

**Decisão:** Utilizar `PreparedStatement` com parâmetros vinculados.

**Justificativa:**

O uso de `PreparedStatement` com parâmetros vinculados evita a concatenação direta de valores na consulta SQL e reduz o risco de SQL Injection. A escolha prioriza a segurança das consultas sem abandonar a funcionalidade do sistema.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

## Relâmpago B — As conexões se fecham

**Tipo:** relâmpago · **Voto:** A

**Decisão:** Utilizar `try-with-resources` para liberar os recursos JDBC corretamente.

**Justificativa:**

O `try-with-resources` garante o fechamento automático de recursos, como conexões, statements e result sets, mesmo quando ocorre uma exceção. A solução corrige a causa do vazamento, em vez de apenas aumentar o pool de conexões e mascarar o problema.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

## Rodada 3 — A noite das contas gêmeas

**Tipo:** rodada · **Voto:** A

**Decisão:** Corrigir o método `getInstancia()` para reutilizar a instância do Singleton.

**Justificativa:**

O método deve retornar a instância existente, em vez de criar um novo `GeradorNumeroConta` a cada chamada. A correção preserva o comportamento esperado do padrão Singleton, embora a garantia de unicidade das contas também deva ser protegida por mecanismos apropriados no banco de dados.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 40 mil · 🧹 1

## Rodada 4 — O comprovante que aponta pra pessoa errada

**Tipo:** rodada · **Voto:** A

**Decisão:** Corrigir a ordem dos parâmetros de pagador e recebedor nas novas transferências.

**Justificativa:**

A ordem dos parâmetros precisa corresponder ao contrato do método e ao significado de cada campo. Corrigir o registro das novas transferências evita que os comprovantes identifiquem incorretamente quem pagou e quem recebeu, embora os registros históricos incorretos continuem precisando de tratamento próprio.

**Placar do grupo após esta decisão:** 🔥 10 · 💰 R$ 55 mil · 🧹 2

## Rodada 5 — A fábrica que devolveu null

**Tipo:** rodada · **Voto:** A

**Decisão:** Lançar uma exceção quando o tipo de conta informado for inválido.

**Justificativa:**

Retornar `null` para um tipo de conta inválido transfere o problema para quem utiliza a fábrica e pode provocar erros posteriores. Uma exceção explícita torna a falha identificável e facilita o tratamento correto pelo código chamador, em vez de permitir que um objeto inválido passe despercebido.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 2

## Relâmpago C — O cadastro com metade dos campos

**Tipo:** relâmpago · **Voto:** B

**Decisão:** Utilizar o padrão Builder com valores padrão e validação no método `build()`.

**Justificativa:**

O Builder permite montar objetos com vários campos de maneira mais legível e centralizar as validações antes da criação do objeto. Essa abordagem reduz a necessidade de múltiplos construtores e evita que instâncias incompletas sejam criadas silenciosamente.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 2

## Relâmpago D — O teste verde que não testa nada

**Tipo:** relâmpago · **Voto:** A

**Decisão:** Adicionar a asserção ausente para que o teste valide efetivamente o comportamento esperado.

**Justificativa:**

Um teste sem uma asserção adequada pode terminar sem detectar uma regressão, produzindo uma falsa sensação de segurança. Adicionar `assertEquals` ou `assertThrows`, conforme o cenário, faz com que a suíte verifique o resultado esperado em vez de apenas executar o código.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 1

## Rodada 6 — O teste vermelho às 03h45

**Tipo:** rodada · **Voto:** B

**Decisão:** Investigar e corrigir a taxa de TED, mesmo perdendo a janela de deploy.

**Evidência:**

```text
[ERROR] Tests run: 13, Failures: 1
[ERROR] TransferenciaServiceTest.tedDeveCobrarTaxaDe5Reais:
        expected: <5.0> but was: <50.0>
```

**Justificativa:**

O contrato de negócio estabelece que a taxa TED deve ser R$ 5,00, enquanto o serviço está retornando R$ 50,00. O teste vermelho identifica uma divergência real entre a implementação e o contrato. A equipe escolheu investigar o problema e corrigir o código, em vez de desativar o teste, alterar a expectativa ou realizar o deploy com a suíte falhando. O trade-off é perder a janela de deploy e adiar a publicação das correções, priorizando a integridade da cobrança e a confiabilidade da aplicação.

**Correção esperada:**

Substituir o valor incorreto por uma constante que represente a taxa definida no contrato e manter o teste verificando R$ 5,00.

```java
private static final double TAXA_TED = 5.00;
```

O cálculo da taxa TED deve utilizar `TAXA_TED`, e o teste deve continuar validando o valor contratual. A correção deve ser seguida da execução da suíte de testes antes do próximo deploy.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 85 mil · 🧹 0

---

## 🔎 O caminho do MEU grupo (preencher na 3ª aula, quando o mapa for revelado)

Uma linha por decisão registrada acima (usem os títulos ditados em aula):

| # | Decisão | Nossa letra | Consequência que ELA teria tido |
|---|---|---|---|
| 1 | O saldo que virou negativo | C | Corrige a validação de saldo e adiciona teste; 🔥 +1 · 💰 +35 mil · 🧹 −1 |
| 2 | A injeção que derreteu o banco | A | Parametriza consultas SQL; sem alteração no placar |
| 3 | As conexões se fecham | A | Corrige o vazamento de recursos JDBC; sem alteração no placar |
| 4 | A noite das contas gêmeas | A | Corrige o retorno do Singleton; 🔥 +1 · 💰 +5 mil |
| 5 | O comprovante que aponta pra pessoa errada | A | Corrige a ordem dos dados nas novas transferências; 🔥 +1 · 💰 +15 mil · 🧹 +1 |
| 6 | A fábrica que devolveu null | A | Falha explícita para tipo inválido; 🔥 −1 |
| 7 | O cadastro com metade dos campos | B | Builder com valores padrão e validação; sem alteração no placar |
| 8 | O teste verde que não testa nada | A | Adiciona asserção ao teste; 🧹 −1 |
| 9 | O teste vermelho às 03h45 | B | Corrige a taxa TED e perde a janela; 🔥 −1 · 💰 +30 mil · 🧹 −1 |

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
