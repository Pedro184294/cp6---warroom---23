# FICHA DE DECISÕES · War Room FiapBank (CP6 · 3 aulas)

> Este arquivo é o **README.md do repositório do grupo** (`cp6-warroom-<nome-do-grupo>`).
> Vale **5,0 pontos** (rodadas 0,5 · relâmpagos 0,3), e a nota é pela
> **justificativa**, não pela letra.
>
> **Grupo:** 23 · **Turma:** 2CCPG
>
> **Repositório:** [cp6---warroom---23](https://github.com/Pedro184294/cp6---warroom---23)

**Grupo (nome da equipe plantonista):** Grupo 23

**Turma:** 2CCPG 

**Repo:** `cp6---warroom---23`

**Integrantes (nome + RM):**

| Nome                              | RM     |
| --------------------------------- | ------ |
| Pedro Luis Tofoli                 | 564441 |
| Fabricio Cardoso de Oliveira      | 561827 |
| Vinicius Barbosa Gomes            | 564854 |
| Leonardo Luster Gomes             | 564448 |
| Nelson Troccoli Santos Neto       | 562815 |
| Raphael Talarico Nascimento Silva | 565219 |

---

## 0. Setup do repositório

Repositório público criado para registrar as decisões tomadas durante a simulação War Room FiapBank, incluindo as justificativas técnicas, os efeitos das escolhas, o placar final e o relatório de Pós-Mortem.

**Link do repositório:** [https://github.com/Pedro184294/cp6---warroom---23](https://github.com/Pedro184294/cp6---warroom---23)

**Convenção de commits:**

```bash
git add README.md
git commit -m "decisao: R1 - opcao C - valida saldo"
git push
```

Para o registro final do Pós-Mortem:

```bash
git add README.md
git commit -m "pos-mortem: relatorio de incidente da madrugada"
git push
```

---

## 📁 Dossiê técnico do FiapBank (MVP em produção)

**Stack:** Java 17 + Spring Boot + Spring Data JPA + Oracle. API com endpoints em `/api/contas` e `/api/transferencias`.

**Contrato e regras de negócio que o banco prometeu aos clientes e aos reguladores:**

| Regra                    | Como deve ser                                                                   |
| ------------------------ | ------------------------------------------------------------------------------- |
| Transferência **PIX**    | Taxa **R$ 0,00**                                                                |
| Transferência **TED**    | Taxa fixa **R$ 5,00**                                                           |
| Saldo                    | Nunca fica negativo: transferência ou saque sem saldo é recusado com erro claro |
| Número de conta          | Sequencial e único, gerado pelo sistema                                         |
| Extrato de transferência | Registra quem pagou e quem recebeu, na ordem certa                              |
| CPF                      | Dado sensível: nunca aparece nas respostas da API                               |
| Consultas ao banco       | Sempre parametrizadas, e cada operação usa e libera a conexão                   |
| Suíte de testes          | Executada antes de todo deploy; testes verdes são pré-requisito para subir      |

**Como escrever a justificativa:** nomear o mecanismo técnico em jogo e o trade-off entre velocidade, segurança, faturamento e dívida técnica.

---

# 📝 REGISTRO DE DECISÕES

> Placar inicial: 🔥 7 · 💰 R$ 0 mil · 🧹 2

## R1 — O saldo que virou negativo

**Tipo:** Rodada · **Voto:** C

**Justificativa:**

Corrigir a validação do saldo e adicionar um teste com `assertThrows`. A validação impede que uma operação deixe a conta com saldo negativo, enquanto o teste verifica se uma operação inválida gera a exceção esperada. A decisão prioriza a integridade financeira.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

---

## R2 — A injeção que derreteu o banco

**Tipo:** Rodada · **Voto:** A

**Justificativa:**

Utilizar `PreparedStatement` com parâmetros vinculados para evitar que dados recebidos sejam interpretados como parte do comando SQL. A parametrização reduz o risco de SQL Injection e prioriza a segurança das consultas ao banco.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

---

## Flash A — A busca que não acha ninguém

**Tipo:** Relâmpago · **Voto:** Não aplicável

**Justificativa:**

O evento era direcionado aos grupos que escolheram a alternativa D na R1. Como o Grupo 23 escolheu C, este relâmpago não afetou o grupo.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

---

## Flash B — As conexões se fecham

**Tipo:** Relâmpago · **Voto:** A

**Justificativa:**

Utilizar `try-with-resources` para garantir o fechamento automático dos recursos JDBC, como conexões, comandos e resultados. O mecanismo reduz o risco de vazamento de recursos e melhora a confiabilidade do acesso ao banco de dados.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

---

## R3 — A noite das contas gêmeas

**Tipo:** Rodada · **Voto:** A

**Justificativa:**

Corrigir o método `getInstancia()` do Singleton para retornar a instância compartilhada do gerador de números de conta, em vez de criar um novo objeto a cada chamada. A decisão busca preservar a geração sequencial e única dos números de conta.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 40 mil · 🧹 1

---

## R4 — O comprovante que aponta pra pessoa errada

**Tipo:** Rodada · **Voto:** A

**Justificativa:**

Corrigir a ordem dos parâmetros de pagador e recebedor no registro das novas transferências. A ordem correta dos argumentos preserva a integridade do extrato e evita que as partes sejam registradas incorretamente. Os registros históricos incorretos permanecem como uma limitação identificada.

**Placar do grupo após esta decisão:** 🔥 10 · 💰 R$ 55 mil · 🧹 2

---

## R5 — A fábrica que devolveu null

**Tipo:** Rodada · **Voto:** A

**Justificativa:**

Lançar uma exceção quando o tipo de conta informado for inválido, em vez de retornar `null`. O tratamento explícito de entradas inválidas facilita a identificação do problema e reduz o risco de erros posteriores causados por referências nulas.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 2

---

## Flash C — O cadastro com metade dos campos

**Tipo:** Relâmpago · **Voto:** B

**Justificativa:**

Utilizar o padrão Builder com valores padrão e validação no método `build()`. O padrão organiza a criação de objetos com vários campos, enquanto a validação ajuda a impedir a construção de objetos incompletos ou inválidos.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 2

---

## Flash D — O teste verde que não testa nada

**Tipo:** Relâmpago · **Voto:** A

**Justificativa:**

Adicionar uma asserção, como `assertEquals` ou `assertThrows`, conforme o comportamento esperado. Um teste precisa verificar o resultado ou a exceção para detectar falhas; apenas executar o código não comprova que o comportamento está correto.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 1

---

## R6 — O teste vermelho às 03h45

**Tipo:** Rodada · **Voto:** B

**Justificativa:**

Investigar e corrigir a divergência da taxa TED: o contrato define R$ 5, mas o serviço retornava R$ 50. O grupo escolheu não desativar o teste nem alterar sua expectativa para esconder o problema. A decisão prioriza a regra de negócio e a qualidade dos testes, mesmo com o custo de perder a janela de deploy.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 85 mil · 🧹 0

---

## Flash E — A taxa é 5 ou 50?

**Tipo:** Relâmpago · **Voto:** Não aplicável

**Justificativa:**

O evento era condicionado às escolhas A, C ou D na R6. Como o Grupo 23 escolheu B, este relâmpago não afetou o grupo.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 85 mil · 🧹 0

---

## R7 — Go/No-Go da Black Friday

**Tipo:** Rodada · **Voto:** B

**Justificativa:**

Corrigir os problemas encontrados, garantir uma suíte de testes realmente verde e adiar a abertura por duas horas. O grupo priorizou a validação da aplicação antes do deploy, aceitando o atraso para reduzir o risco de disponibilizar um sistema bancário com falhas conhecidas.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 185 mil · 🧹 −1

> **Observação:** o placar segue os efeitos registrados nas rodadas. A dívida técnica chegou a −1; é necessário confirmar com o professor se o indicador pode assumir valores negativos ou se existe um limite mínimo de zero.

---

# 📊 PLACAR FINAL DO GRUPO

| Indicador         | Placar final |
| ----------------- | -----------: |
| 🔥 Reputação      |            9 |
| 💰 Caixa          |   R$ 185 mil |
| 🧹 Dívida técnica |           −1 |

## Perfil final — A Noite dos Heróis

O Grupo 23 se enquadra no perfil **A Noite dos Heróis**, pois terminou com reputação igual ou superior a 7 e dívida técnica igual ou inferior a 2.

> “Banco abriu, clientes confiam, time dorme (quase) em paz”.

**Perfis adicionais:**

| Perfil                | Condição                                | Resultado     |
| --------------------- | --------------------------------------- | ------------- |
| O Preço da Pressa     | 💰 Caixa igual ou superior a R$ 400 mil | Não se aplica |
| Firefighters Crônicos | 🧹 Dívida técnica igual ou superior a 6 | Não se aplica |

---

## 🔎 O caminho do MEU grupo

Uma linha por decisão registrada:

| #       | Decisão                                    | Nossa letra   | Consequência que ELA teria tido          |
| ------- | ------------------------------------------ | ------------- | ---------------------------------------- |
| R1      | O saldo que virou negativo                 | C             | 🔥 +1 · 💰 +R$ 35 mil · 🧹 −1            |
| R2      | A injeção que derreteu o banco             | A             | Sem alteração no placar                  |
| Flash A | A busca que não acha ninguém               | Não aplicável | Grupo não afetado, pois escolheu C na R1 |
| Flash B | As conexões se fecham                      | A             | Sem alteração no placar                  |
| R3      | A noite das contas gêmeas                  | A             | 🔥 +1 · 💰 +R$ 5 mil                     |
| R4      | O comprovante que aponta pra pessoa errada | A             | 🔥 +1 · 💰 +R$ 15 mil · 🧹 +1            |
| R5      | A fábrica que devolveu null                | A             | 🔥 −1                                    |
| Flash C | O cadastro com metade dos campos           | B             | Sem alteração no placar                  |
| Flash D | O teste verde que não testa nada           | A             | 🧹 −1                                    |
| R6      | O teste vermelho às 03h45                  | B             | 🔥 −1 · 💰 +R$ 30 mil · 🧹 −1            |
| Flash E | A taxa é 5 ou 50?                          | Não aplicável | Grupo não afetado, pois escolheu B na R6 |
| R7      | Go/No-Go da Black Friday                   | B             | 🔥 +1 · 💰 +R$ 100 mil · 🧹 −1           |

---

# 📋 PÓS-MORTEM · relatório de incidente

> Relatório elaborado com base nas decisões registradas pelo Grupo 23. As causas-raiz abaixo são interpretações técnicas dos incidentes descritos e devem ser ajustadas caso o professor tenha fornecido detalhes adicionais durante a terceira aula.

## 1. Linha do tempo da madrugada

A simulação começou com a necessidade de impedir que operações bancárias deixassem o saldo negativo. Em seguida, o grupo priorizou a proteção das consultas SQL e o fechamento adequado dos recursos JDBC.

Durante as rodadas seguintes, foram abordados problemas na geração de números de conta, no registro das partes de uma transferência e na criação de objetos com tipos inválidos. Os relâmpagos reforçaram a importância de validar os dados durante a construção dos objetos e de garantir que os testes realmente verifiquem os resultados.

Na R6, o grupo enfrentou a divergência da taxa TED: o contrato previa R$ 5, enquanto o serviço retornava R$ 50. A decisão foi investigar e corrigir o problema sem desativar o teste. Na R7, o grupo escolheu corrigir os problemas e adiar a abertura por duas horas para priorizar a validação da aplicação.

## 2. Causa raiz de 2 incidentes (aula + mecanismo técnico)

**Incidente 1:** O saldo que virou negativo

**Aula/mecanismo:** Validação de regras de negócio e testes automatizados.

A causa técnica identificada no cenário é a ausência ou insuficiência de uma validação que impeça operações sem saldo disponível. A regra precisa ser aplicada antes de concluir a operação, e testes como `assertThrows` podem verificar se a tentativa inválida é recusada. Isso reduz o risco de comprometer a integridade financeira das contas.

**Incidente 2:** O teste vermelho às 03h45

**Aula/mecanismo:** Testes automatizados, validação do contrato de negócio e correção da implementação.

O cenário apresentava divergência entre a taxa TED definida no contrato — R$ 5 — e o valor retornado pelo serviço — R$ 50. A causa técnica é a inconsistência entre a regra especificada e a implementação. A correção deve ocorrer no comportamento do sistema, mantendo o teste alinhado ao contrato, em vez de desativá-lo ou alterar a expectativa para esconder a falha.

## 3. O que faríamos diferente (2 rodadas + por quê)

**R1 — O saldo que virou negativo:** anteciparíamos a criação de testes para as regras financeiras críticas, incluindo saldo insuficiente, transferências e saques. Assim, falhas de validação seriam identificadas antes de afetarem outras funcionalidades.

**R6 — O teste vermelho às 03h45:** validaríamos a taxa TED e as demais regras de negócio com testes automatizados desde o início do desenvolvimento. Também executaríamos a suíte completa antes da janela de deploy, reservando tempo para investigar e corrigir falhas sem comprometer a qualidade da liberação.

## 4. A maior lição da equipe

A maior lição foi que, em um sistema bancário, a velocidade de entrega não pode substituir a segurança, a integridade dos dados e a validação do comportamento da aplicação.

Os incidentes mostraram que regras de negócio precisam estar refletidas no código e nos testes; consultas ao banco devem ser parametrizadas; recursos precisam ser liberados corretamente; e padrões de projeto devem ser implementados de forma consistente.

Na decisão final, o grupo aceitou adiar a abertura para corrigir os problemas e priorizar uma suíte de testes verde. Essa escolha reforçou que é melhor assumir um atraso controlado do que disponibilizar um sistema com falhas conhecidas.

