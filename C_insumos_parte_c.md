# C_insumos_parte_c.md — Insumos da Parte C (derivados do Mapa de Atores)

**Origem:** `C_mapa_atores.md` (abordagem funcional, dois perímetros, RTDI).
**Finalidade:** insumos para a proposta de melhoria de processo — o **"Gatilho de Entrada Homologado"** — e para a especificação do motor de cálculo da ajuda de custo.
**Data:** 2026-06-05 · **Reconciliado com `ACT 2025-2027.pdf` (Cláusula Décima) em 2026-06-05.**
**Disciplina de redação (RTDI):** todo vazio de evidência aparece como placeholder; toda regra traz status `[ACT]` / `[HIPÓTESE]` / `[DECISÃO DE IMPL.]` / `[A CONFIRMAR]`. Nenhum sistema ou órgão é nomeado sem fonte.

---

## 1. Jornada As-Is (estado atual)

> ⚠️ **Status do diagnóstico: `[HIPÓTESE a validar]`.** A descrição de "preenchimento manual / auditoria linha a linha / vigências fragmentadas" **não foi comprovada documentalmente** nesta sessão — a planilha/imagem citada nunca foi localizada na pasta. O As-Is abaixo é, portanto, uma **hipótese de trabalho**, não um fato; deve ser confirmado por análise documental do formulário real ou por entrevista com o NUPAG antes de fundamentar a recomendação.

1. `[ATO_FORMAL_DESIGNACAO_ORIGEM]` formaliza a designação do executor (gestor/fiscal/substituto). `[A CONFIRMAR — plataforma e autoridade signatária]`
2. A função **Origem de Parâmetros Contratuais (OPC)** detém valor, classificação obra×serviço, vigências e aditivos — hoje **não entregues de forma estruturada** ao RH. `[HIPÓTESE]`
3. O **Executor (EXE)** protocola requerimento e, em aditivo/renovação, solicita continuidade em ≤30 dias. `[ACT]`
4. **NUPAG/GEPAG (NUP)** recebe os dados de forma reativa e fragmentada e **audita manualmente** carência, proporcionalidade, gatilho de R$ 650 mil e corte do teto. `[HIPÓTESE — é a dor a comprovar]`

**Vulnerabilidade central (derivada do mapa §5):** descentralização regulatória — carência e teto dependem de comunicações do EXE e de checagens manuais em NUP sobre dados não estruturados de OPC, sem conciliação com SUP/GOV.

---

## 2. Jornada To-Be — "Gatilho de Entrada Homologado"

Objetivo: mover a captura dos metadados para a **origem** (OPC), em campos estruturados, e automatizar o cálculo — eliminando a auditoria braçal **se** a dor do As-Is se confirmar.

1. **Entrada estruturada na origem.** OPC registra em `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` os campos do dicionário (§3) no momento da assinatura — não em texto livre. `[DECISÃO DE IMPL.]`
2. **Consumo limpo pelo RH.** O motor de cálculo lê os campos via API/barramento de `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]`, sem leitura manual de documentos. `[DECISÃO DE IMPL. — arquitetura a homologar]`
3. **Cálculo determinístico.** O motor aplica as regras de §4 (carência, proporcionalidade, aditivos, teto). `[ACT + DECISÃO DE IMPL.]`
4. **Trilha de exceções homologadas.** Casos sem regra fechada no ACT (ex.: +5% por aditivo de valor que cruza R$ 650 mil — B-6) seguem para parecer do Jurídico (SUP) e homologação pela autoridade competente da folha `[A CONFIRMAR]`. *Substituto em atraso deixou de ser exceção — o §15 fecha a regra (sem retroativo).* `[DECISÃO DE IMPL.]`
5. **Conciliação e trilha de auditoria.** Saída concilia com SUP (contábil/financeiro) e fica disponível a GOV/EXT. `[FUNCIONAL]`

---

## 3. Dicionário de dados (campos estruturados a capturar na origem)

Derivado integralmente das regras de negócio. Fonte de cada campo marcada conforme RTDI.

