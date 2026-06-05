# Relatório de Pesquisa Inicial (v1) — Mapeamento de Atores e Jornada da Ajuda de Custo (Terracap)

Este relatório apresenta uma investigação profunda sobre o ecossistema de atores e a jornada operacional do serviço interno de concessão, validação e pagamento da "Ajuda de Custo para Execução e Acompanhamento de Contratos e/ou Convênios", regulamentado pela Cláusula Décima do Acordo Coletivo de Trabalho (ACT 2025/2027) no âmbito da Companhia Imobiliária de Brasília (Terracap). O processo administrativo caracteriza-se por um alto volume de interações manuais e regras cumulativas rígidas, gerando desafios de conformidade e governança.

## 1. Jornada Detalhada do Serviço
A jornada inicia-se na **Governança**, com a emissão da Portaria de designação pela Diretoria da Área Requisitante ou pela Diretoria Colegiada, publicando o ato no Diário Oficial do DF (DODF). O empregado designado assume o papel na **Linha de Frente**. Para iniciar o recebimento, o trabalhador deve protocolar um requerimento formal via Sistema de Protocolo/Processo Eletrônico (SEI), anexando a portaria e comprovando que o contrato individual atende aos limites mínimos de elegibilidade baseados nos valores de dispensa de licitação (R$ 152.926,33 para obras e R$ 68.154,40 para serviços). 

O processo é encaminhado à **Retaguarda Operacional** (NUPAG/GEPAG). Os analistas realizam a validação documental e a aplicação manual das travas de negócio: verificam a regra de carência (o benefício só é devido a partir do 4º contrato ativo e distinto); calculam o valor de 5% da FG-01 por contrato (R$ 284,24), aplicando o teto mensal estrito de 60% da FG-01 (R$ 3.410,93) por CPF; e checam se há contratos acima de R$ 650.000,00 para injetar o adicional de 5% da FG-01. Na sequência, cruzam-se os dados com o controle de frequência para aplicar a proporcionalidade de dias trabalhados em caso de afastamentos ou substituições de titulares por substitutos eventuais[cite: 1]. Após o cálculo financeiro, a rubrica é inserida manualmente no ERP/Sistema de Folha de Pagamento para processamento e posterior liquidação financeira, finalizando com o arquivamento documental e abrindo espaço para auditorias posteriores.

## 2. Mapeamento Multicamadas de Atores

### Categoria 1 – Linha de Frente (Beneficiários)
*   **Fiscal de Contrato Titular (Engenheiros, Arquitetos, Técnicos):** Responsáveis pela fiscalização técnica direta. Sofrem com o risco de perda do prazo preclusivo de 30 dias para requerer a continuidade do pagamento após termos aditivos ou renovações[cite: 1].
*   **Gestor de Contrato Titular (Empregados Administrativos/Comissionados):** Responsáveis pela gestão documental e financeira. Possuem a restrição legal de segregação de funções, sendo vedada a indicação simultânea como fiscal no mesmo contrato[cite: 1].
*   **Substitutos Eventuais:** Devem protocolar requerimento formal estritamente no mês da substituição para garantir o recebimento proporcional[cite: 1].

### Categoria 2 – Retaguarda Operacional
*   **Núcleo de Pagamento de Pessoal (NUPAG / GEPAG):** Analistas de RH e operadores de folha. Executam a conferência manual das planilhas de tetos, valores mínimos e carências, acumulando alto risco de erro humano e retrabalho por falta de automação.
*   **Chefias Imediatas:** Atores que avaliam os requerimentos iniciais e validam a real atuação dos servidores antes do envio ao RH.

### Categoria 3 – Governança, Tecnologia e Sistemas
*   **Diretorias Colegiadas e Unidades Emissoras:** Autoridades signatárias das portarias de designação. Ditam o ritmo inicial do processo e autorizam comitês expandidos em contratos complexos.
*   **Equipes de TI e Fornecedores de Software (ERP/Folha):** Administradores dos sistemas que processam as rubricas, operando plataformas sem integração nativa com o banco de dados de contratos.

### Categoria 4 – Controle, Fiscalização e Riscos (Atores Ocultos)
*   **Auditoria Interna e Compliance da Terracap:** Avaliam periodicamente amostragens da folha para identificar inconformidades, pagamentos duplicados ou extrapolação do teto de 60% da FG-01[cite: 1].
*   **Tribunal de Contas do Distrito Federal (TCDF) e MP de Contas:** Órgãos externos que fiscalizam a legalidade das despesas de pessoal, aplicando sanções em caso de descumprimento do ACT ou dano ao erário.

### Categoria 5 – Atores Esquecidos (Relevância Justificada)
*   **Setor de Controle de Frequência / Medicina e Segurança:** Crítico para o processo, pois fornece os registros de licenças médicas, férias e afastamentos que exigem o cálculo de proporcionalidade de dias pelo NUPAG[cite: 1].
*   **Setor de Gestão Contratual / Protocolo Central:** Responsável por registrar a rescisão ou encerramento dos contratos principais. Se falharem em comunicar o término, o benefício continua sendo pago indevidamente.
*   **Equipes de Governança de Dados:** Essenciais para desenhar futuras integrações que eliminem as planilhas manuais do RH.

## 3. Matriz de Riscos Operacionais e Sistêmicos
O maior risco identificado reside na **falha de integração tecnológica** entre o sistema de contratos e o ERP da folha de pagamento. A verificação manual da carência do 4º contrato e o monitoramento do teto de R$ 3.410,93 geram probabilidade alta de pagamento indevido ou passivo trabalhista[cite: 1]. Adicionalmente, a dependência de que o empregado comunique tempestivamente alterações contratuais ao NUPAG abre uma vulnerabilidade crítica de conformidade regulatória perante o TCDF[cite: 1].