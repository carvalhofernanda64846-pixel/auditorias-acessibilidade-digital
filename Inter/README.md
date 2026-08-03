# 🏦 Auditoria e Testes de Acessibilidade Digital (WCAG 2.1 / 2.2)

## 🎯 Alvo da Análise: Homepage Institucional e de Serviços — Banco Inter (Web)
*   **URL Auditada:** `https://inter.co`
*   **Padrão de Referência:** WCAG 2.1 / 2.2 (Nível AA) & LBI (Lei nº 13.146/2015).

---

## 📋 1. Visão Geral do Projeto
Este repositório documenta a auditoria técnica de acessibilidade digital realizada na página inicial do **Banco Inter**. 

O processo foi estruturado em quatro etapas independentes para isolar e compreender o impacto real das barreiras de desenvolvimento na vida do usuário final. A análise confronta os componentes do portal com as diretrizes internacionais da **WCAG 2.1 e 2.2 (Nível AA)** e com o **Artigo 63 da Lei Brasileira de Inclusão (LBI)**.

---

## 📊 2. Resumo das Ferramentas Executadas

| Etapa do Teste | Ferramenta Utilizada | Status / Avaliação | Escopo do Mapeamento |
| :---: | :--- | :--- | :--- |
| **1** | Teste Manual (Teclado `Tab` + NVDA) | 🔴 Crítico | Loop no carrossel, foco invisível, links de telefones sem identificação do setor e omissão de conteúdo (ignora a descrição das imagens e banners, lendo apenas os botões). |
| **2** | Extensão WAVE | 🔴 Crítico | **1 Erro Crítico**, **22 Erros de Contraste** e **65 Alertas**. |
| **3** | Extensão Axe DevTools | 🔴 Crítico | **12 Issues estruturais** globais no HTML da página. |
| **4** | Automação com Cypress | 🔴 Falha | Script automatizado barrou 2 categorias de erros críticos (Contraste e Idioma) em 7 nós da árvore do DOM. |

---

## 🔎 3. Detalhamento dos Achados por Etapa

### ⌨️ ETAPA 1: Testes Manuais Assistivos (Teclado & Leitor de Tela NVDA)
A validação humana sem o uso de mouse revelou que a página inicial do portal cria um cenário severo de exclusão digital e alto ruído cognitivo:

1.  **Loop de Foco Fantasma e Vazamento de Tags de Código em Carrossel:** Ao navegar com a tecla `Tab` pelo carrossel do final da pagina, o leitor de tela (NVDA) apresenta uma quebra crítica de semântica. O sistema entra em um loop infinito, repetindo termos técnicos de desenvolvimento e nomes de arquivos internos (ex: *"slide um botão principal, Marcos Geoto slide, Geoto slide três botão"*), enquanto omite completamente a descrição textual das 4 imagens ativas. Além disso, o seletor obriga o usuário a passar repetidas vezes pelo mesmo botão invisível de ação (*"Conhecer o Wearables"*), gerando desorientação severa.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 4.1.2 (Name, Role, Value) e Critério 1.3.2 (Meaningful Sequence).
2.  **Isolamento e Omissão de Contexto nos Canais de Suporte (Rodapé):** Ao tabular até a seção de atendimento, o seletor de teclado salta diretamente para as tags de link dos números de telefone e anuncia apenas os numerais soltos ("0800..."). O NVDA ignora por completo os textos estáticos que dão nome aos setores (como SAC, Ouvidoria, Capitais). O relacionamento lógico é quebrado, forçando o usuário cego a efetuar ligações "no escuro" por falta de amarração textual no código.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 2.4.4 (Link Purpose - In Context) e Critério 1.3.1 (Info and Relationships).
3.  **Remoção Crítica do Indicador de Foco e Quebra de Rolagem (Scroll):** Nas seções do topo e meio da página, a propriedade visual de foco foi removida ou ocultada via folhas de estilo (`CSS`), impedindo o rastreio do cursor por usuários com baixa visão ou limitações motoras. O indicador só se torna visível em áreas escuras do rodapé por mero acidente cromático. Além disso, a página falha ao não acionar o scroll automático de acompanhamento do cursor, deixando a tela estática enquanto o foco avança escondido pelo código.
    *   *Diretriz Violada:* WCAG 2.2 — Critério 2.4.13 (Focus Appearance) e Critério 2.1.1 (Keyboard).
4.  **Inconsistência de Acessibilidade e Omissão Comercial em Banners:** A interface apresenta um comportamento totalmente inconsistente no tratamento de elementos gráficos. Enquanto o NVDA lê a descrição interna de algumas imagens, ele ignora outras por completo. Na maioria dos banners promocionais, o leitor de tela salta os blocos de textos comerciais informativos (como as vantagens da *Global Account*) e cai direto em botões genéricos (ex: *"Saiba mais"* ou *"Abrir conta"*). Essa falta de padronização oculta o propósito real dos produtos, forçando o usuário cego a navegar por botões de ação sem conseguir consumir o contexto da oferta.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.3.2 (Meaningful Sequence), Critério 2.4.4 (Link Purpose) e Critério 3.2.4 (Consistent Identification).

