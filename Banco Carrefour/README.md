# 🏦 Auditoria e Testes de Acessibilidade Digital (WCAG 2.1)

## 🎯 Alvo da Análise: Homepage Institucional e Desafio de Segurança — Banco Carrefour
*   **URL Auditada:** `https://carrefoursolucoes.com.br`
*   **Padrão de Referência:** WCAG 2.1/2.2 (Nível AA) & LBI (Lei nº 13.146/2015).

---

## 📋 1. Visão Geral do Projeto
Este repositório documenta a auditoria técnica de acessibilidade digital realizada na página inicial e na camada de segurança do **Banco Carrefour (Carrefour Soluções Financeiras)**. 

O processo foi estruturado em quatro etapas independentes para isolar falhas de código e confrontar a eficácia das ferramentas automatizadas contra testes manuais humanos. A análise mapeia as barreiras digitais frente às diretrizes internacionais da **WCAG 2.1 (Nível AA)** e ao **Artigo 63 da Lei Brasileira de Inclusão (LBI)**.

---

## 📊 2. Resumo das Ferramentas Executadas

| Etapa do Teste | Ferramenta Utilizada | Status / Avaliação | Escopo do Mapeamento |
| :---: | :--- | :--- | :--- |
| **1** | Teste Manual (Teclado `Tab` + NVDA) | 🔴 Crítico | Apagão massivo de conteúdo, seções ocultas ao teclado e ruído em imagens de serviços. |
| **2** | Extensão WAVE | 🟡 Alertas | **0 Erros Críticos**, 0 Falhas de Contraste e **23 Alertas de Redundância**. |
| **3** | Extensão Axe DevTools | ✅ Em Conformidade | **0 Issues estruturais** automáticas (Cenário de Falso Positivo no código visível). |
| **4** | Automação com **Cypress** | 🔴 Falha | Capturou 1 erro crítico de tempo limite (`meta-refresh`) na tela de segurança de entrada. |

---

## 🔎 3. Detalhamento dos Achados por Etapa:

### ⌨️ ETAPA 1: Testes Manuais Assistivos (Teclado & Leitor de Tela NVDA)
A validação humana sem o uso de mouse revelou barreiras severas que eliminam a autonomia do usuário e geram um apagão completo de conteúdo comercial:

1.  **Omissão de Conteúdo Comercial e Contratação "No Escuro" (Banners Principais):** Ao navegar via tecla `Tab` pelas seções promocionais iniciais dos cartões Carrefour, Atacadão e Sam's Club, o seletor salta por cima de todas as chamadas explicativas. O NVDA cai diretamente em botões genéricos como "Saiba mais e "Peça já o seu" ocultando o propósito real das ofertas para usuários cegos e gerando quebra severa na árvore de acessibilidade.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.3.2 (Meaningful Sequence) e Critério 2.4.4 (Link Purpose).
2.  **Apagão Massivo de Informações Institucionais e de Negócio (Seções Centrais):** O seletor de teclado simplesmente ignora e pula três seções fundamentais de conversão do portal: a grade de benefícios do cartão (Anuidade zero, parcelas, prazos), o bloco de download do aplicativo móvel (com o QR Code descritivo) e a área de Facilidades de conta (limites e datas de vencimento). Como esses blocos foram programados sem âncoras semânticas ou elementos focáveis, o usuário cego sofre uma perda massiva de contexto informacional, sendo arremessado diretamente para os links do rodapé ("Nosso Blog").
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.3.1 (Info and Relationships) e Critério 2.1.1 (Keyboard).
3.  **Rótulos Redundantes, Imagens Mulas e Links Genéricos (Seção de Serviços):** Na seção "Nossos Serviços" (Seguros, Empréstimos e Aplicativo), os elementos gráficos promocionais carecem de descrições textuais alternativas (atributos `alt`). O sintetizador de voz vaza termos técnicos internos e fragmentados (ex: *"seguros gráfico link", "app cartão Carrefour gráfico link"*). Além disso, a dependência de botões adjacentes idênticos com o rótulo genérico *"Ver mais"* quebra o propósito do link, gerando alto ruído cognitivo e desorientação para usuários cegos.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.1.1 (Non-text Content) e Critério 2.4.4 (Link Purpose - In Context).

### 🌊 ETAPA 2: Varredura Automatizada Visual (Extensão WAVE)
A varredura visual de interface identificou conformidade na validação sintática direta, mas confirmou redundâncias severas na camada de navegação:
*   **0 Erros Críticos e 0 Falhas de Contraste:** O motor automatizado não detectou quebras diretas de código ou taxas de contraste incorretas nos elementos analisados por padrão na homepage visível.
*   **23 Alertas de Estrutura (Alerts):** Concentração massiva de **15 Links Redundantes (Redundant links)**. Esse volume corrobora matematicamente o comportamento de loop e confusão identificado nos testes manuais na seção de Serviços, onde o teclado passa por múltiplos links repetitivos que apontam para o mesmo destino.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 2.4.4 (Link Purpose).

