# 🏦 Auditoria e Testes de Acessibilidade Digital (WCAG 2.1)

## 🎯 Alvo da Análise: Página de Abertura de Conta — Banco Itaú (Uniclass)
*   **URL Auditada:** `https://itau.com.br`
*   **Dispositivo de Teste:** Notebook Acer Aspire (Ambiente Web Windows).
*   **Padrão de Referência:** WCAG 2.1 (Nível AA) & LBI (Lei nº 13.146/2015).

---

## 📋 1. Visão Geral do Projeto
Este relatório documenta a auditoria técnica de acessibilidade digital realizada na página de abertura de conta do **Banco Itaú Uniclass**. 

O processo foi evoluído de uma análise puramente manual para um diagnóstico de engenharia completo, estruturado em quatro etapas complementares para isolar e compreender o impacto real das barreiras de desenvolvimento na árvore do DOM. A análise confronta os componentes do portal com as diretrizes internacionais da **WCAG 2.1 (Nível AA)** e com o **Artigo 63 da Lei Brasileira de Inclusão (LBI)**.

---

## 📊 2. Resumo das Ferramentas Executadas

| Etapa do Teste | Ferramenta Utilizada | Status / Avaliação | Escopo do Mapeamento |
| :---: | :--- | :--- | :--- |
| **1** | Teste Manual (Teclado `Tab` + NVDA) | 🔴 Crítico | Quebra na ordem lógica de foco e omissão de elementos interativos. |
| **2** | Extensão WAVE | 🔴 Crítico | **2 Erros Críticos (Botões Vazios)**, 0 Falhas de Contraste e 23 Alertas. |
| **3** | Extensão Axe DevTools | 🔴 Crítico | **1 Issue estrutural** de contraste crítico no botão principal de conversão. |
| **4** | Automação com **Cypress** | 🔴 Falha | Script automatizado interceptou a ausência de idioma na raiz do HTML. |

---

## 🔎 3. Detalhamento dos Achados por Etapa

### ⌨️ ETAPA 1: Testes Manuais Assistivos (Teclado & Leitor de Tela NVDA)
A validação humana sem o uso de mouse revelou barreiras que geram desorientação espacial e exclusão informativa:

1.  **Falha na Navegação por Teclado (Ordem de Foco):** Ao usar a tecla `Tab` para navegar na página, o foco salta e ignora seções inteiras de benefícios e ofertas. O fluxo de navegação sequencial é interrompido, tornando o conteúdo totalmente inacessível para usuários que não utilizam o mouse.
    *   *Impacto:* Usuários com deficiência motora ou visual são excluídos de informações sobre produtos e vantagens do banco.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 2.4.3 (Ordem de Foco - Nível A).

### 🌊 ETAPA 2: Varredura Automatizada Visual (Extensão WAVE)
A varredura visual de interface na seção Itaú Uniclass identificou não-conformidades de alto impacto na estrutura:

1.  **Botões sem Descrição Acessível (2 Empty buttons):** Identificação de 2 botões interativos flutuantes desprovidos de conteúdo textual ou rótulos, classificados formalmente como "Botões vazios". 
    *   *Impacto:* Leitores de tela não conseguem identificar a função desses componentes, anunciando apenas a palavra genérica "Botão", o que impede a interação e a busca de ajuda por usuários cegos.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 4.1.2 (Nome, Função, Valor - Nível A).
2.  **Alertas de Estrutura (23 Alerts):** Presença de textos alternativos redundantes e saltos na ordem hierárquica dos títulos (headings), gerando ruído na navegação sequencial.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.3.1 (Info and Relationships).
  
### Evidência:

<img width="1876" height="848" alt="Captura de tela 2026-08-06 174246" src="https://github.com/user-attachments/assets/94eda3e2-7ad8-4297-b306-4008a3dadc4f" />


### 📐 ETAPA 3: Inspeção Estrutural de Código (Extensão Axe DevTools)
A inspeção profunda do HTML revelou uma não-conformidade crítica de negócio localizada no principal elemento de conversão da interface (Botão de Call to Action):

1.  **Insuficiência de Contraste Cromático no Fluxo de Conversão — 1 ocorrência:** O botão principal "Abrir conta" apresenta uma relação de contraste de apenas 3.0:1 entre a fonte branca e o fundo laranja. A falha descumpre a taxa mínima exigida, prejudicando severamente a legibilidade para usuários com baixa visão ou ceratocone na porta de entrada de novos clientes.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 1.4.3 (Contraste - Nível AA).
  
### Evidência:

<img width="1898" height="817" alt="Captura de tela 2026-08-06 172235" src="https://github.com/user-attachments/assets/28ae7ccb-729e-4710-b30f-504b6d678508" />


### 🤖 ETAPA 4: Automação Contínua com Script (Cypress + `cypress-axe`)
Execução do script de teste focado na validação contínua da integridade semântica da árvore do DOM. Mesmo sob severa restrição de firewall e bloqueio de servidor (HTTP Status 403 / Access Denied), a automação contornou o bloqueio de renderização gráfica e capturou a seguinte violação na raiz do código:

1.  **Falta do Atributo de Idioma (`html-has-lang`) — 1 ocorrência:** Ausência completa do atributo de idioma na tag raiz do documento do portal.
    *   *Impacto:* Impede que tecnologias assistivas identifiquem a linguagem nativa do site, forçando sintetizadores de voz globais a processarem o conteúdo em português com fonéticas e sotaques estrangeiros inconsistentes e incompreensíveis.
    *   *Diretriz Violada:* WCAG 2.1 — Critério 3.1.1 (Idioma da Página - Nível A).
  
### Evidência:

<img width="1839" height="830" alt="Captura de tela 2026-08-06 173210" src="https://github.com/user-attachments/assets/61e10d64-4f85-4ac8-bf2d-09a7370f007d" />

---

## 💡 4. Diretrizes WCAG & Plano de Correção para a Engenharia

### 1. Declaração Estrutural e Idioma (HTML5):
*   **[Ajuste de Automação]** Injetar imediatamente o atributo de idioma correto na tag raiz do código do portal do Itaú (ex: `<html lang="pt-BR">`), garantindo compatibilidade e fonética perfeitas para leitores de tela globais.

### 2. Saneamento de Componentes e Controles (ARIA):
*   Adicionar o atributo `aria-label` para fornecer o contexto real da ação nos botões flutuantes identificados como vazios pelo WAVE.
    *   *Exemplo de Correção:* `<button type="button" aria-label="Abrir chat de ajuda"></button>`

### 3. Organização de Fluxo e Interface (DOM / CSS):
*   Revisar a hierarquia do DOM e garantir que todos os elementos interativos possuam posicionamento correto na ordem lógica da página, respeitando o fluxo sequencial do teclado.

### 4. Ajuste de Contraste Visual (Design/CSS):
*   **[Ajuste do Axe DevTools]** Corrigir a folha de estilos do botão principal de conversão "Abrir conta", alterando a paleta de cores para atingir o limite mínimo obrigatório de contraste de 4.5:1 exigido pela WCAG.

---

## 📊 5. Conclusão
A auditoria evoluída revelou que, embora o site apresente uma estrutura de base sólida, existem falhas de acessibilidade críticas na árvore do DOM e na camada visual de conversão. A implementação das correções sugeridas, unida à manutenção do script do Cypress como uma barreira de qualidade (Quality Gate), garantirá uma experiência digital fluida, inclusiva e em total conformidade legal para todos os usuários do Banco Itaú.
