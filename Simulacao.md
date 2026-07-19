# 📊 Análise de Dados e Experiência do Cliente (CX) - Canais Digitais Bancários

Este repositório contém um diagnóstico analítico e técnico estruturado a partir do mapeamento de feedbacks e reclamações de usuários em canais digitais (App, Web e Chat). O objetivo deste projeto é traduzir percepções textuais em insights acionáveis para equipes de **Operações, TI e Engenharia de Software**, visando a mitigação de atritos na jornada do cliente.

---

## 📑 Resumo Executivo

Os canais digitais apresentam severa fricção operacional concentrada no ecossistema **Pix (App)** e no **Transbordo do Chat**, registrando volumosa volumetria de falhas críticas de infraestrutura e usabilidade. A indisponibilidade de transações em tempo real e o *looping* de atendimento eletrônico são os principais detratores da experiência, gerando impactos diretos no volume de chamados de suporte.

---

## 🔍 Tabela de Diagnóstico Operacional

Abaixo estão classificados os 10 principais cenários mapeados na amostragem, categorizados por causa raiz, severidade e ações corretivas recomendadas:

| ID | Produto/Canal | Sentimento / Urgência | Causa Raiz Provável | Evidência / Feedback do Cliente | Ação Técnica Sugerida |
| :---: | :--- | :---: | :--- | :--- | :--- |
| **001** | Pix / App | 🔴 Negativo / **Crítico** | Instabilidade Técnica | *"Pix fora do ar, dá erro de timeout e o dinheiro sumiu da conta sem o comprovante."* | Implementar *fallback* automático de transação e notificação *push* em tempo real de estorno/processamento lento. |
| **002** | Pix / App | 🔴 Negativo / **Alto** | Interface / Usabilidade | *"Botão de 'Copiar e Cola' fica escondido, tive que digitar uma chave enorme."* | Redesenhar o fluxo da tela de pagamento Pix, destacando o botão de leitura de área de transferência. |
| **003** | Chat / Web | 🔴 Negativo / **Crítico** | Falha de Processo | *"O robô não entende minha dúvida sobre contestação e não me passa para um humano de jeito nenhum."* | Ajustar a árvore de decisão da URA digital para transbordo imediato em palavras-chave críticas (ex: "contestação", "fraude"). |
| **004** | Cartões / App | 🟡 Negativo / **Médio** | Interface / Usabilidade | *"Não acho a opção de bloquear temporariamente o cartão no aplicativo novo."* | Otimizar a arquitetura de informação (IA) do menu de cartões, trazendo a função de bloqueio para a tela principal (1 clique). |
| **005** | Conta Corrente / Web | ⚪ Neutro / **Baixo** | Interface / Usabilidade | *"O extrato em PDF na versão web está desconfigurado, mas consegui ler."* | Ajustar a folha de estilo (CSS) de impressão e geração de relatórios no Internet Banking. |
| **006** | Pix / App | 🔴 Negativo / **Crítico** | Instabilidade Técnica | *"Erro 504 ao tentar ler QR Code. App fecha sozinho."* | Tratar exceções de *crash* no módulo de câmera do aplicativo e otimizar chamadas de API de *gateway* de pagamento. |
| **007** | Conta Corrente / Chat | 🔴 Negativo / **Alto** | Falha de Processo | *"Fiquei 40 minutos esperando na fila do chat após o robô me transferir."* | Redimensionar a escala da equipe de atendimento humano em horários de pico ou revisar o SLA de distribuição de filas. |
| **008** | Cartões / App | 🟢 Positivo / **Baixo** | Eficiência de Interface | *"Muito fácil emitir a segunda via do cartão pelo app novo, parabéns."* | Manter o padrão de UX/UI adotado no fluxo de imagem e replicar para outras jornadas de solicitação. |
| **009** | Pix / Web | 🔴 Negativo / **Alto** | Instabilidade Técnica | *"Comprovante do Pix não gera, fica carregando infinitamente no navegador."* | Corrigir a query de requisição do blob de arquivo ou implementar cache local temporário para exibição do comprovante. |
| **010** | Suporte / App | ⚪ Ignorado / **Insufe.** | Dados Insuficientes | *"Não gostei."* | Desconsiderar para fins de melhoria de software por falta de insumos qualitativos. |

---

## 🎯 Matriz de Priorização (Top 3 Ações Críticas)

Com base no impacto financeiro, volumetria potencial e severidade na experiência do usuário, as três ações prioritárias estabelecidas são:

### 1. Correção do Timeout e Tratamento de Exceção no Pix (IDs 001 e 006)
* **Grau de Urgência:** 🔥 Crítico
* **Justificativa:** Cenários onde há débito em conta sem a respectiva emissão do comprovante ou *crash* estrutural da aplicação (Erro 504) escalam rapidamente para reclamações em órgãos reguladores (BACEN, Procon) e geram sobrecarga imediata na central de atendimento humano.
* **Plano de Ação:** Revisão imediata das conexões síncronas de API no *gateway* de pagamentos, criação de filas de contingência assíncronas e tratamento nativo de erro na captura de imagem via câmera do smartphone.

### 2. Revisão das Regras de Transbordo do Assistente Virtual / Bot (ID 003)
* **Grau de Urgência:** 🔥 Crítico
* **Justificativa:** A retenção excessiva ou em *looping* em jornadas críticas de segurança (como contestação de despesas) destrói o indicador de *First Contact Resolution* (FCR) e eleva a insatisfação (NPS).
* **Plano de Ação:** Implementação de gatilhos automáticos de transbordo no processamento de linguagem natural (NLP) toda vez que termos correlacionados a fraudes, erros graves ou contestações forem detectados.

### 3. Otimização de Interface (UX/UI) do Fluxo "Pix Copiar e Cola" (ID 002)
* **Grau de Urgência:** ⚡ Alto (*Quick Win*)
* **Justificativa:** Problema recorrente de usabilidade que impacta negativamente a conversão de transações. O usuário é forçado a realizar trabalho manual, aumentando a taxa de erro e o tempo médio de operação.
* **Plano de Ação:** Inclusão de um componente visual de destaque na *homescreen* do Pix que identifique automaticamente se há uma chave Pix válida copiada na área de transferência do dispositivo.

---

## 🚀 Tecnologias e Metodologias Utilizadas
* **Análise de Sentimento:** Categorização qualitativa dos relatos de usuários.
* **Mapeamento de Causa Raiz:** Divisão técnica entre falhas de Engenharia/Infraestrutura (TI), Usabilidade (UX/UI) e Processos Operacionais.
* **Framework de Priorização:** Matriz de Impacto vs. Gravidade para tomada de decisões executivas.