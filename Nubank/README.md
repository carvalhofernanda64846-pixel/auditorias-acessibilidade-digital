# Relatório de Auditoria de Acessibilidade: Nubank Web

## 1. Objetivo e Metodologia
Esta auditoria teve como objetivo avaliar a conformidade de acessibilidade do portal web do Nubank com base nas diretrizes da **WCAG 2.1 (Web Content Accessibility Guidelines)**. Para garantir uma visão completa, utilizei uma abordagem híbrida:

*   **Análise Técnica (Automatizada):** Utilização do **axe-core (DevTools)** para validar a semântica do código e a estrutura ARIA.
*   **Análise Visual e de Design:** Utilização do **WAVE (WebAIM)** para identificar barreiras de contraste e legibilidade.
*   **Teste de Usabilidade (Manual):** Simulação de navegação por teclado (tecla Tab) e verificação da experiência com leitor de tela.

---

## 2. Barreiras Estruturais (Semântica e Código)

**Norma infringida:** **WCAG 2.1 - Critério 4.1.2 (Nome, Função, Valor)**. Este critério exige que componentes de interface tenham nomes acessíveis para serem interpretados corretamente por tecnologias assistivas.
  
*   **Print da evidência:**
  
  <img width="1898" height="814" alt="Captura de tela 2026-07-15 172751" src="https://github.com/user-attachments/assets/4d3f2170-fb3d-4bf9-984f-399ab9cdd67f" />

**Descrição do achado:** Identifiquei botões e links que não possuem descrição textual (nome acessível). Na prática, um usuário de leitor de tela ouve apenas "botão", sem saber qual a sua função (ex: "Transferir PIX").

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
3.  **Contraste:** Revisar a paleta de cores para garantir a relação mínima de 4.5:1 exigida pela WCAG 2.1.
4.  **Foco:** Implementar um contorno (outline) de foco com alto contraste para o indicador de teclado, garantindo visibilidade sobre o fundo roxo da marca.
