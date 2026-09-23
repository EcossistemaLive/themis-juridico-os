# MODELO DE NEGÓCIO, PRECIFICACÃO E GO-TO-MARKET (GTM)
## Themis Jurídico OS · Estratégia Comercial para Escalar Venda em Massa

> **Ecossistema Live · Estratégia Comercial & Unit Economics**  
> **Objetivo:** Rumo a 100+ Escritórios Ativos com R$ 500k+ de MRR

---

## 1. Posicionamento de Mercado e Proposta Única de Valor (UVP)

### Declaração de Posicionamento:
> *"Para sociedades de advogados que sofrem com o caos do WhatsApp, sobrecarga da equipe e medo de alucinações de IAs genéricas, o **Themis Jurídico OS** é o primeiro sistema operacional híbrido de IA que vigia as demandas de clientes em tempo real, garante SLA de atendimento e redige peças jurídicas complexas com ancoragem folha a folha e zero alucinação — mantendo o controle ético e os dados dentro da banca."*

### Por que os escritórios compram imediatamente:
1. **Paz de Espírito dos Sócios:** Elimina a necessidade do sócio responder mensagens de trabalho às 23h de domingo por medo de perder o cliente.
2. **Blindagem contra Danos Morais e Preclusão:** A detecção automática de DTEs e intimações em grupos evita perdas de prazos processuais fatais.
3. **Multiplicação da Capacidade Produtiva:** Um advogado júnior produz com a profundidade analítica de um sênior na metade do tempo.
4. **ROI Comprovado em 30 Dias:** O custo mensal da solução equivale a uma fração de um único salário de estagiário, enquanto resolve o trabalho de triagem de uma equipe inteira de controladoria.

---

## 2. Estrutura de Planos e Precificação

O modelo comercial é composto por **Taxa de Implantação (Setup)** + **Assinatura Mensal Recorrente (MRR)** + **Repasse de Consumo de IA (Transparente)**.

| Plano | **Themis Boutique** | **Themis Growth** (Mais Vendido) | **Themis Enterprise** |
|---|---|---|---|
| **Porte do Escritório** | 2 a 5 advogados | 6 a 20 advogados | 20+ advogados / Múltiplas Filiais |
| **Grupos de WhatsApp** | Até 15 grupos | Até 60 grupos | Ilimitados |
| **Estação Themis Edge** | Instalação Local (1 máquina) | 1 Servidor / Estação Dedicada | Cluster / Multi-estações |
| **Módulos Inclusos** | - Argos (Vigília)<br>- Temis (Concierge)<br>- Mentor Jurídico<br>- Themis Core (Peças) | - Todos do Boutique<br>- Monitor DTE Prioritário<br>- Revisão Adversarial Completa<br>- Rotinas 07h, 12h e 18h | - Todos do Growth<br>- Integração com ERP Legado<br>- Overlays de Estilo Customizados<br>- Treinamento Presencial C-Level |
| **Usuários / Seats** | Até 5 usuários | Até 20 usuários | Ilimitado |
| **Taxa de Setup (Única)** | **R$ 3.500,00** | **R$ 6.500,00** | **R$ 15.000,00+** |
| **Mensalidade (MRR)** | **R$ 1.850,00 / mês** | **R$ 3.850,00 / mês** | **R$ 7.900,00 a R$ 14.500,00 / mês** |
| **Consumo de IA** | Conta Claude/Gemini do cliente | Conta Claude/Gemini do cliente | Faturamento consolidado ou direto |

> **Nota sobre o Custo de IA:** A postura de transparência radical onde o cliente utiliza sua própria chave de API (ou nós criamos a conta empresarial dele) é um dos maiores argumentos de venda. Demonstra que **o escritório não é refém do fornecedor**, paga o custo real da inteligência sem margens ocultas e tem garantia formal de não retenção de dados da Anthropic/Google.

---

## 3. Unit Economics e Margem Operacional

