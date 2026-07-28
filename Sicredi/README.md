# 🏦 Auditoria e Testes de Acessibilidade Digital (WCAG 2.1 / 2.2)

## 🎯 Alvo da Análise: Landing Page de Captação — Sicredi (Web)
*   **URL Auditada:** `https://sicredi.com.br`
---

## 📋 1. Visão Geral do Projeto
Este repositório documenta a auditoria técnica de acessibilidade digital realizada na *Landing Page* de captação e abertura de contas do **Sicredi**. 

O processo foi dividido de forma estrita em quatro etapas sequenciais para garantir a cobertura total da página. Os testes cobriram desde a experiência prática do usuário com tecnologias assistivas até a validação automatizada de código em esteira de testes. Todos os achados foram confrontados com as diretrizes internacionais da **WCAG 2.1 e 2.2 (Nível AA)** e com o **Artigo 63 da Lei Brasileira de Inclusão (LBI)**.

---

## 📊 2. Resumo das Ferramentas Executadas

| Etapa do Teste | Ferramenta Utilizada | Status / Avaliação | Escopo do Mapeamento |
| :---: | :--- | :--- | :--- |
| **1** | Teste Manual (Teclado `Tab` + NVDA) | 🔴 Crítico | Barreiras visuais de foco e omissão de conteúdos essenciais. |
| **2** | Extensão WAVE | 🔴 Crítico | 20 Erros Críticos e 92 Alertas de acessibilidade no HTML. |
| **3** | Extensão Axe DevTools | 🔴 Crítico | 7 Issues estruturais (4 Críticas e 3 Sérias). |
| **4** | Automação com Cypress | 🔴 Falha Técnica | Quebra estrutural por elementos interativos aninhados. |

---

## 🔎 3. Detalhamento dos Achados por Etapa

### ⌨️ ETAPA 1: Testes Manuais Assistivos (Teclado & Leitor de Tela NVDA)
Testes executados sem o uso de mouse, simulando a navegação de usuários cegos, com baixa visão ou limitações motoras. Foram mapeadas 3 barreiras severas:

1.  **Camuflagem Visual do Indicador de Foco:** Ao navegar com a tecla `Tab`, a bordinha preta padrão do navegador que indica a seleção do elemento simplesmente desaparece ou fica invisível ao passar por cima das cores e detalhes em verde escuro corporativo da marca.
    *   *Critério WCAG Afetado:* 2.4.13 (Focus Appearance - WCAG 2.2).
      
2.  **Omissão de Conteúdo e Contratação "No Escuro" (Seção de Cartões):** O foco do teclado cai direto no botão "Solicitar cartão" duas vezes seguidas e pula para "Expandir características". O sistema ignora e não lê o título do cartão (ex: Mastercard Black) e pula todas as vantagens textuais (como Salas VIP). O usuário cego é induzido a contratar um produto sem o sistema ler as especificações.
    *   *Critério WCAG Afetado:* 1.3.2 (Meaningful Sequence) e 2.1.1 (Keyboard).
   
3.  **Falta de Contexto nos Canais de Suporte (Rodapé):** O leitor de tela foca nos links numéricos e lê apenas os números isolados ("0800..."), ignorando os textos estáticos dos setores. É impossível saber qual número é o SAC, Ouvidoria ou Denúncia. Além disso, o seletor ignora os QR Codes, ocultando o canal de atendimento em Libras para usuários surdos.
    *   *Critério WCAG Afetado:* 2.4.4 (Link Purpose - In Context) e 1.1.1 (Non-text Content).

---

### 🌊 ETAPA 2: Varredura Automatizada Visual (Extensão WAVE)
A inspeção automática do WAVE escaneou a interface e acusou erros de preenchimento e relacionamento no código:
*   **13 Erros de Texto Alternativo Ausente (Missing Alternative Text):** Confirma o problema do teste manual. Os QR Codes de suporte (Libras e Português) e mais 11 imagens informativas não possuem a tag `alt`, tornando-se invisíveis para deficientes visuais.

*   **6 Erros de Imagens de Espaçamento (Spacer Image):** Uso de imagens transparentes antigas para diagramar o layout sem o atributo `alt=""` vazio, gerando ruído de leitura inútil no NVDA.

*   **1 Erro de Rótulo de Formulário (Missing Form Label):** O campo de input do topo ("Informe seu nome para iniciar") não possui uma tag `<label>` vinculada por ID no código, impedindo o leitor de anunciar o que deve ser digitado ali.
    *   *Critério WCAG Afetado:* 1.1.1 (Non-text Content) e 1.3.1 (Info and Relationships).
 
### Evidência:

<img width="1875" height="863" alt="Captura de tela 2026-07-28 105858" src="https://github.com/user-attachments/assets/89fdc87d-cf4a-45c3-bc51-92bcf973910f" />

---

### 📐 ETAPA 3: Inspeção Estrutural de Código (Extensão Axe DevTools)
O motor do Axe analisou a semântica do HTML e identificou 7 não-conformidades críticas:
*   **4 Ocorrências de Botões sem Texto (Buttons must have discernible text):** Identificados especificamente na classe `button.owl-dot` (as linhas de paginação do carrossel principal). Os botões existem no código, mas o texto descritivo está totalmente vazio (`Accessible Text: empty`).

*   **3 Ocorrências de Controles Aninhados (Interactive controls must not be nested):** Elementos interativos inseridos incorretamente dentro de outros blocos clicáveis na estrutura do código.
    *   *Critério WCAG Afetado:* 4.1.2 (Name, Role, Value).
 
### Evidência:

<img width="1873" height="822" alt="Captura de tela 2026-07-28 094558" src="https://github.com/user-attachments/assets/b8731cc7-27c0-40ea-b034-0e37f3cd4741" />

---

### 🤖 ETAPA 4: Automação Contínua com Script (Cypress + `cypress-axe`)
Execução do script de teste automatizado local para simular uma esteira de integração contínua (CI/CD). O robô barrou o carregamento da página e acusou a seguinte quebra:
*   **Falha Identificada:** `a11y error! nested-interactive on 3 nodes`

*   **Análise do Bug no Painel:** O motor do Cypress identificou elementos interativos inválidos e aninhados na seção **"Para você"** (bloco informativo de finanças). O código inseriu tags clicáveis de forma incorreta dentro do contêiner do bloco, gerando um conflito de nós que quebra a árvore de acessibilidade do navegador e confunde as tecnologias assistivas.
    *   *Critério WCAG Afetado:* 4.1.2 (Name, Role, Value).

### Evidência:

<img width="1830" height="826" alt="Captura de tela 2026-07-28 103603" src="https://github.com/user-attachments/assets/43282cd5-5241-4afc-9247-9aa9583028f4" />

---

## 💡 4. Plano de Mitigação Técnico:

1.  **Estilização do Foco (`CSS`):** Aplicar a propriedade CSS `:focus-visible` customizada para forçar uma borda espessa e de alto contraste (mínimo de 4.5:1) nos botões e links interativos da página.
2.  **Rótulos no Carrossel:** Adicionar a propriedade `aria-label="Ir para o banner [X]"` em cada tag `button.owl-dot` para dar sentido às linhas de paginação.
3.  **Vínculo Semântico no Suporte:** Utilizar o atributo `aria-describedby` nos links de telefone apontando para o ID do texto do setor correspondente (SAC, Ouvidoria), além de preencher a tag `alt` nas imagens dos QR Codes de Libras e Português.
4.  **Correção de Tags Aninhadas:** Separar os elementos clicáveis inválidos apontados pelo Cypress na seção "Para você" em componentes limpos, independentes e hierárquicos no HTML.

---
