# Auditoria e Testes de Acessibilidade Digital (WCAG 2.1)
> **Alvo da Análise:** Landing Page — Poupança Premiada Sicoob 2026   
> **Metodologias:** Testes Manuais Assistivos (Teclado + Leitor de Tela) Varreduras Automatizadas (WAVE, axe-core / Axe DevTools) e automação de testes com Cypress (cypress-axe).

---

## 📋 1. Visão Geral do Projeto
Este repositório documenta a auditoria técnica de acessibilidade digital realizada na landing page oficial da campanha **Poupança Premiada Sicoob 2026**. O objetivo principal é identificar barreiras de navegação, falhas de inclusão e não-conformidades com os critérios internacionais da **WCAG 2.1 (Web Content Accessibility Guidelines - Nível AA)** e com a **Lei Brasileira de Inclusão (Lei nº 13.146/2015, Art. 63)**.

---

## 📊 2. Resumo das Métricas & AIM Score

| Ferramenta / Método | Métricas Mapeadas | Status / Nota | Impacto na Experiência |
| :--- | :--- | :--- | :--- |
| **AIM Score (WAVE WebAIM)** | **2.7 / 10** | 🔴 **Muito Crítico** | Indica alto impacto negativo para usuários com deficiência. |
| **WAVE Tool** | 11 Erros Críticos \| 52 Falhas de Contraste | 🔴 **Reprovado** | Barreiras diretas na leitura e na visualização. |
| **Axe DevTools** | 72 Problemas Graves (*Serious Issues*) | 🔴 **Reprovado** | Links inacessíveis, baixo contraste e regiões bloqueadas. |
| **Navegação Manual (NVDA + Tab)** | Seções e Banners Ignorados | 🔴 **Reprovado** | Pulo de etapas do tutorial, ausência de `alt text` e tabelas semânticas. |

---

## 🖐️ 3. Achados dos Testes Manuais (Teclado + Leitor de Tela NVDA)

Durante a navegação assistida por teclado (tecla `Tab` e setas) e leitor de tela NVDA, foram identificadas falhas severas de fluxo e conteúdo:

### A. Imagens Informativas e Banners sem Texto Alternativo (`alt`)
* **Banner Principal de Prêmios:** O leitor de tela ignora totalmente as informações visuais da campanha (3 Fiat Strada, 1 Hilux e motos Honda), bem como os textos da imagem (*"A cada R$ 200..."*, *"Mais de 2 milhões em prêmios"*).
* **Banner Poupança Kids:** O leitor de tela não descreve o elemento gráfico (4 porquinhos no parque) e não lê o texto (*"30 viagens para o Beto Carrero com seu filho"*).
* **Banner do App Sicoob:** O leitor não identifica o mockup visual do celular contendo a interface do aplicativo.

### B. Quebra de Fluxo e Passos de Instrução Ignorados
* **Passo a Passo "Como Participar":** O leitor ignora o card informativo *"A cada R$ 200 = 1 cupom"* e os 3 passos seguintes do tutorial, pulando direto para o botão *"Participe agora e comece a concorrer a prêmios!"*.
* **Alerta de Menores de Idade:** Logo após o botão de participação, o leitor ignora o texto de aviso (*"Atenção responsáveis: a participação de menores de idade na promoção só será efetivada após a aceitação do cadastro"*) e salta direto para o botão/link *"Clique aqui para preencher os dados do menor participante"*.
* **Passo a Passo "Como Abrir a Conta no App":** O leitor ignora os 5 passos do tutorial de abertura de conta pelo aplicativo e salta direto para o FAQ do rodapé.

### C. Tabelas, Consultas e Avisos Omitidos
* **Tabela do Período de Participação e Sorteios:** O leitor ignora completamente o aviso *"Atenção para as datas do sorteio e para o período de participação"* e pula toda a tabela estruturada com as datas de início e término dos períodos, privando o usuário de saber quando os sorteios acontecem.
* **Consulta de Números da Sorte:** O leitor não lê o título/instrução *"Consulte seus números da sorte"* e posiciona o foco diretamente dentro do campo *"Digite seu CPF ou CNPJ"*, seguido pelo botão *"Buscar"*.
* **Título de Descadastro:** O título da seção é ignorado, lendo apenas o link *"Clique aqui para fazer o descadastro"*.

## 🤖 4. Achados das Ferramentas Automatizadas

