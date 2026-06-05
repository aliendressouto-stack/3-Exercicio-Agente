# C_mapa_atores.md — Mapa Final de Atores (Abordagem Funcional)

**Serviço:** Concessão e Pagamento de Ajuda de Custo para Executores de Contrato na Terracap — adicional de 5% da FG-01 por contrato/convênio em gestão, execução ou fiscalização (Cláusula Décima, ACT 2025/2027).
**Base metodológica:** consolidado a partir de `B_relatorio_assistente_v3.md` após a sabatina de 6 rodadas (ver `C_grill_transcript.md`).
**Data:** 2026-06-05

---

## 1. Critério de fronteira (funcional) e os dois perímetros

A sabatina substituiu o critério **organizacional** (autocontraditório) por um critério **funcional**, e identificou que o mapa precisa de **dois perímetros distintos** para não recair na contradição original (quem toca o cálculo × quem tensiona a conformidade ex-post):

- **Perímetro I — Fluxo de Cálculo (critério estrito).** Inclui-se a função que **gera, processa ou certifica dados (numéricos ou fáticos) que servem de base de cálculo ou gatilho de elegibilidade** do benefício.
- **Perímetro II — Governança e Conformidade (critério secundário, explicitamente diferente).** Inclui-se a instância que **monitora, controla ou tensiona a conformidade** do pagamento — antes, durante ou depois — sem operar o cálculo.
- **Exclusão.** Instâncias cujos atos produzem **efeitos econômicos genéricos** para a empresa (atividade-fim de mercado, ex.: comercialização de imóveis). Note que a *mesma* gerência finalística entra no Perímetro I **apenas** quando atua como origem de parâmetros de um contrato de suporte/serviço (cisão funcional — ver Ator 2).

---

## 2. Atores e funções mapeados (8 categorias + 2 fontes-placeholder)

### Perímetro I — Fluxo de Cálculo
1. **Executor de Contrato (EXE)** — Fiscal titular, Gestor titular e Substituto legal (engenheiros, arquitetos, técnicos, comissionados, administrativos). Gera o fato gerador (execução/fiscalização) e protocola o requerimento. *Trava de segregação:* vedado acúmulo gestor+fiscal no mesmo contrato. `[ACT]`
2. **Origem de Parâmetros Contratuais (OPC)** — *função cindida* da Unidade Gestora / Área Demandante (inclusive uma gerência finalística "de outro chapéu"). Fornece valor do contrato, classificação obra×serviço, vigências e aditivos — insumos diretos das travas de R$ 152.926,33 / R$ 68.154,40 e de R$ 650.000,00. `[FUNCIONAL]`
3. **NUPAG / GEPAG (NUP)** — Núcleo e Gerência de Pagamento de Pessoal. Processa o cálculo, aplica carência, proporcionalidade, +5% e o corte do teto. `[ACT/FUNCIONAL]`
4. **Instância Superior de Gestão de Pessoas (ISP)** — nível decisório que homologa a folha. `[A CONFIRMAR — nomenclatura/estrutura não evidenciada]`
5. **Suporte: Jurídico / Contabilidade / Financeiro (SUP)** — pareceres em controvérsias de acumulação, classificação contábil da despesa de pessoal e liberação financeira. `[FUNCIONAL]`

### Perímetro II — Governança e Conformidade
6. **Controle e Fiscalização Interna (GOV)** — Controle Interno, Auditoria Interna, Corregedoria, Ouvidoria e Gestão de Riscos Corporativos. Monitora conformidade da folha (teto, carência, afastamentos) e apura denúncias. `[GOVERNANÇA]`
7. **Atores Coletivos (COL)** — Sindicato e Comissão de Negociação do ACT. Pactuaram a Cláusula Décima e cobram o cumprimento; tensionam a conformidade jurídico-passiva. *Entra pelo Perímetro II — não toca o cálculo.* `[GOVERNANÇA]`
8. **Controle Externo (EXT)** — TCDF e MP de Contas. Fiscalizam legalidade e economicidade da despesa de pessoal da estatal. `[GOVERNANÇA]`

### Fontes de dados (placeholders RTDI — não são atores; são origens de insumo)
- **`[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]`** — banco de cadastro estruturado (datas/valores/aditivos) que o Gatilho de Entrada consome via API/barramento. *Existência e nome a confirmar.*
- **`[ATO_FORMAL_DESIGNACAO_ORIGEM]`** — documento que formaliza a designação e inicia o direito do executor. *Sistema/plataforma a confirmar.*

---

## 3. Matriz RACI

**Legenda:** **R** = Responsável (executa) · **A** = Autoridade/presta contas (1 por linha) · **C** = Consultado · **I** = Informado · `—` = sem papel.
Colunas = atores da Seção 2 (EXE, OPC, NUP, ISP, SUP, GOV, COL, EXT).