### Evidência:

<img width="1890" height="862" alt="Captura de tela 2026-08-15 111940" src="https://github.com/user-attachments/assets/d572fc8b-a4e7-48a9-a386-cc7e206f6b8d" />


### 📐 ETAPA 3: Inspeção Estrutural de Código (Extensão Axe DevTools)
O motor automatizado do Axe DevTools realizou a varredura profunda nas linhas do código HTML e cravou **0 não-conformidades de código**:

1.  **Conformidade Sintática Estática (Total Issues: 0):** O código fonte estrutural atende aos critérios básicos de validação estática automatizada monitorados pelo motor do Axe, sem apresentar quebras explícitas de tags ou atributos mal formados na árvore visível do DOM.
    *   *Análise Crítica de QA Sênior (O Falso Positivo):** Este resultado consolida o conceito de "Falso Positivo" em testes automáticos. Embora o motor classifique a interface com zero erros, o teste funcional assistivo humano (Etapa 1) comprovou o apagão de conteúdo nas seções centrais. Isso ocorre porque o algoritmo do robô falha ao não conseguir mensurar a ausência total de elementos interativos e o isolamento de blocos de negócios estáticos fora do fluxo de tabulação.
    *   *Diretriz Relacionada:* WCAG 2.1 — Critério 2.1.1 (Keyboard - Princípio da Operabilidade).
  
### Evidência:

<img width="1901" height="823" alt="Captura de tela 2026-08-15 112157" src="https://github.com/user-attachments/assets/eb6204ae-9b6b-4604-bfd1-80a323908e2d" />


### 🤖 ETAPA 4: Automação Contínua com Script (Cypress + `cypress-axe`)
Execução do script de teste automatizado local integrado ao motor do Cypress. O ecossistema de segurança do portal interceptou a execução gerando uma tela de barreira contra bots maliciosos (Desafio de WAF). Contudo, a esteira atuou com sucesso como Quality Gate e barrou o processo ao capturar **1 violação crítica estrutural na página de entrada**:

1.  **`meta-refresh` (detectado em 1 nó):** Presença de tag de atualização automatizada de tempo limite na raiz do HTML da tela de segurança de firewall do banco.
    *   *O Impacto Prático:* O recarregamento forçado e periódico da página de segurança sem o comando do usuário faz com que leitores de tela (NVDA) reiniciem a leitura do zero e percam a posição do foco do teclado. Isso impede que pessoas cegas ou com limitações motoras tenham tempo hábil para decifrar e superar o desafio de segurança, sendo bloqueadas na portaria do site.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 2.2.1 (Tempo Limite Ajustável - Nível A).

### Evidência:

<img width="1820" height="880" alt="Captura de tela 2026-08-15 113245" src="https://github.com/user-attachments/assets/1198a5d3-ebea-47fa-bc30-7eb471ece6ef" />

---

## 💡 4. Diretrizes WCAG & Plano de Correção para a Engenharia

### 1. Camada de Segurança e Resolução do Cypress:
*   **[Ajuste de Automação]** Eliminar a dependência de tags de atualização forçada baseadas em `meta-refresh` nas telas de validação de firewall do banco. Substituir o mecanismo por requisições assíncronas via JavaScript ou dar ao usuário o controle completo para pausar, estender ou ocultar o tempo de expiração da página de segurança, respeitando o Critério 2.2.1 da WCAG.

### 2. Saneamento Temático e Semântica de Conteúdo (HTML5 / DOM):
*   Reestruturar os blocos estáticos das seções centrais de benefícios (Anuidade Zero, Funcionalidades do App e Facilidades), aplicando elementos focáveis adequados ou garantindo que o fluxo de leitura do leitor de telas percorra os textos institucionais de forma linear antes de saltar para o rodapé.
*   Injetar o atributo `tabindex="0"` em áreas informativas chave ou reorganizar a ordem do DOM para que as vantagens comerciais do cartão não fiquem ocultas ao usuário de teclado.

### 3. Tratamento de Imagens e Componentes de Conversão (ARIA):
*   Corrigir os atributos textuais alternativos (tags `alt`) nas imagens promocionais da seção "Nossos Serviços". Substituir os termos técnicos e vazamentos de arquivos (ex: *"seguros gráfico link"*) por descrições humanas funcionais (ex: `alt="Mulher sorrindo segurando notas de dinheiro, representando o serviço de empréstimo fácil"`).
*   Saneá-los para evitar links repetitivos redundantes apontando para o mesmo nó de destino, eliminando os 15 alertas mapeados pelo WAVE.

