# 📑 Relatório de Auditoria de Acessibilidade (WCAG) - Home Mercado Livre

Este relatório consolida os achados da avaliação de acessibilidade realizada na página inicial do Mercado Livre, seguindo a ordem exata de mapeamento da ferramenta automatizada Axe DevTools combinada com testes manuais de teclado.

---

## 🛠️ Resumo Técnico da Varredura
* **Ferramenta Utilizada:** Axe DevTools (Versão Gratuita)
* **Total de Erros Automatizados:** 46 vulnerabilidades sérias (Serious)
* **Padrão de Conformidade:** WCAG 2.1 AA / LBI (Lei Brasileira de Inclusão)

---

## 1. [Acessibilidade - Contraste] Elements must meet minimum color contrast ratio thresholds (42 ocorrências)

### 🔍 Descrição do Bug
A varredura automatizada identificou 42 pontos de falha onde elementos de texto e componentes de interface não possuem a proporção de contraste mínima exigida contra o plano de fundo. 

*Nota de teste manual:* Durante a navegação por teclado, esse problema de contraste se torna crítico no **Carrossel de Banners Principais (Banner Amarelo)**, onde o indicador de foco perde totalmente o contraste contra o fundo vibrante, tornando-se visualmente invisível.

### 🎯 Impacto
Dificulta ou impede completamente a leitura de informações e a identificação de elementos selecionados por usuários com baixa visão, daltonismo ou sob condições de forte iluminação/reflexo na tela do computador.

### 🕹️ Passos para Reproduzir
1. Acessar a página inicial do Mercado Livre.
2. Abrir o Inspetor de Elementos (F12) e rodar a varredura na aba do Axe DevTools.
3. Observar a primeira categoria listada com 42 falhas de taxa de contraste.
4. Para o teste manual do foco: Navegar com a tecla TAB até o banner principal amarelo e notar a perda de contraste do indicador azul.

### ⚖️ Diretrizes e Leis Violadas
* **WCAG 2.1 - Critério de Sucesso 1.4.3:** Contraste Mínimo (Nível AA).
* **WCAG 2.1 - Critério de Sucesso 1.4.11:** Contraste de Componentes de Interface Não Textuais (Nível AA).
* **WCAG 2.1 - Critério de Sucesso 2.4.7:** Foco Visível (Nível AA).
* **Legislação Brasileira:** Artigo 63 da Lei nº 13.146 (Lei Brasileira de Inclusão - LBI).

### 🚀 Sugestão de Melhoria e Resultado Esperado
Todos os textos e links devem passar por uma revisão da paleta de cores para atingir o contraste mínimo de 4.5:1. Para o foco do teclado no banner, sugere-se a aplicação de um estilo CSS customizado para destacar o elemento do fundo amarelo.

### 📸 Evidência Visual:

<img width="1864" height="765" alt="Captura de tela 2026-07-12 165506" src="https://github.com/user-attachments/assets/87e1e497-5abb-47e3-bbe0-d1d267f3ccdd" />

---

## 2. [Acessibilidade - Cores] Links must be distinguishable without relying on color (1 ocorrência)

### 🔍 Descrição do Bug
O robô identificou que existe link na página que se diferencia do texto comum apenas pela mudança na cor do texto, sem apresentar nenhuma outra marcação gráfica complementar.

### 🎯 Impacto
Anuncia barreiras para usuários daltônicos ou usuários com restrições visuais severas, visto que eles não conseguem identificar que o texto se trata de um elemento clicável por dependerem apenas da cor.

### 🕹️ Passos para Reproduzir
1. Analisar a segunda linha de erros do Axe DevTools na Home do Mercado Livre.
2. Clicar na categoria correspondente para expandir o erro.

### 💻 Elemento Identificado (Código):
**Tag HTML afetada:** `<a class="nav-header-link" href="...">...</a>`

### ⚖️ Diretrizes e Leis Violadas
* **WCAG 2.1 - Critério de Sucesso 1.4.1:** Uso de Cores (Nível A).
* **Legislação Brasileira:** Decreto nº 5.296/2004 (Direito de acesso à informação e eliminação de barreiras digitais).

### 🚀 Sugestão de Melhoria e Resultado Esperado
Garantir que todos os links inseridos no meio de blocos de texto possuam o sublinhado padrão ativo (text-decoration: underline) ou fiquem com formatação em negrito, permitindo a identificação do elemento clicável por meio da forma e não apenas da cor.

