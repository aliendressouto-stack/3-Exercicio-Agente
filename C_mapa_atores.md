# C_mapa_atores.md — Mapa Final de Atores (Abordagem Funcional)

**Serviço:** Concessão e Pagamento de Ajuda de Custo para Executores de Contrato na Terracap — adicional de 5% da FG-01 por contrato/convênio em gestão, execução ou fiscalização (Cláusula Décima, ACT 2025/2027).
**Base metodológica:** consolidado a partir de `B_relatorio_assistente_v3.md` após a sabatina de 6 rodadas (ver `C_grill_transcript.md`).
**Data:** 2026-06-05 · **Reconciliado com `ACT 2025-2027.pdf` (Cláusula Décima) em 2026-06-05.**

---

## 1. Critério de fronteira (funcional) e os dois perímetros

A sabatina substituiu o critério **organizacional** (autocontraditório) por um critério **funcional**, e identificou que o mapa precisa de **dois perímetros distintos** para não recair na contradição original (quem toca o cálculo × quem tensiona a conformidade ex-post):

- **Perímetro I — Fluxo de Cálculo (critério estrito).** Inclui-se a função que **gera, processa ou certifica dados (numéricos ou fáticos) que servem de base de cálculo ou gatilho de elegibilidade** do benefício.
- **Perímetro II — Governança e Conformidade (critério secundário, explicitamente diferente).** Inclui-se a instância que **monitora, controla ou tensiona a conformidade** do pagamento — antes, durante ou depois — sem operar o cálculo.
- **Exclusão.** Instâncias cujos atos produzem **efeitos econômicos genéricos** para a empresa (atividade-fim de mercado, ex.: comercialização de imóveis). Note que a *mesma* gerência finalística entra no Perímetro I **apenas** quando atua como origem de parâmetros de um contrato de suporte/serviço (cisão funcional — ver Ator 2).

---

## 2. Atores e funções mapeados (8 categorias + 2 fontes-placeholder)

### Perímetro I — Fluxo de Cálculo
1. **Executor de Contrato (EXE)** — Fiscal titular, Gestor titular e Substituto legal. *Perfil (§6/§7):* preferencialmente TEP de nível superior ou empregado em comissão com vínculo com a Adm. Pública; excepcionalmente EC sem vínculo, em contrato administrativo sem exigência de responsabilidade técnica de nível superior. *Equipes expandidas (§16):* em contratos ≥ R$ 10 mi ou de alta complexidade, o Diretor pode autorizar até **5 fiscais e 2 gestores** (e substitutos). Gera o fato gerador e protocola o requerimento. *Segregação (§17):* vedado gestor+fiscal no mesmo contrato. `[ACT §6, §7, §16, §17]`
2. **Origem de Parâmetros Contratuais (OPC)** — *função cindida* da Unidade Gestora / Área Demandante (inclusive gerência finalística "de outro chapéu"). Fornece tipo de objeto (obras/serviços continuados/projetos — §1), valor, vigências e aditivos — insumos das travas do RILC (§1) e de R$ 650.000,00 (§9). O **Diretor da área responsável pelo contrato assina a Portaria de designação** (§5). `[ACT §1, §5, §9 + FUNCIONAL]`
3. **NUPAG / GEPAG (NUP)** — Núcleo e Gerência de Pagamento de Pessoal. Processa o cálculo, aplica carência, proporcionalidade, +5% e o corte do teto. `[ACT/FUNCIONAL]`
4. **Instância Superior de Gestão de Pessoas (ISP)** — nível decisório que homologa a folha. A Cláusula Décima **não** nomeia a autoridade homologadora da folha (≠ assinatura da designação, que é do Diretor da área, §5). `[A CONFIRMAR — não evidenciado no ACT]`
5. **Suporte: Jurídico / Contabilidade / Financeiro (SUP)** — pareceres em controvérsias de acumulação, classificação contábil da despesa de pessoal e liberação financeira. `[FUNCIONAL]`

