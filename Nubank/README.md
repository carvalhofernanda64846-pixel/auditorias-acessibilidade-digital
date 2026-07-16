# Relatório de Auditoria de Acessibilidade: Nubank Web

## 1. Objetivo e Metodologia
Esta auditoria teve como objetivo avaliar a conformidade de acessibilidade do portal web do Nubank com base nas diretrizes da **WCAG 2.1 (Web Content Accessibility Guidelines)**. Para garantir uma visão completa, utilizei uma abordagem híbrida:

*   **Análise Técnica (Automatizada):** Utilização do **axe-core (DevTools)** para validar a semântica do código e a estrutura ARIA.
*   **Análise Visual e de Design:** Utilização do **WAVE (WebAIM)** para identificar barreiras de contraste e legibilidade.
*   **Teste de Usabilidade (Manual):** Simulação de navegação por teclado (tecla Tab) e verificação da experiência com leitor de tela.

---

## 2. Barreiras Estruturais (Semântica e Código)

A auditoria automatizada realizada com a ferramenta axe-core identificou um total de 14 problemas de acessibilidade, classificados como barreiras técnicas na semântica e na estrutura do código.

**Norma infringida:** **WCAG 2.1 - Critério 4.1.2 (Nome, Função, Valor)**. Este critério exige que componentes de interface tenham nomes acessíveis para serem interpretados corretamente por tecnologias assistivas.
  
*   **Print da evidência:**
  
  <img width="1898" height="814" alt="Captura de tela 2026-07-15 172751" src="https://github.com/user-attachments/assets/4d3f2170-fb3d-4bf9-984f-399ab9cdd67f" />

**Descrição do achado:** Foram identificadas 14 violações que impactam a interpretação por tecnologias assistivas. Estas falhas englobam desde a falta de descrição textual em elementos interativos (como botões que são lidos apenas como 'botão' pelo leitor de tela), até erros no uso de atributos ARIA e na estrutura hierárquica do código (ex: elementos semânticos mal organizados). Esses pontos impedem uma navegação fluida e intuitiva para usuários com deficiência.

---

## 3. Barreiras Visuais (Contraste e Legibilidade)

*   **Norma infringida:** **WCAG 2.1 - Critério 1.4.3 (Contraste Mínimo)** e **Critério 2.4.7 (Foco Visível)**. O contraste insuficiente impede a leitura por pessoas com baixa visão, e a falta de foco visível impede a navegação por teclado.
   
*   **Print da evidência:**
    
  <img width="1888" height="814" alt="Captura de tela 2026-07-15 174515" src="https://github.com/user-attachments/assets/2cb00ae6-a8a4-4714-a7e5-6df5220e02f0" />

*   **Descrição do achado:** O design utiliza a cor roxa primária com fontes de baixo contraste. Adicionalmente, durante o teste manual com a tecla Tab, o indicador de foco torna-se imperceptível ao passar sobre elementos roxos, impedindo que o usuário saiba em qual botão está posicionado.

---

## 4. Relato de Usabilidade (Teste Humano)
*Como não é possível capturar em print a experiência sonora do leitor de tela, registro aqui a falha observada:*

*   **Falha identificada:** Durante a navegação manual, observei que diversos elementos interativos são ignorados pelo leitor de tela ou não possuem uma descrição clara de sua finalidade. Isso cria um "bloqueio de navegação", onde o usuário não consegue concluir tarefas básicas (como acessar o menu ou interagir com cartões) apenas pelo teclado.

---

## 💡 Sugestões de Melhoria

1.  **Semântica:** Adicionar atributos `aria-label` descritivos em todos os botões e links que utilizam apenas ícones.
2.  **Contraste:** Revisar a paleta de cores para garantir a relação mínima de 4.5:1 exigida pela WCAG 2.1.
3.  **Foco:** Implementar um contorno (outline) de foco com alto contraste para o indicador de teclado, garantindo visibilidade sobre o fundo roxo da marca.

## 5. 🚀 Automação de Testes de Acessibilidade

Para garantir a conformidade contínua, implementei testes automatizados utilizando **Cypress** e **cypress-axe**.

#### 🛠️ Tecnologias Adicionadas
*   **Cypress**: Framework para automação E2E.
*   **cypress-axe**: Plugin para auditoria de acessibilidade baseada nas diretrizes **WCAG (Web Content Accessibility Guidelines)**.

#### 📊 Relatório de Auditoria
Foram identificadas 48 violações na página inicial. Abaixo, a análise técnica das regras infringidas:

| Categoria | Ocorrências | Regra WCAG Infringida | Sugestão de Melhoria |
| :--- | :---: | :--- | :--- |
| `region` | 34 | WCAG 1.3.1 | Adicionar landmarks (ex: `<main>`) |
| `aria-prohibited` | 4 | WCAG 4.1.2 | Remover atributos ARIA inválidos |
| `heading-order` | 4 | WCAG 1.3.1 | Ajustar hierarquia de títulos |
| `link-name` | 4 | WCAG 2.4.4 | Adicionar descrição (aria-label) |
| `required-children` | 3 | WCAG 1.3.1 | Corrigir estrutura de elementos |
| `aria-allowed` | 1 | WCAG 4.1.2 | Ajustar roles permitidas |
| `command-name` | 1 | WCAG 4.1.2 | Nomear botões/comandos |
| `progressbar` | 1 | WCAG 1.3.1 | Adicionar rótulo em progressbar |
| `role-conflict` | 1 | WCAG 4.1.2 | Corrigir conflitos de role |

> **Nota Técnica:** A alta incidência da regra `region` indica uma falha na estrutura semântica global, cuja correção trará um impacto positivo imediato para usuários de leitores de tela.

### Evidência da execução dos testes automatizados via Cypress/axe

<img width="1790" height="746" alt="Captura de tela 2026-07-16 113810" src="https://github.com/user-attachments/assets/5a43c607-4132-4849-b64c-344287b958c3" />

