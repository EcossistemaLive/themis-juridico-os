# ARQUITETURA TÉCNICA E SEGURANÇA
## Themis Jurídico OS · Especificação de Engenharia e Compliance

> **Ecossistema Live · Documento de Arquitetura de Software e Infraestrutura**  
> **Público-Alvo:** CTOs, Tech Leads, Engenheiros de Software e Comitês de Segurança/LGPD de Escritórios

---

## 1. Visão Arquitetural Sistêmica

A **Themis Jurídico OS** adota uma topologia híbrida de **Borda Soberana (Edge Appliance) + Nuvem Serviceless Segura (Cloud Functions & Vector Engine)**. 

```
                                      ESCRITÓRIO DO CLIENTE (EDGE)
  ┌────────────────────────────────────────────────────────────────────────────────────────┐
  │                                                                                        │
  │   [WhatsApp Web] ──> [Playwright Persistent Engine]                                   │
  │                              │                                                         │
  │                              ▼                                                         │
  │                     [Hermes Runtime (s6)]                                              │
  │                        ├── Argos (Vigília Silenciosa)                                  │
  │                        ├── Temis (Concierge / Acolhimento)                             │
  │                        └── Mentor (Técnico Interno)                                    │
  │                              │                                                         │
  │                              ▼                                                         │
  │                     [SQLite Local (themis.db)] <────> [Painel Local / Server Flask]    │
  │                              │                                                         │
  │                              ▼                                                         │
  │                     [Task Scheduler Windows]                                           │
  │                        ├── 07h: Briefing Matinal                                       │
  │                        ├── 12h: Auditoria SLA                                          │
  │                        └── 18h: Fechamento Adversarial                                 │
  └──────────────────────────────┬─────────────────────────────────────────────────────────┘
                                 │ TLS 1.3 / mTLS / HMAC
                                 ▼
  ┌────────────────────────────────────────────────────────────────────────────────────────┐
  │   NUVEM SOBERANA (South America - SP / Firebase & Cloud Functions)                     │
  │                                                                                        │
  │   [Auth Middleware + Zod Validation]                                                   │
  │                  │                                                                     │
  │                  ├── [doc-analyst]: Leitura de PDFs & Cálculo Determinístico Prazos    │
  │                  ├── [petition-drafter]: Plano Silogístico & Redação Streaming         │
  │                  └── [adversarial-review]: Auditoria Pré-Protocolo                     │
  │                  │                                                                     │
  │                  ▼                                                                     │
  │   [Anthropic Claude API Enterprise (Zero Data Retention)]                              │
  └──────────────────────────────┬─────────────────────────────────────────────────────────┘
                                 │ Webhooks / REST API
                                 ▼
  ┌────────────────────────────────────────────────────────────────────────────────────────┐
  │   CAMADA DE GESTÃO DO ESCRITÓRIO                                                       │
  │   [ClickUp Workspace Próprio / LegalOne / Projuris / Advbox]                            │
  └────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Componentes da Borda (Themis Edge Station)

A Estação Themis roda fisicamente ou virtualmente na infraestrutura do escritório do cliente (mini-PC dedicado, desktop Windows 11 Pro ou VM Windows Server), garantindo soberania de dados.

### 2.1 Banco de Dados Local (`themis.db`)
O banco SQLite local gerencia as operações com zero latência e sem dependência de conexão permanente:
- **`demandas`:** Registro de todas as solicitações extraídas pelo Argos, mapeando `grupo_id`, `solicitante_numero`, `legitimidade`, `urgencia` (N0 a N5), `sla_acolhimento_minutos` e status de ciclo de vida.
- **`procedimentos_pecas`:** Gerenciamento do estado da elaboração de peças (`leitura_autos`, `plano_silogistico`, `minutando`, `revisao_adversarial`, `pronta_assinatura`).
- **`fila_envio`:** Portão de saída estrito com proteção anti-bloqueio.
- **`status_estacao`:** Health-check contínuo de conectores e consumo de tokens.

### 2.2 Fila de Envio Anti-Bloqueio (Anti-Ban Envelope)
Para eliminar qualquer risco de bloqueio da linha telefônica do escritório:
1. **Janela de Operação Estrita:** Mensagens ativas somente em dias úteis das 08:00 às 18:00.
2. **Jitter Estocástico Humano:** Delays variáveis entre 30 e 90 segundos entre mensagens.
3. **Simulação de Digitação e Leitura:** O driver do navegador envia sinais de `presence: composing` e marca mensagens como lidas antes da emissão.
4. **Volume Máximo e Aquecimento:** Limite de 100 interações/dia por linha; protocolo de aquecimento de 14 dias para novos chips.
5. **Aprovação Humana (Human-in-the-loop):** Todas as respostas substantivas são geradas como rascunho e aguardam clique de aprovação no ClickUp antes de entrar na fila.

---

## 3. O Motor de Inteligência Nuvem (Themis Core)

### 3.1 Prazos em Código Determinístico (Zero Alucinação de Prazos)
O sistema **proíbe terminantemente** que LLMs calculem contagem de dias úteis ou prazos fatais. 
- A IA extrai apenas a **data de publicação** e o **dispositivo legal** (ex.: Art. 1.003, § 5º do CPC).
- O motor de código determinístico (`prazos.js`) aplica a tabela oficial de feriados nacionais, forenses (carnaval, recesso forense de 20/12 a 20/01) e feriados locais do tribunal da causa.
- Gera automaticamente as réguas:
  - **D-2:** Alerta de minuta pronta.
  - **D-1:** Alerta de revisão do sócio.
  - **D-0 (Fatal):** Protocolo até as 18h/23h59.

### 3.2 O Silogismo Jurídico Estruturado
Na elaboração de peças, o motor executa em duas etapas desacopladas:
1. **Fase de Planejamento (JSON Estruturado):**
   - Extração do fato controvertido.
   - Indicação da prova dos autos com folha exata (`fls. 142 do PDF`).
   - Tese jurídica e subsunção normativa.
   - Avaliação da suficiência probatória (suficiente / fraca / ausente).
2. **Fase de Redação:**
   - Invocação do modelo de linguagem com streaming SSE.
   - Inserção forçada do pacote de estilo do escritório (fonte, vocabulário, estrutura de tópicos).
   - Bloqueio estrito: fatos ausentes viram `[DADO FALTANTE: descrever o documento que a parte precisa fornecer]`.

### 3.3 Módulo de Revisão Adversarial Pré-Protocolo
Antes do envio para o cliente ou protocolo, a peça é auditada por uma instância que atua no papel da parte contrária:
- Localiza falhas de pressuposto processual (tempestividade, representação, preparo).
- Aponta teses fracas ou incompatíveis entre si (ex.: preliminar que conflita com o mérito).
- Emite score de risco: `Apto`, `Apto com Ressalvas` ou `Inapto (Revisão Crítica Obrigatória)`.

---

## 4. Segurança da Informação, LGPD e Conformidade OAB

A conformidade regulatória foi desenhada para superar as exigências de bancos, seguradoras e multinacionais atendidas pelos escritórios de advocacia.

### 4.1 Conformidade com a Lei Geral de Proteção de Dados (LGPD - Lei 13.709/2018)
- **Não Retenção de Dados por Terceiros (Zero Data Retention):** O contrato de API empresarial com Anthropic/Google garante expressamente que **nenhum dado enviado é utilizado para treinar ou aprimorar modelos de inteligência artificial**.
- **Isolamento Criptográfico Multi-Tenant:** Cada escritório possui um cofre de credenciais e um identificador de tenant (`org_id`) isolado. Não existe cruzamento de dados entre bancas.
- **Padrão de Mascaramento de PII (Personally Identifiable Information):** Scripts de pré-processamento mascaram CPF, dados bancários e nomes de partes protegidas por segredo de justiça antes da transmissão para o endpoint de IA.

### 4.2 Código de Ética e Disciplina da OAB (Provimento 205/2021)
- O provimento da OAB autoriza o uso de ferramentas tecnológicas e de inteligência artificial na advocacia, desde que **a decisão técnica, a redação final e a assinatura permaneçam sob responsabilidade privativa do advogado**.
- O Themis Jurídico OS implementa a salvaguarda de **Revisão Humana Obrigatória**: o sistema gera exclusivamente minutas com estado de revisão pendente. Ele nunca assina eletronicamente e nunca protocola diretamente no tribunal sem o token físico (A1/A3) do advogado.

---

## 5. Rotinas Agendadas e Automação Operacional

A Estação Themis opera em piloto automático através de três gatilhos diários nativos via Windows Task Scheduler / Cron:

| Horário | Rotina | Script | Ação Executada |
|---|---|---|---|
| **07h00** | **Briefing Matinal Executivo** | `rotina_07h_briefing_matinal.py` | Varre mensagens recebidas na madrugada, identifica urgências críticas (N4/N5), monta pauta do dia e notifica sócios por e-mail/WhatsApp. |
| **12h00** | **Auditoria de SLAs e Prazos** | `rotina_12h_auditoria_sla_prazos.py` | Audita demandas sem acolhimento há mais de 1h30 e peças com prazo fatal para hoje; envia alerta sonoro e visual para as coordenações. |
| **18h00** | **Fechamento Diário & Revisão** | `rotina_18h_fechamento_revisao_adversarial.py` | Audita peças prontas do dia no modo adversarial, atualiza o status de todas as demandas e gera relatório de produtividade da equipe. |