### Perímetro II — Governança e Conformidade
6. **Controle e Fiscalização Interna (GOV)** — Controle Interno, Auditoria Interna, Corregedoria, Ouvidoria e Gestão de Riscos Corporativos. Monitora conformidade da folha (teto, carência, afastamentos) e apura denúncias. `[GOVERNANÇA]`
7. **Atores Coletivos (COL)** — Sindicato e Comissão de Negociação do ACT. Pactuaram a Cláusula Décima e cobram o cumprimento; tensionam a conformidade jurídico-passiva. *Entra pelo Perímetro II — não toca o cálculo.* `[GOVERNANÇA]`
8. **Controle Externo (EXT)** — TCDF e MP de Contas. Fiscalizam legalidade e economicidade da despesa de pessoal da estatal. `[GOVERNANÇA]`

### Fontes de dados (placeholders RTDI — não são atores; são origens de insumo)
- **`[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]`** — banco de cadastro estruturado (datas/valores/aditivos) que o Gatilho de Entrada consome via API/barramento. *Existência e nome a confirmar.*
- **`[ATO_FORMAL_DESIGNACAO_ORIGEM]`** — a **Portaria de designação assinada pelo Diretor da área responsável** (§5), que inicia o direito do executor. *Resta confirmar o sistema/plataforma de emissão.*

---

## 3. Matriz RACI

**Legenda:** **R** = Responsável (executa) · **A** = Autoridade/presta contas (1 por linha) · **C** = Consultado · **I** = Informado · `—` = sem papel.
Colunas = atores da Seção 2 (EXE, OPC, NUP, ISP, SUP, GOV, COL, EXT).

| # | Atividade do processo | EXE | OPC | NUP | ISP | SUP | GOV | COL | EXT | Status de evidência |
|---|---|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|---|
| 1 | Formalizar designação / indicar executor (Portaria, via `[ATO_FORMAL_DESIGNACAO_ORIGEM]`) | I | A/R¹ | I | — | — | — | — | — | ACT §5 (assina o Diretor da área) |
| 2 | Fornecer parâmetros do contrato (valor, classificação, vigência, aditivos) | I | A/R | C | — | — | — | — | — | FUNCIONAL |
| 3 | Protocolar requerimento (e renovar em ≤30 dias / substituto requerer no mês) | A/R | C | I | — | — | — | — | — | ACT |
| 4 | Triagem e validação documental | I | C | A/R | — | — | — | — | — | **HIPÓTESE a validar** |
| 5 | Calcular benefício: carência, proporcionalidade, +5%, corte do teto | I | C | A/R | I | C² | — | — | — | ACT + DECISÃO DE IMPL. |
| 6 | Homologar a folha de pagamento | — | — | R | A | C | I | — | — | A CONFIRMAR (instância) |
| 7 | Classificar despesa (contábil) e liberar pagamento (financeiro) | I | — | C | I | A/R | I | — | — | FUNCIONAL |
| 8 | Monitorar conformidade / apurar denúncias | — | — | C | I | C | A/R | I | I | GOVERNANÇA |
| 9 | Negociar e cobrar o direito (instrumento ACT) | I | — | — | C | — | I | A/R | — | GOVERNANÇA |
| 10 | Fiscalizar legalidade e economicidade (controle externo) | — | — | I | I | I | C | — | A/R | GOVERNANÇA |

¹ Resolvido pelo ACT §5: a Portaria de designação é **assinada pelo Diretor da área responsável pelo contrato/convênio** (papel exercido pela função OPC).
² Suporte Jurídico é consultado **apenas em controvérsias** de acumulação/elegibilidade; não participa do cálculo de rotina.

---

## 4. Regras de negócio consolidadas (insumo para o "Gatilho de Entrada Homologado")

Reproduzidas já corrigidas pela sabatina. Cada regra traz seu **status de homologação**.

