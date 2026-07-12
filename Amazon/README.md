# 📑 Laudo Técnico de Acessibilidade — Amazon Brasil

## 🔍 Informações da Auditoria
*   **Data:** 12/07/2026
*   **Página:** Home Page (amazon.com.br)
*   **Ferramenta Utilizada:** Axe DevTools (Painel do Desenvolvedor)

## ⚖️ Conformidade e Base Legal
Esta auditoria fundamenta-se nas diretrizes internacionais de acessibilidade **WCAG 2.1 (Web Content Accessibility Guidelines)** e no modelo nacional **eMAG (Modelo de Acessibilidade em Governo Eletrônico)**, em total conformidade com o **Artigo 63 da Lei Brasileira de Inclusão (Lei nº 13.146/2015)**.
---

## 👾 Bugs Identificados

### Bug 01 - Atributo ARIA inválido e não suportado na Barra de Pesquisa Principal
*   **Elemento afetado:** `#twotabsearchtextbox` (Campo de busca principal)
*   **Impacto no Usuário:** Crítico 🔴 (Impede ou confunde gravemente a navegação de usuários de leitores de tela)
*   **Diretriz WCAG Violada:** Critério de Sucesso 4.1.2 - Nome, Função, Valor (Robustez / Semântica Correta)
*   **Infração Legal:** Desconformidade com o Art. 63 da LBI por gerar barreiras tecnológicas de acesso ao consumo.

**Descrição do problema:**
O campo de busca principal da Amazon Brasil está configurado com o atributo `aria-expanded="false"`. Na especificação técnica do W3C, este atributo serve exclusivamente para indicar se um elemento expansível (como um menu ou sanfona/accordion) está aberto ou fechado. Como a barra de pesquisa possui a função de entrada de texto pura (`role="searchbox"`), o uso desse atributo é inválido. Isso confunde os leitores de tela (como NVDA ou JAWS), que anunciam ao usuário cego que há um menu para expandir ali, gerando uma quebra de expectativa e uma navegação confusa.

**Evidência do Erro (Print do Axe DevTools):**

<img width="1874" height="812" alt="Captura de tela 2026-07-12 122123" src="https://github.com/user-attachments/assets/be16600b-f17e-4563-95b2-946d7b9dcf6b" />

*   **Infração Legal:** Desconformidade com o Art. 63 da LBI por gerar barreiras tecnológicas no acesso ao comércio e consumo eletrônico.

**Solução Proposta:**
O time de engenharia de software da Amazon deve remover completamente o atributo `aria-expanded="false"` da tag `<input>` da barra de pesquisa, mantendo apenas os atributos padrão suportados para campos de texto.