| Campo | Tipo | Fonte | Status |
|---|---|---|---|
| `id_contrato` (chave primária única) | string | `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` | DECISÃO DE IMPL. |
| `classificacao` (obra \| serviço) | enum | `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` | ACT (define qual limite mínimo aplica) |
| `valor_contrato` | decimal (R$) | `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` | ACT (insumo das travas) |
| `data_inicio_vigencia` | date | `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` | ACT |
| `data_fim_vigencia` | date | `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` | ACT |
| `aditivos[]` → `{tipo: prazo\|valor, nova_data_fim?, novo_valor?, data_inicio_vigencia_aditivo}` | array | `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` | DECISÃO DE IMPL. (modelagem aditivo prazo/valor) |
| `id_empregado` | string | `[ATO_FORMAL_DESIGNACAO_ORIGEM]` | ACT |
| `papel` (gestor \| fiscal \| substituto) | enum | `[ATO_FORMAL_DESIGNACAO_ORIGEM]` | ACT §17 (segregação); §16 admite múltiplos por contrato |
| `data_designacao` | date | `[ATO_FORMAL_DESIGNACAO_ORIGEM]` = Portaria (assina o Diretor da área, §5) | ACT §5 |
| `afastamentos[]` → `{inicio, fim}` | array | empregado comunica ao NUPAG/GEPAG (§13); sistema-fonte `[A CONFIRMAR]` | ACT §13, §14 / fonte A CONFIRMAR |
| `data_requerimento` | date | EXE / `[ATO_FORMAL_DESIGNACAO_ORIGEM]` | ACT |
| `fg_01_vigente` | decimal (R$ 5.684,88) | parâmetro RH | ACT |

---

## 4. Especificação do motor de cálculo (regras determinísticas)

Reconciliado com a Cláusula Décima integral. **Ordem de operações:** elegibilidade de objeto → elegibilidade de valor → carência → valor por contrato → proporcionalidade → soma → corte do teto.

1. **Elegibilidade do objeto + segregação.** *Objeto (§1):* só contratos de **obras, serviços continuados ou projetos** com responsabilidade executiva direta. *Excluir (§2):* contratos de adesão (água/esgoto/energia/internet/link/previdência/consignados), grupos de trabalho, comissões, concessão de uso sem obrigações acessórias, termos de cooperação/compromisso/referência e congêneres sem repasse de recursos. *Excluir (§3):* designação só para acompanhar tarefas internas de contrato em que o empregado já seja fiscal/gestor do principal. *Segregação (§17):* vedado gestor+fiscal no mesmo `id_contrato` (uma função por contrato). `[ACT §1, §2, §3, §17]`
2. **Trava de valor mínimo.** `valor_contrato ≥` limite de dispensa de licitação do **RILC** da TERRACAP (§1); valores de referência: R$ 152.926,33 (obra) / R$ 68.154,40 (serviço), conforme `classificacao`. `[ACT §1 → RILC]`
3. **Carência (B-7 RESOLVIDO — interpretação (i)).** Devida **por contrato, exclusivamente a partir do 4º contrato/convênio distinto** (ordem de designação); os 3 primeiros são carência **permanente** (R$ 0), **sem destravamento retroativo**. Para N contratos distintos elegíveis: N<4 → R$ 0; N≥4 → pagam os contratos nas posições 4…N. `[ACT — Cláusula Décima §4, §8, §10]`
4. **Valor por contrato.** Cada contrato pago (4º em diante) = 5% da FG-01 = R$ 284,24 (§8, *"por contrato"*); **+5%** (R$ 284,24) para o contrato que enseja a 4ª/posterior designação **cujo valor > R$ 650.000,00** (§9). `[ACT — §8, §9]`
5. **Proporcionalidade.** Quando a execução no mês for inferior a 30 dias, paga-se proporcionalmente aos dias trabalhados (§12); `valor_diario = valor_por_contrato / 30` (base 30 implícita em *"inferior a 30 dias"*); soma dos dias efetivos, expurgando afastamento do titular (§14) e vacância. `[ACT §12, §14 + DECISÃO DE IMPL. (forma de contagem)]`
6. **Aditivo / renovação.** *Renovação (§10):* novo requerimento de continuidade em até 30 dias da assinatura do aditivo; passados 30 dias, a continuidade conta só a partir do novo requerimento. *Aditivo de valor:* recálculo da trava de R$ 650 mil a partir de `data_inicio_vigencia_aditivo` — o ACT **não** trata expressamente o cruzamento de R$ 650 mil por aditivo (§9 fala do *contrato que enseja a designação*), logo permanece interpretação. `[ACT §10 + DECISÃO DE IMPL./interpretação (aditivo de valor)]`
7. **Teto.** `total_mensal_empregado = min(Σ contratos, R$ 3.410,93)`; excedente cortado (§8). `[ACT §8]`
8. **Substituto (§14–§15).** Durante afastamento legal do titular, só o substituto designado recebe, mediante requerimento e comprovação (§14). O substituto deve requerer **no mês da substituição**; **não há ajuda retroativa sem requerimento no período correspondente** (§15). Regra determinística — sem fila de homologação inventada. `[ACT §14, §15]`

