# 🏦 Auditoria e Testes de Acessibilidade Digital (WCAG 2.1 / 2.2)

## 🎯 Alvo da Análise: Homepage Institucional e de Captação — Serasa Experian (Web)
*   **URL Auditada:** `https://serasa.com.br`
*   **Dispositivo de Teste:** Notebook Acer Aspire (Ambiente Web Windows).
*   **Padrão de Referência:** WCAG 2.1 / 2.2 (Nível AA) & LBI (Lei nº 13.146/2015).

---

## 📋 1. Visão Geral do Projeto
Este repositório documenta a auditoria técnica de acessibilidade digital realizada na página inicial e de captação de crédito da **Serasa Experian**. 

O processo foi dividido rigorosamente em quatro etapas independentes para mapear o impacto real das barreiras de código na vida do usuário. A análise cobriu desde testes manuais assistivos até varreduras de código em conformidade com as diretrizes internacionais da **WCAG 2.1 e 2.2 (Nível AA)** e com o **Artigo 63 da Lei Brasileira de Inclusão (LBI)**.

---

## 📊 2. Resumo das Ferramentas Executadas

| Etapa do Teste | Ferramenta Utilizada | Status / Avaliação | Escopo do Mapeamento |
| :---: | :--- | :--- | :--- |
| **1** | Teste Manual (Teclado `Tab` + NVDA) | 🔴 Crítico | Bloqueio de navegação por foco fantasma e quebra de rolagem. |
| **2** | Extensão WAVE | 🔴 Crítico | **29 Erros Críticos**, **19 Erros de Contraste** e **112 Alertas**. |
| **3** | Extensão Axe DevTools | 🔴 Crítico | **21 Issues estruturais** no HTML (Regiões de rolagem e ARIA). |
| **4** | Automação com **Cypress** | ⏳ Aguardando | Script automatizado para validação contínua da árvore do DOM. |

---

## 🔎 3. Detalhamento dos Achados por Etapa

### ⌨️ ETAPA 1: Testes Manuais Assistivos (Teclado & Leitor de Tela NVDA)
A validação humana sem o uso de mouse revelou que a página impede a navegação autônoma e independente:

1.  **Camuflagem Crítica de Foco e Falha de Rolagem (Scroll):** Ao navegar utilizando a tecla `Tab`, o indicador visual de foco (borda padrão) é totalmente camuflado pelas folhas de estilo (`CSS`). Além disso, o site trava e impede o navegador de descer a tela automaticamente. A janela fica estática no topo enquanto o cursor avança "às cegas" internamente pelo código até o rodapé, quebrando a orientação de quem tem baixa visão.
    *   *Diretriz Violada:* WCAG 2.2 — Critério 2.4.13 (Focus Appearance) e Critério 2.1.1 (Keyboard).
2.  **Desorientação Crítica no NVDA:** O leitor de tela anuncia pedaços de frases soltas e pula seções consecutivas do portal sem critério semântico, omitindo informações essenciais de serviços de forma randômica devido à falta de uma ordem lógica estrutural.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.3.2 (Meaningful Sequence).

---

### 🌊 ETAPA 2: Varredura Automatizada Visual (Extensão WAVE)
A inspeção automática do WAVE identificou falhas severas de relacionamento e rotulagem nos elementos de captura de dados da página:
*   **14 Rótulos Duplicados (Multiple form labels):** Presença de mais de uma tag `<label>` vinculada ao mesmo campo de formulário, causando um grave conflito de voz na tecnologia assistiva.
*   **10 Campos Sem Rótulo (Missing form label):** 10 caixas de entrada de dados totalmente sem identificação no HTML, fazendo o leitor de tela anunciar apenas "caixa de edição", sem conseguir ler se o campo é para digitar o CPF, nome ou telefone.
*   **1 Imagem Sem Texto Alternativo (Missing alternative text):** Elemento gráfico importante sem a tag `alt`, ocultando o contexto visual para usuários cegos.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.3.1 (Info and Relationships) e Critério 1.1.1 (Non-text Content).
 
### Evidência:

<img width="1910" height="866" alt="Captura de tela 2026-07-29 102039" src="https://github.com/user-attachments/assets/2145520c-9977-4259-821c-4b5deea00e1c" />

