# 📑 Relatório de Auditoria de Acessibilidade (WCAG) - Home Mercado Livre

Este relatório consolida os achados da avaliação de acessibilidade realizada na página inicial do Mercado Livre, seguindo a ordem exata de mapeamento da ferramenta automatizada Axe DevTools combinada com testes manuais.

---

## 🛠️ Resumo Técnico da Varredura
* **Ferramenta Utilizada:** Axe DevTools
* **Total de Erros Automatizados:** 46 vulnerabilidades sérias (Serious)

---

## 1. [Acessibilidade - Contraste] Elements must meet minimum color contrast ratio thresholds (42 ocorrências)

### 🔍 Descrição do Bug
A varredura automatizada identificou 42 pontos de falha onde elementos de texto e componentes de interface não possuem a proporção de contraste mínima exigida por lei contra o plano de fundo. 

*Nota de teste manual:* Durante a navegação por teclado, esse problema de contraste se torna crítico no **Carrossel de Banners Principais (Banner Amarelo)**, onde o indicador de foco (`outline` azul padrão) perde totalmente o contraste contra o fundo vibrante, tornando-se visualmente invisível.

### 🎯 Impacto
Dificulta ou impede completamente a leitura de informações e a identificação de elementos selecionados por usuários com baixa visão, daltonismo ou sob condições de forte iluminação na tela.

### 🕹️ Passos para Reproduzir
1. Acessar a página inicial do Mercado Livre.
2. Abrir o Inspetor de Elementos (`F12`) e rodar a varredura na aba do Axe DevTools.
3. Observar a primeira categoria listada com 42 falhas de taxa de contraste.
4. Para o teste manual do foco: Navegar com a tecla `TAB` até o banner principal amarelo e notar a perda de contraste do indicador azul.

### 📸 Evidência Visual

<img width="1864" height="765" alt="Captura de tela 2026-07-12 165506" src="https://github.com/user-attachments/assets/94e69cbb-def9-4267-a359-d4f2c6596a12" />



## 2. [Acessibilidade - Cores] Links must be distinguishable without relying on color (1 ocorrência)

### 🔍 Descrição do Bug
O robô identificou que existe um ou mais links na página que se diferenciam do texto comum apenas pela cor do texto, sem apresentar nenhuma outra marcação gráfica (como sublinhado).

### 🎯 Impacto
Usuários daltônicos ou com restrições visuais não conseguem identificar que o texto em questão se trata de um link clicável, pois não percebem a diferença de cor.

### 🕹️ Passos para Reproduzir
1. Analisar a segunda linha de erros do Axe DevTools na Home do Mercado Livre.
2. Clicar na categoria correspondente e utilizar a função *Highlight* para localizar o elemento na página.

### 📸 Evidência Visual

<img width="1863" height="817" alt="Captura de tela 2026-07-12 163825" src="https://github.com/user-attachments/assets/d8a93c26-c83d-4fab-9efa-d604da62dca8" />

---

## 3. [Acessibilidade - Estrutura] <ul> and <ol> must only directly contain <li>, <script> or <template> elements (2 ocorrências)

### 🔍 Descrição do Bug
A estrutura de código HTML de duas listas na página inicial está incorreta. Foram inseridas tags inválidas diretamente dentro de elementos de lista (`<ul>` ou `<ol>`), violando as regras semânticas da web.

### 🎯 Impacto
A árvore de acessibilidade do navegador é corrompida. Quando um leitor de telas tenta ler essa lista para um usuário cego, ele pode anunciar o conteúdo de forma confusa, incompleta ou ignorar elementos importantes.

### 🕹️ Passos para Reproduzir
1. Analisar a terceira linha de erros do relatório do Axe DevTools.
2. Expandir o item para identificar as duas tags de lista que contêm elementos filhos inválidos no código fonte.

### 📸 Evidência Visual

<img width="1908" height="803" alt="Captura de tela 2026-07-12 163918" src="https://github.com/user-attachments/assets/e7c93506-28a7-4b9e-b5e1-bd7a0c828a3e" />

<img width="1860" height="808" alt="Captura de tela 2026-07-12 164015" src="https://github.com/user-attachments/assets/f04d521a-34ff-4d4c-a7dc-fec8f44abe07" />


---

## 4. [Acessibilidade - Teclado] Scrollable region must have keyboard access (1 ocorrência)

### 🔍 Descrição do Bug
O componente de carrossel de benefícios do "Meli+" (`class="andes-carousel-free"`) possui conteúdo dinâmico estruturado em uma região de rolagem horizontal. No entanto, a estrutura utilizada impede que o foco do teclado entre nessa área de scroll, ignorando o bloco completamente durante a navegação por `TAB`.

### 🎯 Impacto
Usuários que dependem exclusivamente do teclado ficam impossibilitados de rolar a seção para o lado, perdendo o acesso aos benefícios ocultos do plano e aos cards interativos.

### 🕹️ Passos para Reproduzir
1. Analisar a quarta e última linha de erros do painel do Axe DevTools.
2. Utilizar a tecla `TAB` manualmente descendo pela página até a seção do Meli+.
3. Verificar que o foco pula por cima do quadrado rolável (destacado em roxo pelo *Highlight* da ferramenta), impossibilitando o scroll horizontal através das setas direcionais ($\leftarrow$ e $\rightarrow$).

### 💻 Elemento Identificado (Código)
```html
<div class="andes-carousel-free" id="_r_1_"> ... </div>

### 📸 Evidência Visual

<img width="1882" height="767" alt="Captura de tela 2026-07-12 164058" src="https://github.com/user-attachments/assets/65755061-c5bc-457b-a828-f7c7e94d7d01" />