### 🌊 ETAPA 2: Varredura Automatizada Visual (Extensão WAVE)
A varredura visual de interface identificou não-conformidades de alto impacto na estrutura do portal:
*   **1 Erro de Idioma Ausente (Language missing or invalid):** Confirmação visual da ausência do atributo de idioma na raiz do HTML, gerando incompatibilidade fonética.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 3.1.1 (Language of Page).
*   **22 Erros de Contraste Cromático (Very low contrast):** 22 ocorrências graves de elementos de texto com relação de contraste abaixo de 4.5:1, gerando a camuflagem visual do foco.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.4.3 (Contrast).
*   **65 Alertas de Estrutura (Alerts):** Concentração massiva de redundâncias de links e elementos adjacentes, mapeando o loop de foco do carrossel.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 2.4.4 (Link Purpose).

### Evidência:

<img width="1898" height="845" alt="Captura de tela 2026-08-02 155735" src="https://github.com/user-attachments/assets/67960681-8fae-4d14-b216-3e4804ec1fbd" />


### 📐 ETAPA 3: Inspeção Estrutural de Código (Extensão Axe DevTools)
O motor do Axe analisou a semântica profunda do HTML e apontou **12 não-conformidades críticas** distribuídas em 3 categorias exatas:

1.  **Insuficiência de Contraste Cromático (Elements must meet minimum color contrast ratio thresholds) — 10 ocorrências:** Elementos de texto e links cruciais de navegação com cores abaixo da taxa de contraste exigida pela norma.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.4.3 (Contrast).
2.  **Quebra de Hierarquia em Elementos ARIA (Certain ARIA roles must contain particular children) — 1 ocorrência:** Tag ARIA aplicada de forma incorreta no HTML, deixando filhos sem o elemento pai adequado, confundindo o sintetizador de voz.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.3.1 (Info and Relationships).
3.  **Ausência de Idioma no Documento Raiz (<html> element must have a lang attribute) — 1 ocorrência:** O site omitiu a declaração do atributo de idioma na tag principal do código, afetando o processamento fonético de leitores de tela globais.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 3.1.1 (Language of Page).
  
### Evidência:

<img width="1889" height="842" alt="Captura de tela 2026-08-02 155641" src="https://github.com/user-attachments/assets/5dfcc552-8328-4a76-b583-bf1d8fc0d8e7" />


---
### 🤖 ETAPA 4: Automação Contínua com Script (Cypress + `cypress-axe`)
Execução do script de teste automatizado local focado na validação contínua da integridade semântica do código. O motor do Cypress barrou a execução da esteira ao detectar **2 categorias de violações críticas totalizando 7 nós afetados**:

1.  **`color-contrast` (detectado em 6 nós):** Alerta automatizado que ratifica a ausência de contraste mínimo em elementos textuais da interface, gerando camuflagem visual para pessoas com baixa visão.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.4.3 (Contrast).
2.  **`html-has-lang` (detectado em 1 nó):** Confirmação em código de que o portal omitiu o atributo de idioma na raiz do documento HTML, impedindo que sintetizadores de voz processem a fonética de maneira correta.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 3.1.1 (Language of Page).

*   **Impacto de Engenharia:** O script funcionou com sucesso como um Quality Gate (Barreira de Qualidade), impedindo de forma automatizada que códigos inacessíveis avancem para o ambiente de produção.

### Evidência:

<img width="1889" height="835" alt="Captura de tela 2026-08-03 095130" src="https://github.com/user-attachments/assets/6c025db5-5bd1-45e2-afda-cd398d7d8417" />


---

## 💡 4. Diretrizes WCAG & Plano de Correção para a Engenharia

### 1. Declaração e Semântica Global (HTML5):
*   **[Ajuste de Automação]** Injetar imediatamente o atributo de idioma correto na tag raiz do código (ex: `<html lang="pt-BR">`) para garantir que os sintetizadores de voz processem a fonética sem sotaques estrangeiros, resolvendo a quebra apontada pelo Cypress.
*   Corrigir a árvore de componentes ARIA, garantindo que as tags de acessibilidade respeitem os elementos pais obrigatórios exigidos pela especificação W3C.

### 2. Interface, Navegação e Carrossel (CSS/JS):
*   Sanear o componente de carrossel promocional do topo, injetando atributos `aria-label` descritivos nos botões de paginação para substituir o vazamento de termos internos de desenvolvimento (*"Geoto slide"*).
*   Utilizar propriedades ARIA (como `aria-live` e `aria-hidden`) para garantir que apenas o slide visível na tela receba o foco do teclado, destruindo o loop de links e botões repetitivos (*"Conhecer o Wearables"*).
*   Customizar a propriedade CSS `:focus-visible` em todo o portal para restaurar a borda visual do indicador de seleção sobre fundos claros.

### 3. Associação de Conteúdo e Canais de Suporte (Código/Acessibilidade):
*   Vincular os textos informativos dos setores de atendimento (SAC, Ouvidoria) aos links dos seus respectivos números de telefone utilizando o atributo `aria-label` ou `aria-describedby`, impedindo que o teclado anuncie numerais isolados e sem contexto.
*   Garantir a descrição e a leitura linear das chamadas comerciais de todos os banners antes de direcionar o foco para os botões de ação genéricos (evitando a leitura apenas de imagens soltas ou botões vazios).

### 4. Ajuste de Contraste Visual (Design/CSS):
*   Corrigir a folha de estilos das 6 ocorrências identificadas pelo Cypress (e 22 do WAVE), elevando a taxa de contraste cromático das fontes e links para o mínimo de 4.5:1 exigido pela WCAG.