### 🔹 WAVE Web Accessibility Evaluation Tool
* **AIM Score:** **2.7 de 10**.
* **11 Erros Críticos:**
  * `1x Missing alternative text`: Imagem informativa sem atributo `alt`.
  * `10x Empty link`: Links que não possuem texto discernível ou identificável.
* **52 Erros de Contraste (`Contrast Errors`):** Proporções de cor de texto vs. fundo abaixo da taxa recomendada de **4.5:1** para textos normais.

  ### Evidência:
  
  <img width="1873" height="847" alt="Captura de tela 2026-07-24 173358" src="https://github.com/user-attachments/assets/b33f1a4a-bd13-4719-883b-fe7dcd13c442" />

### 🔹 Axe DevTools (axe-core)
* **72 Violations (Classificadas como SERIOUS):**
  * **61 Ocorrências de Baixo Contraste:** Risco alto de fadiga visual e inacessibilidade para daltônicos ou pessoas com baixa visão.
  * **10 Ocorrências de Links Sem Texto Discernível:** Impede o leitor de anunciar o destino do link.
  * **1 Ocorrência de Região com Scroll Sem Acesso por Teclado:** Seção de rolagem inacessível via tecla `Tab`.

 ### Evidência:

 <img width="1882" height="830" alt="Captura de tela 2026-07-24 173216" src="https://github.com/user-attachments/assets/86673ad2-e4e6-477a-b728-c176bcf0297f" />


## 📜 5. Diretrizes da WCAG e Legislação Afetada

As não-conformidades encontradas violam diretamente os seguintes critérios de sucesso da **WCAG 2.1 (Nível A e AA)** e normas legais:

| Critério WCAG | Nome da Regra | Nível | Descrição da Infração |
| :--- | :--- | :--- | :--- |
| **1.1.1** | *Non-text Content* | Nível A | Banners promocionais e informativos sem atributo `alt` equivalente. |
| **1.3.1** | *Info and Relationships* | Nível A | Falta de estrutura semântica em tabelas e tutoriais passo a passo. |
| **1.3.2** | *Meaningful Sequence* | Nível A | O leitor de tela pula blocos essenciais, alterando a ordem lógica de leitura. |
| **1.4.3** | *Contrast (Minimum)* | Nível AA | 52 a 61 elementos sem o contraste mínimo de 4.5:1. |
| **2.1.1** | *Keyboard* | Nível A | Regiões de scroll e passos de tutoriais inacessíveis via teclado. |
| **2.4.4** | *Link Purpose (In Context)* | Nível A | Presença de 10 links vazios/sem texto descritivo. |

> ⚖️ **Legislação Brasileira:** As falhas mapeadas descumprem a **Lei nº 13.146/2015 (Lei Brasileira de Inclusão - LBI)**, Art. 63, que estabelece ser **obrigatória a acessibilidade nos sítios da internet mantidos por órgãos ou entidades de administração pública e empresas privadas**.

---

## 💡 6. Sugestões de Melhoria

1. **Adicionar Textos Alternativos (`alt`):**
   * Preencher o atributo `alt` de todas as imagens informativas (ex: `alt="Banner da Promoção Poupança Premiada Sicoob 2026 exibindo prêmios como Hilux, Fiat Strada e motos Honda"`).
2. **Corrigir a Semântica do Passo a Passo:**
   * Estruturar os tutoriais (4 passos de participação e 5 passos do app) utilizando listas ordenadas `<ol>` e `<li>`, garantindo que os nós de texto estejam na árvore de acessibilidade do DOM.
3. **Adequação da Paleta de Cores (Contraste):**
   * Ajustar as cores de texto e botões para garantir a proporção mínima de contraste de **4.5:1** contra o fundo verde/amarelo.
4. **Rotular Links Vazios:**
   * Inserir textos visíveis ou atributos `aria-label` descritivos em todos os 10 links identificados como vazios pelo WAVE e Axe DevTools.
5. **Estrutura de Tabelas:**
   * Utilizar tags HTML5 nativas de tabela (`<table>`, `<thead>`, `<tbody>`, `<th>`, `<td>`) para a seção de datas dos sorteios, permitindo navegação via leitor de tela.

---

## 🚀 7. Próximos Passos
**Automação de Testes End-to-End de Acessibilidade com Cypress e `cypress-axe`** *(Etapa em desenvolvimento)*
