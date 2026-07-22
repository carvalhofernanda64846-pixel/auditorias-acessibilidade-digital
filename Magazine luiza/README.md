# 🔍 Auditoria de Acessibilidade (A11y) - Magazine Luiza (Home)

Relatório de auditoria de acessibilidade web realizado na página inicial (Home) do e-commerce da **Magazine Luiza**, combinando **análise automatizada** (Axe DevTools e WAVE) com **testes manuais e exploratórios** utilizando leitor de tela e navegação por teclado (`TAB`).

---

## 🎯 Objetivo
Avaliar a conformidade de acessibilidade da plataforma com base nas diretrizes internacionais **WCAG 2.1 (Web Content Accessibility Guidelines)**, na **Lei Brasileira de Inclusão (LBI - Lei nº 13.146/2015)** e no **Decreto nº 5.296/2004**, identificando barreiras que dificultam ou impedem o acesso de pessoas com deficiência.

---

## 🛠️ Ferramentas Utilizadas
* **Testes Manuais:** Leitor de tela (NVDA/TalkBack) e navegação estruturada por teclado (`TAB`).
* **Ferramentas Automatizadas:** 
  * **Axe DevTools:** Mapeamento estrutural e de contraste (identificou **7 erros** no total, focados em conformidade de contraste mínimo de cores).
  * **WAVE (Web Accessibility Evaluation Tool):** Identificação de erros de elementos, botões e alertas (identificou **6 erros de botões vazios / Empty Buttons** e **8 erros de contraste / Very Low Contrast**).

---

## 📋 Resumo dos Achados, Impactos e Leis Infringidas

### 1. 🤖 Achados de Automação (WAVE & Axe DevTools)
* **Erros de Botões Vazios (*Empty Buttons* - 6 encontrados no WAVE):** 
  * *Impacto:* Botões interativos sem rótulo de texto impedem que tecnologias assistivas identifiquem a função do elemento.
  * *Leis e Critérios Infringidos:* 
    * **WCAG 2.1 - Critério 4.1.2 (Nome, Função e Valor - Nível A):** Componentes de interface precisam ter nome e função programaticamente determináveis.
    * **LBI (Lei nº 13.146/2015) - Artigo 63:** Torna obrigatória a acessibilidade nos sítios eletrônicos da rede mundial de computadores para uso da pessoa com deficiência.
* **Erros de Contraste (*Low Contrast* - 7 encontrados no Axe DevTools e 8 no WAVE):** 
  * *Impacto:* Dificuldade ou impossibilidade de leitura para usuários com baixa visão ou daltonismo devido ao limite inadequado da proporção de cores.
  * *Leis e Critérios Infringidos:* 
    * **WCAG 2.1 - Critério 1.4.3 (Contraste Mínimo - Nível AA):** O texto e imagens de texto devem ter uma relação de contraste de pelo menos 4.5:1.

> **📸 Evidências**
> 
<img width="1894" height="852" alt="Captura de tela 2026-07-22 110339" src="https://github.com/user-attachments/assets/6362af2c-a0d6-427e-8b1a-1119796e7826" />

<img width="1911" height="721" alt="Captura de tela 2026-07-22 111030" src="https://github.com/user-attachments/assets/b89db3d5-b4b6-473d-a9d9-d905ff3ada14" />


### 2. 👁️ Achados Críticos do Teste Manual (Leitor de Tela e Teclado)
As ferramentas automatizadas não detectam falhas de fluxo e experiência de navegação real, que foram descobertas através da exploração manual:

* **Inversão na Ordem de Leitura (Fluxo do Leitor de Tela):**
  * *O problema:* O leitor inicia a leitura pelos blocos inferiores, sobe de forma invertida para a primeira linha e depois salta novamente, evidenciando falha na árvore do DOM e na hierarquia (`H1`/`H2`).
  * *Leis e Critérios Infringidos:*
    * **WCAG 2.1 - Critério 1.3.1 (Informações e Relações - Nível A):** A informação, estrutura e relações transmitidas através da apresentação devem ser passíveis de serem lidas por software (ordem de leitura programática).
    * **WCAG 2.1 - Critério 2.4.3 (Ordem de Foco - Nível A):** Se uma página puder ser navegada sequencialmente e a ordem de navegação afetar o significado ou a operação, os componentes focáveis devem receber foco na ordem que preserve o significado.

* **Banners Promocionais e Patrocinados Sem Contexto ("10k home"):**
  * *O problema:* O leitor de tela vocaliza apenas metadados internos ou códigos genéricos (ex: *"Abrir oferta patrocinada, 10k home, 9 link"*), deixando o usuário cego sem saber qual é o produto ou desconto.
  * *Leis e Critérios Infringidos:*
    * **WCAG 2.1 - Critério 1.1.1 (Conteúdo Não Textual - Nível A):** Todo conteúdo não textual apresentado ao usuário deve possuir uma alternativa em texto equivalente.
    * **WCAG 2.1 - Critério 2.4.4 (Propósito do Link - Nível A):** O propósito de cada link deve ser determinável pelo texto do link isoladamente ou pelo texto do link juntamente com o contexto do link.
    * **LBI (Lei nº 13.146/2015) - Artigo 63, Parágrafo Único:** Os sítios eletrônicos devem exibir o símbolo de acessibilidade em destaque.

* **Armadilha de Foco e Falha na Sanfona de Busca (*Focus Trap / State Management*):**
  * *O problema:* Ao acionar a busca, a caixa expansível abre, mas o menu permanece estático e aberto na tela mesmo após o usuário navegar via `TAB` por todo o site, quebrando o contexto.
  * *Leis e Critérios Infringidos:*
    * **WCAG 2.1 - Critério 2.1.2 (Sem Armadilha de Teclado - Nível A):** Se o foco do teclado puder ser movido para um componente usando um mecanismo de teclado, o foco deve poder ser movido para fora desse componente.
    * **WCAG 2.1 - Critério 3.2.1 (Em Foco - Nível A):** Quando qualquer componente recebe foco, isso não deve iniciar uma mudança de contexto de forma inesperada.

---

## 💡 Recomendações de Correção 
1. **Reestruturação do DOM:** Ajustar a semântica do código HTML e a ordem lógica de foco (`Tab Order`) para atender estritamente aos critérios **1.3.1** e **2.4.3** da WCAG.
2. **Atributos ARIA e Textos Alternativos:** Inserir descrições claras via `aria-label` ou texto alternativo em banners e links patrocinados, sanando as violações do critério **1.1.1** e **2.4.4**.
3. **Gerenciamento de Foco (Modais/Menus):** Implementar lógica para fechar o componente de busca expansível ao perder o foco ou utilizar corretamente o atributo `aria-expanded`, garantindo conformidade com o critério **2.1.2**.
4. **Correção de Contraste:** Adequar a paleta de cores para cumprir o critério **1.4.3 (Nível AA)** mapeado pelas ferramentas de varredura.

---

## 🚀 Próximos Passos
* [ ] Incluir testes automatizados de acessibilidade integrados.
* [ ] Consolidar os dados desta auditoria em formato PDF para portfólio profissional.
*
