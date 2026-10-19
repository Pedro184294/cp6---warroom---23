# FICHA DE DECISÕES · War Room FiapBank (CP6 · 3 aulas)

> Este arquivo é o **README.md do repositório do grupo** (`cp6-warroom-<nome-do-grupo>`).
> Vale **5,0 pontos** (rodadas 0,5 · relâmpagos 0,3), e a nota é pela
> **justificativa**, não pela letra. Preencham após cada aula e commitem até
> **23h59 do mesmo dia** (regras completas na seção 5 do enunciado).
>
> **Os incidentes da madrugada são revelados só em aula.** O título de cada registro
> será **ditado pelo professor na hora**; ninguém se antecipe.

**Grupo (nome da equipe plantonista):** Grupo 23

**Turma:** 2CCPG

**Repo:** `cp6---warroom---23`

**Link:** https://github.com/Pedro184294/cp6---warroom---23

**Integrantes (nome + RM):**

| Nome | RM |
|---|---|
| Pedro Luis Tofoli | 564441 |
| Fabricio Cardoso de Oliveira | 561827 |
| Vinicius Barbosa Gomes | 564854 |
| Leonardo Luster Gomes | 564448 |
| Nelson Troccoli Santos Neto | 562815 |
| Raphael Talarico Nascimento Silva | 565219 |

---

## 0. Setup do repositório (antes da 1ª aula; podem apagar esta seção depois)

1. Repositório público criado no GitHub: `cp6---warroom---23`.
2. Arquivo `README.md` publicado no repositório.
3. Commit inicial realizado com a mensagem `chore: ficha em branco do grupo`.
4. Link do repositório para compartilhar no Teams:

   https://github.com/Pedro184294/cp6---warroom---23

### Convenção de commits

**Um commit por rodada; relâmpagos podem ir junto com a rodada seguinte.**

```text
decisao: R1 - opcao C (corrige saldo e adiciona teste)
decisao: R2 - opcao A (resumo da justificativa em uma frase)
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

> A cada incidente, o professor dita o título. Copiem o modelo abaixo e preencham
> com o rascunho feito em aula, junto com o placar do grupo após a consequência.
> Commitem 1 vez por rodada até 23h59 do dia.
>
> **Eventos relâmpago:** registrem apenas se o grupo for **afetado** (o professor
> chama quem for; não ser chamado é bom sinal).

### RODADA 1 — O saldo que virou negativo (19h12)

**Tipo:** rodada · **Voto:** C

**Justificativa:**

Escolhemos corrigir a validação de saldo e escrever um teste automatizado com `assertThrows` antes de subir a correção. O teste deve garantir que transferências sem saldo suficiente sejam rejeitadas, impedindo que o débito continue após a exceção. A solução consome cerca de 40 minutos, mas melhora a confiabilidade e reduz a dívida técnica.

**Placar do grupo após esta decisão:** 🔥 8 · 💰 R$ 35 mil · 🧹 1

---

### Próximas decisões

> Preencher somente quando os incidentes forem apresentados pelo professor e o grupo tiver tomado sua decisão. Para cada registro, usem o modelo abaixo.

```markdown
## <título ditado pelo professor>

**Tipo:** ( rodada / relâmpago ) · **Voto:** ( A / B / C / D )

**Justificativa:**

<2 a 3 linhas: mecanismo técnico + trade-off>

**Placar do grupo após esta decisão:** 🔥 __ · 💰 R$ __ mil · 🧹 __
```

---

## 🔎 O caminho do MEU grupo (preencher na 3ª aula, quando o mapa for revelado)

Uma linha por decisão registrada acima (usem os títulos ditados em aula):

| # | Decisão | Nossa letra | Consequência que ELA teria tido |
|---|---|---|---|
| 1 | R1 — O saldo que virou negativo | C | Corrigir a validação do saldo e adicionar teste; +1 reputação, +R$ 35 mil de prejuízo e -1 dívida técnica. |
| | | | |
| | | | |
| | | | |

*(adicionem linhas conforme as decisões da madrugada)*

---

# 📋 PÓS-MORTEM · relatório de incidente (montar em sala na 3ª aula)

> Rascunho em aula e commit final `pos-mortem: relatorio de incidente da madrugada` até 23h59 do dia da 3ª aula.

## 1. Linha do tempo da madrugada

_______________________________________________________________________________________

_______________________________________________________________________________________

_______________________________________________________________________________________

## 2. Causa raiz de 2 incidentes (aula + mecanismo técnico)

**Incidente 1:** _______________________________________________

**Aula/mecanismo:**

_______________________________________________________________________________________

**Incidente 2:** _______________________________________________

**Aula/mecanismo:**

_______________________________________________________________________________________

## 3. O que faríamos diferente (2 rodadas + por quê)

_______________________________________________________________________________________

_______________________________________________________________________________________

## 4. A maior lição da equipe

_______________________________________________________________________________________