| Métrica | Valor Estimado | Premissas |
|---|---|---|
| **Ticket Médio de Entrada (Setup)** | **R$ 6.500,00** | Concentração no Plano Growth |
| **MRR Médio por Cliente** | **R$ 3.850,00** | Assinatura mensal da suíte |
| **Custo de Servidor Cloud / Cliente** | **R$ 120,00 / mês** | Firebase + Cloud Functions southamerica-east1 |
| **Custo de Suporte N2 / Cliente** | **R$ 280,00 / mês** | Monitoramento remoto proativo via 2FA |
| **Margem Bruta Recorrente** | **> 85%** | Altamente escalável por software |
| **CAC (Custo de Aquisição de Cliente)** | **R$ 2.400,00** | Prospecção ativa B2B + Comissões |
| **Payback do CAC** | **Imediato no Setup (< 1 mês)** | O valor de Setup cobre 2x o CAC |
| **LTV Médio (Chun anual < 4%)** | **R$ 92.400,00** | Retenção média estimada de 24 meses |
| **Relação LTV / CAC** | **38,5 : 1** | Eficiência de capital excepcional |

---

## 4. Estratégia de Go-to-Market (GTM) para Venda em Massa

Para atingir escala nacional sem depender exclusivamente de indicações orgânicas, a esteira de vendas utiliza os próprios ativos desenvolvidos pelo Ecossistema Live:

### 4.1 A Máquina de Prospecção Autônoma B2B (Scripts `agente-prospeccao`)
1. **Mineração de Alvos:** Varredura automática no CNES / OAB / Receita Federal por sociedades de advogados com 5 a 50 funcionários nas capitais (SP, RJ, MG, GO, PR, RS, DF).
2. **Abordagem Personalizada ("O Teste dos Grupos"):** Mensagem no LinkedIn ou WhatsApp para os sócios com a pergunta provocativa:
   > *"Doutor, se um cliente mandar uma notificação de DTE ou uma penhora agora às 21h em um dos 80 grupos do escritório, sua banca tem um alerta automático ou você depende de alguém lembrar de ver a mensagem amanhã à tarde?"*
3. **Taxa de Conversão em Reunião:** Em testes empíricos, essa pergunta atinge mais de 28% de resposta positiva para agendamento de diagnóstico.

### 4.2 A Demonstração Fatal de 15 Minutos (The "Aha!" Moment)
A demonstração comercial nunca é genérica. O consultor pede ao sócio:
- *"Doutor, me envie o PDF de uma contestação ou apelação que seu escritório protocolou recentemente, ou os autos de um caso complexo."*
- Ao vivo na tela, o Themis Core roda o **Modo 1 (Análise Processual)** e a **Revisão Adversarial** em 3 minutos.
- O sistema mostra na tela:
  1. A folha exata de cada prova que o advogado levou horas para achar.
  2. Um ponto cego ou contradição adversarial na peça que a equipe deixou passar.
  3. O painel do Argos demonstrando o Kanban de demandas e a esteira de SLA.
- **Taxa de Fechamento:** Superior a 60% após a demonstração prática nos autos reais do cliente.

### 4.3 Canais de Parceria e Alavancagem
- **Comissões e Seccionais da OAB e ESA (Escolas Superiores de Advocacia):** Patrocínio e palestras sobre *"Inteligência Artificial Responsável e Governança de SLA na Advocacia"*.
- **Integradores de TI Jurídica:** Empresas que vendem infraestrutura, servidores e segurança para escritórios de advocacia recebem 20% de comissão recorrente sobre o MRR.
- **Boutiques como Showcase (Ex.: MLP Advogados):** Utilização do caso de sucesso da MLP como prova social inquestionável de eficiência tributária e cível.

---

## 5. Projeção de Crescimento e Escala (Roadmap de 12 Meses)

| Mês | Clientes Ativos | Setup Acumulado | MRR Recorrente | Faturamento Anualizado (ARR) |
|---|---|---|---|---|
| **Mês 3** | 10 escritórios | R$ 65.000,00 | R$ 38.500,00 | R$ 462.000,00 |
| **Mês 6** | 30 escritórios | R$ 195.000,00 | R$ 115.500,00 | R$ 1.386.000,00 |
| **Mês 9** | 60 escritórios | R$ 390.000,00 | R$ 231.000,00 | R$ 2.772.000,00 |
| **Mês 12** | **120 escritórios** | **R$ 780.000,00** | **R$ 462.000,00** | **R$ 5.544.000,00** |