---

## 5. Responsabilidades no To-Be (extraído da RACI)

| Atividade | R/A | Apoio |
|---|---|---|
| Cadastrar metadados estruturados na origem | OPC | NUP (define schema) |
| Protocolar requerimento / renovação ≤30 dias | EXE | OPC |
| Executar motor de cálculo (regras §4) | NUP | SUP (jurídico em controvérsias) |
| Homologar folha | ISP `[A CONFIRMAR]` | NUP, SUP |
| Conciliar e liberar financeiro | SUP | NUP |
| Monitorar conformidade / trilha de auditoria | GOV | EXT (controle externo) |

---

## 6. Matriz de risco (ancorada nos atores)

| Risco | Causa (ator/etapa) | Efeito | Mitigação no To-Be |
|---|---|---|---|
| Pagamento acima do teto | Checagem manual em NUP sobre dados fragmentados de OPC | Glosa, TCE perante EXT (TCDF) | Corte automático (§4.7) com dado estruturado |
| Subpagamento em aditivo de valor | Modelo As-Is ignora aditivo de valor | Passivo trabalhista cobrado por COL | Reprocessamento §4.6 |
| Pagamento na carência (1º–3º) | Confusão carência×teto (erro corrigido) | Pagamento indevido | Trava §4.3 |
| Pagamento em afastamento (titular) | `afastamentos[]` não capturado | Indébito (ACT §14) | Campo obrigatório no dicionário; glosa automática (§14) — fonte de frequência **`[A CONFIRMAR]`** |

---

## 7. Backlog de validação (o que precisa ser resolvido antes de virar código)

**A. Placeholders a preencher (pesquisa documental/entrevista):**
- A-1 `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` — o ACT cita o **RILC** (regulamento, não sistema); o sistema que cadastra contratos/valores/aditivos **continua não nomeado**. `[A CONFIRMAR]`
- A-2 `[ATO_FORMAL_DESIGNACAO_ORIGEM]` — **autoridade signatária RESOLVIDA:** Portaria assinada pelo **Diretor da área responsável pelo contrato** (§5). Resta a **plataforma/sistema** de emissão. `[parcialmente resolvido]`
- A-3 Autoridade que **homologa a folha** — a Cláusula Décima não a nomeia (≠ assinatura da designação, §5). `[A CONFIRMAR]`
- A-4 Sistema/unidade que consolida **afastamento/frequência** — o empregado comunica ao NUPAG/GEPAG (§13), mas a fonte de dados não é nomeada. `[A CONFIRMAR]`

**B. Decisões/interpretações:**
- B-5 **Alinhado ao ACT:** a base de 30 dias decorre do §12 (*"inferior a 30 dias"*); a forma exata de contagem permanece `DECISÃO DE IMPL.`
- B-6 **Renovação RESOLVIDA (§10):** novo requerimento em ≤30 dias do aditivo; após 30 dias, continuidade só do novo requerimento. O **+5% por aditivo de valor** que cruze R$ 650 mil **não** é tratado expressamente (§9 fala do contrato que enseja a designação) → permanece **interpretação a homologar**.
- B-7 **RESOLVIDO** (com base no `ACT 2025-2027.pdf`, Cláusula Décima): vence a **interpretação (i)** — paga-se **por contrato, a partir do 4º** (§4 e §8: *"exclusivamente, apenas a partir do quarto contrato"*; §10: *"por cada contrato"*); os três primeiros são carência permanente, **sem destravamento retroativo**; ordenação por **sequência de designação** (§9). Refletido em §4.3 e §4.4.
- B-8 **RESOLVIDO (§14–§15):** sem ajuda retroativa ao substituto sem requerimento no período correspondente; não há "decadência" inventada nem fila de homologação. Regra determinística.

**C. Hipótese a comprovar antes da recomendação:**
- C-9 O diagnóstico de "processo manual / fragmentado" agora **tem fonte localizável**: `Planilha executor de contrato.xlsx` existe (pasta do OneDrive do mestrado), mas **ainda não foi inspecionada nem está nos autos do repo**. Até a inspeção, a recomendação do To-Be permanece **condicional** ("*se* o As-Is for manual, *então*..."). *(Posso inspecioná-la mediante seu OK.)*
