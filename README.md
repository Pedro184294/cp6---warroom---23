# FICHA DE DECISÕES · War Room FiapBank (CP6 · 3 aulas)

## Identificação do grupo

- **Grupo:** 23
- **Turma:** 2CCPG
- **Repositório:** [cp6---warroom---23](https://github.com/Pedro184294/cp6---warroom---23)

### Integrantes

| Nome completo | RM |
|---|---|
| Pedro Luis Tofoli | 564441 |
| Fabricio Cardoso de Oliveira | 561827 |
| Vinicius Barbosa Gomes | 564854 |
| Leonardo Luster Gomes | 564448 |
| Nelson Troccoli Santos Neto | 562815 |
| Raphael Talarico Nascimento Silva | 565219 |

---

## 1. Configuração inicial — antes da primeira aula

- [ ] Criar o repositório público `cp6---warroom---23`.
- [ ] Colocar esta ficha no arquivo `README.md`.
- [ ] Fazer o primeiro commit com a mensagem exigida pelo professor.
- [ ] Enviar o link do repositório no Teams.

**Link do repositório:**  
https://github.com/Pedro184294/cp6---warroom---23

### Convenção de commits

Cada rodada deve ser registrada em um commit, seguindo o padrão:

```text
decisao: R1 - opcao C (resumo da justificativa em uma frase)
decisao: R2 - opcao A (resumo da justificativa em uma frase)
pos-mortem: relatorio de incidente da madrugada
```

A letra e a justificativa devem corresponder à decisão realmente tomada pelo grupo.

---

## 2. Dossiê técnico do FiapBank

Este dossiê apresenta as regras e restrições técnicas que devem orientar as decisões durante a War Room.

### Tecnologias utilizadas

- Java 17
- Spring Boot
- Spring Data JPA
- Oracle Database

### Endpoints da API

- `/api/contas`
- `/api/transferencias`

### Regras de negócio e requisitos técnicos

1. **PIX:** a taxa de transferência é de R$ 0.
2. **TED:** a taxa de transferência é fixa em R$ 5.
3. **Saldo:** uma transferência ou um saque sem saldo suficiente deve ser rejeitado com uma mensagem de erro clara. O saldo da conta nunca pode ficar negativo.
4. **Numeração de contas:** os números devem ser únicos e sequenciais, começando por 1001, 1002, 1003 e assim por diante.
5. **Extrato:** as transferências devem registrar corretamente quem pagou e quem recebeu.
6. **CPF:** é um dado sensível e nunca deve aparecer nas respostas da API.
7. **Banco de dados:** as consultas devem utilizar parâmetros, evitando SQL Injection. As conexões e os recursos utilizados devem ser liberados corretamente.
8. **Testes:** a suíte de testes deve ser executada antes de cada implantação, e todos os testes precisam passar.

### Como justificar uma decisão

Cada justificativa deve apresentar:

- **Mecanismo técnico:** o que será alterado ou utilizado para resolver o problema.
- **Trade-off:** qual é a vantagem e qual é o custo, risco ou consequência da decisão.
- **Impacto:** como a escolha afeta segurança, reputação, prejuízo financeiro ou dívida técnica.

---

## 3. Registro das decisões

**Placar inicial do grupo:** 🔥 7 · 💰 R$ 0 mil · 🧹 2

> Preencher cada seção durante a aula, de acordo com o incidente apresentado pelo professor, a alternativa votada e as consequências anunciadas.

### R1 — O saldo que virou negativo

**Tipo:** Rodada  
**Voto do grupo:** ______

**Justificativa:**

<!-- Escrever de 2 a 3 linhas explicando o mecanismo técnico e o trade-off da escolha. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### Flash A — A busca que não acha ninguém

**Participação:** somente para grupos que escolheram a alternativa D na R1.

**Tipo:** Relâmpago  
**O grupo foi afetado?** ______  
**Voto do grupo, se aplicável:** ______

**Justificativa:**

<!-- Preencher somente se o grupo participar deste evento. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### R2 — A injeção que derreteu o banco

**Tipo:** Rodada  
**Voto do grupo:** ______

**Justificativa:**

<!-- Escrever de 2 a 3 linhas explicando o mecanismo técnico e o trade-off da escolha. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### Flash B — As conexões se fecham

**Participação:** somente para grupos que escolheram a alternativa A na R2.

**Tipo:** Relâmpago  
**O grupo foi afetado?** ______  
**Voto do grupo, se aplicável:** ______

**Justificativa:**

<!-- Preencher somente se o grupo participar deste evento. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### R3 — A noite das contas gêmeas

**Tipo:** Rodada  
**Voto do grupo:** ______

**Justificativa:**

<!-- Escrever de 2 a 3 linhas explicando o mecanismo técnico e o trade-off da escolha. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### R4 — A preencher durante a segunda aula

**Tipo:** Rodada  
**Título do incidente conforme o professor:** ______  
**Voto do grupo:** ______

**Justificativa:**

<!-- Escrever de 2 a 3 linhas com o mecanismo técnico e o trade-off. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### R5 — A preencher durante a segunda aula

**Tipo:** Rodada  
**Título do incidente conforme o professor:** ______  
**Voto do grupo:** ______

**Justificativa:**

<!-- Escrever de 2 a 3 linhas com o mecanismo técnico e o trade-off. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### Flash C — A preencher durante a segunda aula

**Tipo:** Relâmpago  
**Título do evento conforme o professor:** ______  
**O grupo foi afetado?** ______  
**Voto do grupo, se aplicável:** ______

**Justificativa:**

<!-- Preencher de acordo com a participação e a decisão do grupo. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### Flash D — A preencher durante a segunda aula

**Tipo:** Relâmpago  
**Título do evento conforme o professor:** ______  
**O grupo foi afetado?** ______  
**Voto do grupo, se aplicável:** ______

**Justificativa:**

<!-- Preencher de acordo com a participação e a decisão do grupo. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### R6 — A preencher durante a segunda aula

**Tipo:** Rodada  
**Título do incidente conforme o professor:** ______  
**Voto do grupo:** ______

**Justificativa:**

<!-- Escrever de 2 a 3 linhas com o mecanismo técnico e o trade-off. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### Flash E — A preencher durante a terceira aula, se aplicável

**Tipo:** Relâmpago  
**Título do evento conforme o professor:** ______  
**O grupo foi afetado?** ______  
**Voto do grupo, se aplicável:** ______

**Justificativa:**

<!-- Preencher de acordo com a participação e a decisão do grupo. -->

**Placar do grupo após esta decisão:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

### R7 — A preencher durante a terceira aula

**Tipo:** Rodada  
**Título do incidente conforme o professor:** ______  
**Voto do grupo:** ______

**Justificativa:**

<!-- Escrever de 2 a 3 linhas com o mecanismo técnico e o trade-off. -->

**Placar final do grupo:** 🔥 ______ · 💰 R$ ______ mil · 🧹 ______

---

## 4. Caminho do grupo

Preencher ao longo das rodadas, registrando as decisões tomadas e suas consequências.

| # | Decisão | Nossa letra | Consequência que ela teria tido |
|---|---|---|---|
| 1 | R1 — O saldo que virou negativo | ___ | ___ |
| 2 | Flash A — A busca que não acha ninguém | ___ | ___ |
| 3 | R2 — A injeção que derreteu o banco | ___ | ___ |
| 4 | Flash B — As conexões se fecham | ___ | ___ |
| 5 | R3 — A noite das contas gêmeas | ___ | ___ |
| 6 | R4 | ___ | ___ |
| 7 | R5 | ___ | ___ |
| 8 | Flash C | ___ | ___ |
| 9 | Flash D | ___ | ___ |
| 10 | R6 | ___ | ___ |
| 11 | Flash E | ___ | ___ |
| 12 | R7 | ___ | ___ |

---

## 5. Pós-mortem — Relatório de incidente da madrugada

**Preencher durante a terceira aula**, com base nas decisões e nas consequências discutidas em sala.

### 5.1. Linha do tempo da madrugada

<!-- Registrar os principais acontecimentos, as decisões tomadas e as consequências. -->

- **Início:**
- **Principais incidentes:**
- **Decisões críticas:**
- **Desfecho:**

### 5.2. Causa-raiz de dois incidentes

**Incidente 1:**

- **Problema observado:**
- **Causa-raiz:**
- **Mecanismo técnico envolvido:**

**Incidente 2:**

- **Problema observado:**
- **Causa-raiz:**
- **Mecanismo técnico envolvido:**

### 5.3. O que faríamos diferente?

**Rodada 1 — decisão que mudaríamos:**

- **Decisão original:**
- **Nova decisão:**
- **Justificativa técnica:**

**Rodada 2 — decisão que mudaríamos:**

- **Decisão original:**
- **Nova decisão:**
- **Justificativa técnica:**

### 5.4. Maior aprendizado do grupo

<!-- Registrar o principal aprendizado sobre decisões técnicas sob pressão, seus trade-offs e suas consequências. -->

### 5.5. Conclusão

<!-- Escrever uma conclusão breve sobre o que o grupo aprendeu com a War Room e como esse aprendizado pode ser aplicado em projetos reais. -->

---

## 6. Entrega final

- [ ] Decisões registradas ao longo das rodadas.
- [ ] Justificativas técnicas preenchidas.
- [ ] Placar final atualizado.
- [ ] Caminho do grupo preenchido.
- [ ] Pós-mortem concluído na terceira aula.
- [ ] Apresentação final de 2 a 3 minutos preparada.
- [ ] Repositório público atualizado.
- [ ] Link do repositório enviado no Teams.

**Último commit obrigatório:**

```text
pos-mortem: relatorio de incidente da madrugada
```
