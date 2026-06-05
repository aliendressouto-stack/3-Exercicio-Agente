# C_insumos_parte_c.md — Insumos da Parte C (derivados do Mapa de Atores)

**Origem:** `C_mapa_atores.md` (abordagem funcional, dois perímetros, RTDI).
**Finalidade:** insumos para a proposta de melhoria de processo — o **"Gatilho de Entrada Homologado"** — e para a especificação do motor de cálculo da ajuda de custo.
**Data:** 2026-06-05
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

1. **Entrada estruturada na origem.** OPC registra em `[SISTEMA_ORIGEM_DADOS_CONTRATOAIS]` os campos do dicionário (§3) no momento da assinatura — não em texto livre. `[DECISÃO DE IMPL.]`
2. **Consumo limpo pelo RH.** O motor de cálculo lê os campos via API/barramento de `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]`, sem leitura manual de documentos. `[DECISÃO DE IMPL. — arquitetura a homologar]`
3. **Cálculo determinístico.** O motor aplica as regras de §4 (carência, proporcionalidade, aditivos, teto). `[ACT + DECISÃO DE IMPL.]`
4. **Trilha de exceções homologadas.** Casos sem regra fechada (ex.: substituto em atraso) entram em fila de homologação da `[INSTÂNCIA_ADMINISTRATIVA_COMPETENTE_A_CONFIRMAR]`, com pagamento retroativo após aprovação. `[DECISÃO DE IMPL.]`
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
| `papel` (gestor \| fiscal \| substituto) | enum | `[ATO_FORMAL_DESIGNACAO_ORIGEM]` | ACT (trava de segregação) |
| `data_designacao` | date | `[ATO_FORMAL_DESIGNACAO_ORIGEM]` | ACT |
| `afastamentos[]` → `{inicio, fim}` | array | `[A CONFIRMAR — unidade/sistema de frequência]` | A CONFIRMAR |
| `data_requerimento` | date | EXE / `[ATO_FORMAL_DESIGNACAO_ORIGEM]` | ACT |
| `fg_01_vigente` | decimal (R$ 5.684,88) | parâmetro RH | ACT |

---

## 4. Especificação do motor de cálculo (regras determinísticas)

Reproduz o consolidado do mapa §4. **Ordem de operações:** elegibilidade → valor por contrato → proporcionalidade → soma → corte do teto.

1. **Segregação.** Rejeitar empregado designado como gestor **e** fiscal no mesmo `id_contrato`. `[ACT]`
2. **Trava de valor mínimo.** Contrato elegível se `valor_contrato ≥` R$ 152.926,33 (obra) ou R$ 68.154,40 (serviço), conforme `classificacao`. `[ACT]`
3. **Carência.** Benefício só a partir do **4º contrato/convênio distinto** elegível; contratos 1–3 = carência (R$ 0). `[ACT]` — *ver ambiguidade B-7 no backlog: "a partir do 4º" = paga só do 4º em diante, ou destrava todo o conjunto?*
4. **Valor por contrato.** 5% da FG-01 = R$ 284,24; **+5%** (R$ 284,24) se `valor_contrato > ` R$ 650.000,00. `[ACT]`
5. **Proporcionalidade.** Mês comercial de 30 dias; `valor_diario = valor_por_contrato / 30`; soma dos dias efetivos no mês, expurgando afastamentos/vacância. `[ACT + DECISÃO DE IMPL. (denominador 30)]`
6. **Aditivo de valor.** Recalcula trava de R$ 650 mil a partir de `data_inicio_vigencia_aditivo` (incidência ou corte do +5% proporcional no mês da virada). `[DECISÃO DE IMPL.]`
7. **Teto.** `total_mensal_empregado = min(Σ contratos, R$ 3.410,93)`; excedente cortado. `[ACT]`
8. **Substituto em atraso.** Requerimento fora do mês → reter + fila de homologação → pagar retroativo se aprovado (sem confisco). `[DECISÃO DE IMPL.]`

---

## 5. Responsabilidades no To-Be (extraído da RACI)

| Atividade | R/A | Apoio |
|---|---|---|
| Cadastrar metadados estruturados na origem | OPC | NUP (define schema) |
| Protocolar requerimento / renovação ≤30 dias | EXE | OPC |
| Executar motor de cálculo e fila de exceções | NUP | SUP (jurídico em controvérsias) |
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
| Pagamento em afastamento | `afastamentos[]` não capturado | Indébito | Campo obrigatório (§3) — **`[A CONFIRMAR]` a fonte** |

---

## 7. Backlog de validação (o que precisa ser resolvido antes de virar código)

**A. Placeholders a preencher (pesquisa documental/entrevista):**
- A-1 `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` — nome/existência do sistema de cadastro de contratos.
- A-2 `[ATO_FORMAL_DESIGNACAO_ORIGEM]` — plataforma e **autoridade signatária** da designação.
- A-3 `[INSTÂNCIA_ADMINISTRATIVA_COMPETENTE_A_CONFIRMAR]` — quem homologa folha e exceções.
- A-4 Unidade/sistema que detém os dados de **afastamento/frequência**.

**B. Decisões que exigem homologação jurídica:**
- B-5 Denominador "mês comercial de 30 dias" (vs. dias corridos).
- B-6 Tratamento do aditivo de valor (data de incidência do +5%).
- B-7 **Ambiguidade normativa nova (descoberta ao especificar o motor):** "devido a partir do 4º contrato" significa (i) pagar **apenas** os contratos do 4º em diante, ou (ii) o 4º contrato **destrava o conjunto** e passa-se a pagar todos os contratos elegíveis? O ACT resumido não decide. **Não escolher sem parecer** — o resultado financeiro difere materialmente.
- B-8 Sanção do substituto em atraso (regra default proposta, sem base normativa explícita).

**C. Hipótese a comprovar antes da recomendação:**
- C-9 O diagnóstico de "processo manual / fragmentado" (§1) — confirmar com o formulário real ou entrevista; **enquanto não comprovado, a recomendação do To-Be é condicional** ("*se* o As-Is for manual, *então*...").