### 📸 Evidência Visual:

<img width="1863" height="817" alt="Captura de tela 2026-07-12 163825" src="https://github.com/user-attachments/assets/2c8ebc3f-be9b-41de-b5be-e3686b424460" />


## 3. [Acessibilidade - Estrutura] ul and ol must only directly contain li, script or template elements (2 ocorrências)

### 🔍 Descrição do Bug
A estrutura de código HTML de duas listas na página inicial está incorreta. Foram inseridas tags inválidas diretamente dentro do elemento
da lista (`<ul> ou <ol>`), quebrando a semântica correta do código.

### 🎯 Impacto
A árvore de acessibilidade do navegador é corrompida. Quando um software de leitura de tela (como o NVDA) processa essa área, ele pode anunciar o conteúdo de forma truncada ou pular informações vitais para o usuário cego.

### 🕹️ Passos para Reproduzir
1. Analisar a terceira linha de erros do relatório do Axe DevTools.
2. Expandir o item para identificar a tag inválida que foi colocada incorretamente dentro da lista.

### 💻 Elemento Identificado (Código):
**Estrutura identificada:** `<ul class="nav-header-list"> <div class="invalid-child-element">...</div> </ul>`

### ⚖️ Diretrizes e Leis Violadas
* **WCAG 2.1 - Critério de Sucesso 1.3.1:** Informações e Relações (Nível A).
* **Modelo de Acessibilidade em Governo Eletrônico (eMAG):** Diretriz de Marcação Correta e Semântica.

### 🚀 Sugestão de Melhoria e Resultado Esperado
Corrigir a estrutura do código para garantir que a lista contenha apenas itens de lista (`tags <li>`) imediatamente dentro dela, sem outros elementos intermediários.

### 📸 Evidência Visual:

<img width="1908" height="803" alt="Captura de tela 2026-07-12 163918" src="https://github.com/user-attachments/assets/9b7e3205-2b84-4a79-9b50-353a0abece4c" />



<img width="1860" height="808" alt="Captura de tela 2026-07-12 164015" src="https://github.com/user-attachments/assets/571c778e-245e-404e-bca4-10ef1d744f2f" />


---

## 4. [Acessibilidade - Teclado] Scrollable region must have keyboard access (1 ocorrência)

### 🔍 Descrição do Bug
O componente de carrossel de benefícios do Meli+ possui conteúdo estruturado em uma região de rolagem horizontal. Contudo, a estrutura de código utilizada impede que o foco do teclado entre ou interaja com essa área, ignorando o bloco completamente durante a navegação sequencial por TAB.

### 🎯 Impacto
Usuários que dependem estritamente da navegação por teclado ficam impossibilitados de interagir ou rolar o componente para o lado para ler os benefícios ocultos do plano, gerando uma barreira de navegação intransponível.

### 🕹️ Passos para Reproduzir
1. Analisar a quarta e última linha de erros do painel do Axe DevTools.
2. Utilizar a tecla TAB manualmente descendo pela página até a seção do Meli+.
3. Verificar que o foco pula por cima do quadrado rolável, impossibilitando o scroll horizontal através das setas direcionais.

### 💻 Elemento Identificado (Código):
**Tag HTML identificada:** `<div class="andes-carousel-free" id="_r_1_"> ... </div>`

### ⚖️ Diretrizes e Leis Violadas
* **WCAG 2.1 - Critério de Sucesso 2.1.1:** Teclado (Nível A).
* **WCAG 2.1 - Critério de Sucesso 2.4.3:** Ordem do Foco (Nível A).
* **Legislação Brasileira:** Artigo 63 da LBI (Garantia de pleno acesso a recursos interativos na web de forma autônoma).

### 🚀 Sugestão de Melhoria e Resultado Esperado
Adicionar o atributo tabindex="0" no elemento contêiner div do carrossel (class="andes-carousel-free"). Isso incluirá a região de rolagem na ordem natural de tabulação da página, permitindo que o usuário dê foco na área e utilize as setas direcionais do teclado para rolar os cards livremente.

### 📸 Evidência Visual:

<img width="1882" height="767" alt="Captura de tela 2026-07-12 164058" src="https://github.com/user-attachments/assets/0f946873-2142-4a90-820e-1c856f8b7e07" />
