# FICHA DE DECISÕES · War Room FiapBank (CP6 · 3 aulas)

> Este arquivo é o **README.md do repositório do grupo**.
>
> Registro das decisões tomadas durante a dinâmica, suas justificativas técnicas, os impactos na pontuação e o perfil final da noite.
>
> **Grupo:** 23 · **Turma:** 2CCPG

**Grupo (nome da equipe plantonista):** Grupo 23

**Turma:** 2CCPG  
**Repo:** [`cp6---warroom---23`](https://github.com/Pedro184294/cp6---warroom---23)

**Integrantes (nome + RM):**

| Nome | RM |
|---|---:|
| Pedro Luis Tofoli | 564441 |
| Fabricio Cardoso de Oliveira | 561827 |
| Vinicius Barbosa Gomes | 564854 |
| Leonardo Luster Gomes | 564448 |
| Nelson Troccoli Santos Neto | 562815 |
| Raphael Talarico Nascimento Silva | 565219 |

---

## 0. Setup do repositório

O repositório público do grupo foi criado para registrar as decisões tomadas durante a dinâmica War Room FiapBank.

**Link do repositório:** https://github.com/Pedro184294/cp6---warroom---23

**Convenção de commits:**

```bash
git add README.md
git commit -m "epilogo: placar final e perfil da noite"
git push
```

---

## 📁 Dossiê técnico do FiapBank (MVP em produção)

**Stack:** Java 17 + Spring Boot + Spring Data JPA + Oracle. API com endpoints em `/api/contas` e `/api/transferencias`.

**Contrato e regras de negócio que o banco prometeu aos clientes e aos reguladores:**

| Regra | Como deve ser |
|---|---|
| Transferência **PIX** | Taxa **R$ 0,00** |
| Transferência **TED** | Taxa fixa **R$ 5,00** |
| Saldo | **Nunca fica negativo**: transferência ou saque sem saldo é recusado com erro claro |
| Número de conta | **Sequencial e único** (1001, 1002, 1003...), gerado pelo sistema |
| Extrato de transferência | Registra **quem pagou** e **quem recebeu**, na ordem certa |
| CPF | **Dado sensível**: nunca aparece nas respostas da API |
| Consultas ao banco | Sempre parametrizadas, com os recursos utilizados liberados corretamente |
| Suíte de testes | Executada antes de todo deploy; **verde** é pré-requisito para subir |

**Como escrever a justificativa:** nomear o mecanismo técnico envolvido e explicar o trade-off entre velocidade, segurança, faturamento e dívida técnica.

---

# 📝 REGISTRO DE DECISÕES

> As decisões abaixo registram as escolhas feitas pelo grupo durante a dinâmica, incluindo o placar após cada consequência.

**Placar inicial:** 🔥 7 · 💰 R$ 0 mil · 🧹 2

---

## R1 — O saldo que virou negativo

**Tipo:** Rodada · **Voto:** C

**Justificativa:**

O grupo escolheu corrigir a validação do saldo e adicionar um teste para impedir operações que deixem a conta negativa. A decisão prioriza a integridade financeira e a confiabilidade do sistema, reduzindo o risco de inconsistências nas operações bancárias.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | +1 |
| 💰 Receita | +R$ 35 mil |
| 🧹 Dívida técnica | -1 |

---

## R2 — A injeção que derreteu o banco

**Tipo:** Rodada · **Voto:** A

**Justificativa:**

O grupo escolheu utilizar `PreparedStatement` com parâmetros vinculados para evitar a concatenação direta de entradas nas consultas SQL. A decisão prioriza a segurança e reduz o risco de SQL Injection.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | 0 |
| 💰 Receita | R$ 0 mil |
| 🧹 Dívida técnica | 0 |

---

## Flash A — A busca que não acha ninguém

**Tipo:** Relâmpago · **Situação:** Não aplicável

O evento era destinado aos grupos que escolheram a opção D na R1. Como o grupo escolheu a opção C, este Flash não foi contabilizado como decisão do grupo.

---

## Flash B — As conexões se fecham

**Tipo:** Relâmpago · **Voto:** A

**Justificativa:**

O grupo escolheu utilizar `try-with-resources` para garantir o fechamento automático dos recursos JDBC. Essa abordagem reduz o risco de vazamento de conexões e melhora a organização do acesso ao banco de dados.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | 0 |
| 💰 Receita | R$ 0 mil |
| 🧹 Dívida técnica | 0 |

---

## R3 — A noite das contas gêmeas

**Tipo:** Rodada · **Voto:** A

**Justificativa:**

O grupo escolheu corrigir o Singleton do gerador de números de conta. O método `getInstancia()` deveria retornar a mesma instância, mas criava uma nova a cada chamada. A correção busca garantir o comportamento esperado do gerador e reduzir o risco de duplicidade de números de conta.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 40 mil · 🧹 1

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | +1 |
| 💰 Receita | +R$ 5 mil |
| 🧹 Dívida técnica | 0 |

---

## R4 — O comprovante que aponta pra pessoa errada

**Tipo:** Rodada · **Voto:** A

**Justificativa:**

O grupo escolheu corrigir a ordem dos parâmetros utilizados no registro das transferências, garantindo que o pagador e o recebedor sejam identificados corretamente nas novas operações. Os registros históricos incorretos permanecem sem correção nessa alternativa.

**Placar do grupo após esta decisão:** 🔥 10 · 💰 R$ 55 mil · 🧹 2

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | +1 |
| 💰 Receita | +R$ 15 mil |
| 🧹 Dívida técnica | +1 |

---

## R5 — A fábrica que devolveu null

**Tipo:** Rodada · **Voto:** A

**Justificativa:**

O grupo escolheu lançar uma exceção quando o tipo de conta informado for inválido, em vez de retornar `null`. Essa abordagem deixa o erro explícito e facilita o tratamento de situações inválidas, reduzindo o risco de falhas posteriores.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 2

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | -1 |
| 💰 Receita | R$ 0 mil |
| 🧹 Dívida técnica | 0 |

---

## Flash C — O cadastro com metade dos campos

**Tipo:** Relâmpago · **Voto:** B

**Justificativa:**

O grupo escolheu utilizar o padrão Builder, com valores padrão e validação no método `build()`. A abordagem organiza a construção de objetos com vários atributos e ajuda a impedir que objetos incompletos ou inválidos sejam criados.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 2

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | 0 |
| 💰 Receita | R$ 0 mil |
| 🧹 Dívida técnica | 0 |

---

## Flash D — O teste verde que não testa nada

**Tipo:** Relâmpago · **Voto:** A

**Justificativa:**

O grupo escolheu adicionar uma asserção para verificar o comportamento esperado do teste, como `assertEquals` ou `assertThrows`. Um teste precisa validar efetivamente o resultado ou a exceção esperada, e não apenas executar o código sem verificar o comportamento.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 55 mil · 🧹 1

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | 0 |
| 💰 Receita | R$ 0 mil |
| 🧹 Dívida técnica | -1 |

---

## R6 — O teste vermelho às 03h45

**Tipo:** Rodada · **Voto:** B

**Justificativa:**

O grupo escolheu investigar e corrigir a divergência na tarifa TED, que deveria ser de R$ 5,00, mas estava retornando R$ 50,00. A decisão prioriza o cumprimento do contrato de negócio e a confiabilidade dos testes, em vez de desativar testes ou liberar uma versão com a suíte vermelha.

A correção esperada é ajustar a implementação da tarifa e executar novamente a suíte completa antes da liberação.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 85 mil · 🧹 0

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | -1 |
| 💰 Receita | +R$ 30 mil |
| 🧹 Dívida técnica | -1 |

---

## Flash E — A taxa é 5 ou 50? (05h58)

**Tipo:** Relâmpago · **Situação:** Não aplicável

Este Flash era destinado aos grupos que escolheram A, C ou D na R6 e permaneceram com a suíte de testes comprometida. Como o grupo escolheu a opção B na R6, o evento não foi contabilizado como decisão do grupo.

---

## R7 — Go/No-Go da Black Friday (06h15)

**Tipo:** Rodada · **Voto:** B

**Justificativa:**

O grupo escolheu corrigir os problemas identificados durante a noite e garantir que a suíte de testes estivesse realmente verde antes da abertura do banco. A decisão aceita um atraso de duas horas, com abertura prevista para as 10h, para priorizar a estabilidade do sistema, a integridade das operações e a confiança dos clientes.

**Placar do grupo após esta decisão:** 🔥 9 · 💰 R$ 185 mil · 🧹 -1

| Indicador | Alteração |
|---|---:|
| 🔥 Saúde do banco | +1 |
| 💰 Receita | +R$ 100 mil |
| 🧹 Dívida técnica | -1 |

> **Observação:** a dívida técnica foi calculada literalmente com os efeitos informados nas decisões. O material fornecido não esclarece se esse indicador pode assumir valor negativo; confirmar com o professor.

---

## 🔎 O caminho do MEU grupo

Uma linha por decisão registrada, na ordem em que os eventos ocorreram.

| # | Decisão | Nossa letra | Consequência que ela teria tido |
|---:|---|:---:|---|
| 1 | R1 — O saldo que virou negativo | C | Correção da validação de saldo e inclusão de teste |
| 2 | R2 — A injeção que derreteu o banco | A | Consultas parametrizadas com `PreparedStatement` |
| 3 | Flash B — As conexões se fecham | A | Fechamento automático de recursos JDBC |
| 4 | R3 — A noite das contas gêmeas | A | Correção do Singleton do gerador de contas |
| 5 | R4 — O comprovante que aponta pra pessoa errada | A | Registro correto de pagador e recebedor |
| 6 | R5 — A fábrica que devolveu null | A | Exceção para tipo de conta inválido |
| 7 | Flash C — O cadastro com metade dos campos | B | Builder com valores padrão e validação |
| 8 | Flash D — O teste verde que não testa nada | A | Inclusão de asserção para validar o teste |
| 9 | R6 — O teste vermelho às 03h45 | B | Correção da tarifa TED antes da liberação |
| 10 | R7 — Go/No-Go da Black Friday | B | Correção dos problemas antes da abertura |

**Eventos não aplicáveis:** Flash A e Flash E, conforme as condições de cada evento.

---

# 🏁 EPÍLOGO · AMANHECE A BLACK FRIDAY (07h00)

> O placar final foi congelado conforme os efeitos das decisões registradas pelo grupo. Os perfis representam a situação da equipe ao final da noite, não uma premiação.

## Placar final congelado

| Indicador | Resultado final |
|---|---:|
| 🔥 Saúde do banco | 9 |
| 💰 Receita | R$ 185 mil |
| 🧹 Dívida técnica | -1 |

## Perfil da noite do grupo

### A Noite dos Heróis

**Critério:** 🔥 7 ou mais e 🧹 até 2.

**Como amanhece o banco:** banco abriu, clientes confiam, time dorme (quase) em paz.

**Justificativa do enquadramento:** o grupo terminou com saúde do banco igual a 9 e dívida técnica calculada em -1. Esses valores atendem aos critérios apresentados para o perfil A Noite dos Heróis.

## Perfis adicionais

| Perfil | Critério | Resultado do grupo |
|---|---|---|
| O Preço da Pressa | 💰 400 ou mais | Não se aplica: receita de R$ 185 mil |
| Firefighters Crônicos | 🧹 6 ou mais | Não se aplica: dívida técnica calculada em -1 |

### Conclusão do epílogo

O grupo priorizou a integridade financeira, a segurança das consultas, o registro correto das transferências e a validação do sistema por testes. Na decisão final, escolheu corrigir os problemas antes da abertura, aceitando o atraso de duas horas para evitar uma liberação sem a validação necessária.

**Ponto pendente:** confirmar com o professor se a dívida técnica pode assumir valor negativo. Até essa confirmação, o valor permanece registrado conforme o cálculo literal dos efeitos das decisões.

---

# 📋 PÓS-MORTEM · relatório de incidente

> Rascunho em aula e commit final `pos-mortem:` até 23h59 do dia da 3ª aula.

## 1. Linha do tempo da madrugada

| Horário | Incidente | Decisão tomada | Consequência observada |
|---|---|---|---|
| A preencher em sala | A preencher | A preencher | A preencher |
| A preencher em sala | A preencher | A preencher | A preencher |
| A preencher em sala | A preencher | A preencher | A preencher |

## 2. Causa-raiz de 2 incidentes (aula + mecanismo técnico)

**Incidente 1:** _______________________________________________

**Aula/mecanismo:**

A preencher em sala com base no incidente apresentado pelo professor.

**Causa-raiz:** a preencher.

**Correção ou decisão tomada:** a preencher.

**Incidente 2:** _______________________________________________

**Aula/mecanismo:**

A preencher em sala com base no incidente apresentado pelo professor.

**Causa-raiz:** a preencher.

**Correção ou decisão tomada:** a preencher.

## 3. O que faríamos diferente (2 rodadas + por quê)

**Decisão 1:** a preencher.

**O que mudaríamos e por quê:**

A preencher em sala, considerando o mecanismo técnico e o trade-off envolvido.

**Decisão 2:** a preencher.

**O que mudaríamos e por quê:**

A preencher em sala, considerando o mecanismo técnico e o trade-off envolvido.

## 4. A maior lição da equipe

A preencher após a discussão em sala.

A reflexão deverá considerar o que a equipe aprendeu sobre segurança, integridade financeira, testes, dívida técnica, pressão de tempo e tomada de decisões em produção.