---

### 📐 ETAPA 3: Inspeção Estrutural de Código (Extensão Axe DevTools)
O motor do Axe analisou a semântica profunda do HTML e trouxe as evidências técnicas das falhas de engenharia do portal, totalizando **21 não-conformidades críticas** divididas em 7 categorias de erros:

1.  **Região de Rolagem Sem Acesso por Teclado (1 ocorrência):** Alvo da regra *Scrollable region must have keyboard access*. Bloqueio estrutural no código que impede fisicamente o teclado de comandar o movimento de descida da tela (causa direta do travamento e da falha de scroll relatada na Etapa 1).
    *   *Diretriz Violada:* WCAG 2.1 — Critério 2.1.1 (Keyboard).
2.  **Insuficiência de Contraste Cromático (12 ocorrências):** Alvo da regra *Elements must meet minimum color contrast*. Textos e links com cores apagadas abaixo do limite aceitável de leitura de 4.5:1, prejudicando severamente pessoas com baixa visão ou ceratocone.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.4.3 (Contrast).
3.  **Hierarquia Inválida de Tags ARIA (4 ocorrências):** Alvo da regra *Certain ARIA roles must be contained by particular parents*. Elementos ARIA soltos e mal estruturados no HTML que quebram o fluxo, fazendo o leitor de tela anunciar pedaços de frases sem nexo.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.3.1 (Info and Relationships).
4.  **Foco em Elementos Ocultos (1 ocorrência):** Alvo da regra *ARIA hidden element must not be focusable*. Links ou botões interativos inseridos por erro dentro de blocos marcados com `aria-hidden="true"`, forçando o teclado a passar por links invisíveis (Focos Fantasmas).
    *   *Diretriz Violada:* WCAG 2.1 — Critério 4.1.2 (Name, Role, Value).
5.  **Valores Inválidos em Atributos ARIA (1 ocorrência):** Alvo da regra *ARIA attributes must conform to valid values*. Atributos de acessibilidade preenchidos com termos incorretos no código, confundindo o sintetizador de voz do NVDA.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 4.1.2 (Name, Role, Value).
6.  **Botões Sem Texto Informativo (1 ocorrência):** Alvo da regra *Buttons must have discernible text*. Tag `<button>` vazia ou sem rótulo acessível, fazendo o leitor de tela falar apenas "Botão", ocultando a ação do usuário cego.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 4.1.2 (Name, Role, Value).
7.  **Imagem Sem Descrição Textual (1 ocorrência):** Alvo da regra *Images must have alternative text*. Elemento gráfico sem o preenchimento da tag `alt`, omitindo o contexto visual.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.1.1 (Non-text Content).
    
### Evidência:

<img width="1907" height="838" alt="Captura de tela 2026-07-29 101844" src="https://github.com/user-attachments/assets/c5aace9d-51fa-41eb-af25-74cc0b1ad298" />


## 💡 4. Diretrizes WCAG & Plano de Correção para a Engenharia

1.  **Sincronização de Scroll (`CSS/JS`):** Ajustar as propriedades de transição da página para garantir que o contêiner e a janela acompanhem visualmente o foco ativo do teclado de forma dinâmica.
2.  **Saneamento de Formulários (`HTML5`):** Remover os rótulos duplicados e garantir que cada um dos 10 campos de entrada possua exatamente uma tag `<label>` exclusiva vinculada via atributo `for` ao `id` do campo.
3.  **Remoção de Focos Fantasmas:** Ajustar a árvore de acessibilidade do DOM, garantindo que nenhum elemento que receba foco via teclado (`Tab`) esteja aninhado dentro de contêineres ocultados por tags ARIA hidden.
4.  **Ajuste de Acessibilidade Visual:** Corrigir as 12 fontes e links apagados, elevando a taxa de contraste cromático para o mínimo de 4.5:1 exigido pela WCAG.

---

### 🤖 ETAPA 5: Automação com (Cypress + `cypress-axe`)
*   *Seção reservada para a execução do script automatizado de integração contínua (CI/CD) para capturar a quebra sintática da árvore do DOM.*
*   `[AGUARDANDO CÓDIGO DA EXECUÇÃO DO CYPRESS]`

---