| # | Atividade do processo | EXE | OPC | NUP | ISP | SUP | GOV | COL | EXT | Status de evidência |
|---|---|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|---|
| 1 | Formalizar designação / indicar executor (via `[ATO_FORMAL_DESIGNACAO_ORIGEM]`) | I | A/R | I | C¹ | — | — | — | — | A CONFIRMAR (autoridade signatária) |
| 2 | Fornecer parâmetros do contrato (valor, classificação, vigência, aditivos) | I | A/R | C | — | — | — | — | — | FUNCIONAL |
| 3 | Protocolar requerimento (e renovar em ≤30 dias / substituto requerer no mês) | A/R | C | I | — | — | — | — | — | ACT |
| 4 | Triagem e validação documental | I | C | A/R | — | — | — | — | — | **HIPÓTESE a validar** |
| 5 | Calcular benefício: carência, proporcionalidade, +5%, corte do teto | I | C | A/R | I | C² | — | — | — | ACT + DECISÃO DE IMPL. |
| 6 | Homologar a folha de pagamento | — | — | R | A | C | I | — | — | A CONFIRMAR (instância) |
| 7 | Classificar despesa (contábil) e liberar pagamento (financeiro) | I | — | C | I | A/R | I | — | — | FUNCIONAL |
| 8 | Monitorar conformidade / apurar denúncias | — | — | C | I | C | A/R | I | I | GOVERNANÇA |
| 9 | Negociar e cobrar o direito (instrumento ACT) | I | — | — | C | — | I | A/R | — | GOVERNANÇA |
| 10 | Fiscalizar legalidade e economicidade (controle externo) | — | — | I | I | I | C | — | A/R | GOVERNANÇA |

¹ A autoridade que assina o ato de designação **não está evidenciada** — tratada como `[INSTÂNCIA_ADMINISTRATIVA_COMPETENTE_A_CONFIRMAR]`.
² Suporte Jurídico é consultado **apenas em controvérsias** de acumulação/elegibilidade; não participa do cálculo de rotina.

---

## 4. Regras de negócio consolidadas (insumo para o "Gatilho de Entrada Homologado")

Reproduzidas já corrigidas pela sabatina. Cada regra traz seu **status de homologação**.

1. **Carência (piso de elegibilidade).** O 5% da FG-01 (R$ 284,24) só é devido **a partir do 4º contrato/convênio distinto, inclusive**. Contratos 1–3 = carência, sem efeito financeiro. *Não confundir com teto.* `[ACT]`
2. **Teto financeiro (limite superior).** A soma das gratificações do empregado no mês não pode exceder **R$ 3.410,93** (60% da FG-01); o sistema aplica corte automático no excedente. `[ACT]`
3. **Proporcionalidade.** Mês comercial de **30 dias**; `Valor_Diario = (0,05 × FG-01) / 30`. Em mês partido, soma-se os dias efetivos de exercício, expurgando a vacância. `[ACT (regra) + DECISÃO DE IMPL. (denominador 30 fixo)]`
4. **Aditivos.** Chave Primária = nº do contrato original. *Aditivo de prazo* atualiza `Data_Fim`. *Aditivo de valor* atualiza `Valor_Contrato` e **reprocessa** o gatilho de R$ 650.000,00 (+5% passa a incidir, ou é cortado, **a partir da data de início da vigência do Termo Aditivo** — marco único, alinhado às demais datas). `[DECISÃO DE IMPL. — exige parecer jurídico]`
5. **Substituto com requerimento em atraso.** ACT silente sobre sanção → **decisão a homologar**. Comportamento default: reter os dias do mês anterior (bloqueio preventivo), encaminhar à `[INSTÂNCIA_ADMINISTRATIVA_COMPETENTE_A_CONFIRMAR]` e, homologada a justificativa, pagar retroativo na folha seguinte (sem confisco). `[DECISÃO DE IMPL.]`

---

## 5. Matriz de risco amarrada ao mapa

A vulnerabilidade central é a **descentralização regulatória**: carência e teto dependem de comunicações do empregado (EXE) e de checagens em NUP a partir de dados que hoje chegam fragmentados de OPC. Sem conformidade integrada com SUP (conciliação contábil) e GOV (gestão de riscos), eleva-se o risco de pagamento em duplicidade ou acima do teto — expondo a estatal a apontamentos de EXT (TCDF). **Importante:** o diagnóstico de "processo manual / auditoria linha a linha" **permanece hipótese a validar** — a fonte documental (`.xlsx`/`.jpg`) citada na sessão nunca foi localizada na pasta e não pode ser tratada como fato.

---

## 6. Pendências obrigatórias antes de virar código (Parte C)

- Resolver **todo** placeholder (`[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]`, `[ATO_FORMAL_DESIGNACAO_ORIGEM]`, `[INSTÂNCIA_ADMINISTRATIVA_COMPETENTE_A_CONFIRMAR]`) por pesquisa documental/entrevista.
- Submeter toda regra etiquetada `DECISÃO DE IMPL.` a **homologação jurídica** formal.
- Validar empiricamente o diagnóstico de dor operacional (item §5) antes de fundamentar a recomendação de automação.