1. **Carência (piso — B-7 resolvido).** 5% da FG-01 (R$ 284,24) devido **por contrato, exclusivamente a partir do 4º contrato/convênio distinto** (ordem de designação); os 3 primeiros = carência **permanente**, **sem destravamento retroativo** do conjunto (§4, §8, §10). *Não confundir com teto.* `[ACT §4, §8, §10]`
2. **Teto financeiro (limite superior).** A soma das gratificações do empregado no mês não pode exceder **R$ 3.410,93** (60% da FG-01); o sistema aplica corte automático no excedente. `[ACT]`
3. **Proporcionalidade.** Quando a execução no mês for inferior a 30 dias, paga-se proporcionalmente aos dias trabalhados (§12); `Valor_Diario = (0,05 × FG-01) / 30` (base 30 implícita no "inferior a 30 dias"); em mês partido soma-se os dias efetivos, expurgando afastamento do titular (§14) e vacância. `[ACT §12, §14 + DECISÃO DE IMPL. (forma de contagem)]`
4. **Aditivos.** Chave Primária = nº do contrato original. *Aditivo de prazo* atualiza `Data_Fim`. *Renovação (§10):* novo requerimento em ≤30 dias da assinatura; após 30 dias, continuidade só a partir do novo requerimento. *Aditivo de valor:* reprocessa o gatilho de R$ 650.000,00 a partir da vigência do aditivo — o ACT não trata o cruzamento por aditivo (§9 fala do contrato que enseja a designação), logo é **interpretação a homologar**. `[ACT §10 + DECISÃO DE IMPL./interpretação]`
5. **Substituto (§14–§15).** Durante afastamento legal do titular, só o substituto designado recebe, mediante requerimento e comprovação (§14); deve requerer **no mês da substituição** — **sem ajuda retroativa sem requerimento no período** (§15). Regra determinística (a "decadência" antes proposta era desnecessária). `[ACT §14, §15]`
6. **Elegibilidade do objeto (§1–§3).** Só geram direito contratos de obras, serviços continuados ou projetos com responsabilidade executiva direta (§1, valor ≥ limite de dispensa do RILC). **Não** geram: contratos de adesão (água/energia/internet…), grupos de trabalho, comissões, termos de cooperação/compromisso/referência sem repasse (§2); nem a designação só para acompanhar tarefas internas de contrato em que já se é fiscal/gestor do principal (§3). `[ACT §1, §2, §3]`

---

## 5. Matriz de risco amarrada ao mapa

A vulnerabilidade central é a **descentralização regulatória**: carência e teto dependem de comunicações do empregado (EXE) e de checagens em NUP a partir de dados que hoje chegam fragmentados de OPC. Sem conformidade integrada com SUP (conciliação contábil) e GOV (gestão de riscos), eleva-se o risco de pagamento em duplicidade ou acima do teto — expondo a estatal a apontamentos de EXT (TCDF). **Importante:** o diagnóstico de "processo manual / auditoria linha a linha" **permanece hipótese a validar** — a fonte (`Planilha executor de contrato.xlsx`) **existe** na pasta do OneDrive do mestrado, mas ainda não foi inspecionada nem trazida aos autos do repo; até lá, não é tratada como fato.

---

## 6. Pendências obrigatórias antes de virar código (Parte C)

- **Placeholders ainda abertos:** `[SISTEMA_ORIGEM_DADOS_CONTRATUAIS]` (sistema de cadastro de contratos — não nomeado no ACT) e a **autoridade homologadora da folha**. *Resolvidos pelo ACT:* assinatura da designação = Diretor da área (§5); carência (B-7); regra do substituto (§14–§15).
- Submeter as regras ainda etiquetadas `DECISÃO DE IMPL./interpretação` (forma de contagem proporcional; +5% por aditivo de valor) a **homologação jurídica** formal.
- Validar empiricamente o diagnóstico de dor operacional (§5) — inspecionar a `Planilha executor de contrato.xlsx` — antes de fundamentar a recomendação de automação.
