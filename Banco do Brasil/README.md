# Relatório Técnico de Auditoria de Acessibilidade (A11y)
**Alvo:** Página Inicial do Banco do Brasil (bb.com.br)  
**Padrão de Referência:** WCAG 2.1 (Nível AA)  

---

## 1. Resumo Executivo
Esta auditoria técnica unificada avaliou a acessibilidade digital da página inicial do Banco do Brasil, combinando varreduras automatizadas recentes (WAVE e Axe DevTools) com testes manuais rigorosos focados na experiência de navegação por tecnologias assistivas (leitor de tela, navegação dinâmica por teclado, carrossel e acordeões/FAQ).

| Ferramenta / Método | Indicador / Métrica | Resultado / Status |
| :--- | :--- | :--- |
| **WAVE Evaluation Tool** | Erros Estruturais | **1 Erro** (Cabeçalho Vazio / *Empty heading*) |
| **WAVE Evaluation Tool** | Erros de Contraste | **10 Contrast Errors** (Contraste muito baixo) |
| **Axe DevTools (axe-core)** | Issues Automáticas | **12 Issues** (Focadas em proporção mínima de contraste - Gravidade *Serious*) |
| **Testes Manuais (Teclado)** | Menus Expansíveis (*Sanfonas*) | **Conformidade OK** (Validação correta com a tecla *Esc* e foco preservado) |
| **Testes Manuais (Leitor de Tela)** | Carrossel de Banners e Mídia | **Falhas Críticas** (Falta de pausa de autoplay e imagens sem rótulo) |
| **Testes Manuais (Leitor de Tela)** | Acordeões de FAQ (*Sanfonas*) | **Falha Crítica** (Rótulos repetitivos: leitor lê apenas "botão recolhido") |

---

## 2. Detalhamento Completo dos Achados e Não-Conformidades

### 🔴 Achado 01: Falhas de Contraste Mínimo de Cores (WAVE & Axe DevTools)
* **Critério WCAG:** 1.4.3 (Contraste Mínimo - Nível AA)
* **Severidade:** Séria (*Serious*)
* **Descrição:** As varreduras automatizadas identificaram divergências críticas de contraste. A ferramenta WAVE apontou **10 Contrast Errors**, enquanto o Axe DevTools mapeou **12 ocorrências** (issues automáticas) onde a proporção de contraste entre o texto e o fundo da página está abaixo do limite recomendado de 4.5:1 para textos normais.
* **Impacto:** Usuários com baixa visão, daltonismo ou que acessam a plataforma sob alta incidência de luz solar enfrentam grande dificuldade de leitura e fadiga visual rápida.

### 🟡 Achado 02: Presença de Cabeçalho Vazio (*Empty Heading*)
* **Critério WCAG:** 1.3.1 (Informações e Relações)
* **Severidade:** Moderada
* **Descrição:** A varredura do WAVE detectou **1 Erro** estrutural referente a tags de cabeçalho (`<h1>` a `<h6>`) desprovidas de conteúdo textual descritivo.
* **Impacto:** Leitores de tela utilizam a árvore de cabeçalhos para orientar a navegação rápida de usuários cegos. Elementos vazios geram ruídos de áudio e quebram a orientação espacial na página.

* ### Evidências:

<img width="1878" height="832" alt="Captura de tela 2026-07-23 182933" src="https://github.com/user-attachments/assets/d0452fde-6153-4878-8717-5cdcf8e57311" />

<img width="1911" height="794" alt="Captura de tela 2026-07-23 183937" src="https://github.com/user-attachments/assets/7aa08881-f989-40c2-8651-943f05bce923" />


### 🔴 Achado 03: Barreira Crítica no Carrossel de Banners (Autoplay e Semântica)
* **Critério WCAG:** 2.2.2 (Pausar, Parar, Ocultar) & 1.1.1 (Conteúdo Não Textual)
* **Severidade:** Crítica
* **Descrição:** Durante a navegação assistida por leitor de tela, identificou-se que o carrossel principal possui rotação automática acelerada (*autoplay*) sem um mecanismo de pausa acessível. Adicionalmente, há elementos gráficos com avisos de descrições ausentes e duplicação excessiva de links cruzados na transição dos slides.
* **Impacto:** O conteúdo rotativo desaparece rapidamente antes que o usuário com deficiência cognitiva ou baixa visão consiga processá-lo. Para o usuário cego, a falta de etiquetas textuais nas imagens gera confusão severa e perda de autonomia.

### 🔴 Achado 04: Falta de Contexto em Acordeões de FAQ (*Sanfonas*)
* **Critério WCAG:** 2.4.6 (Cabeçalhos e Rótulos) & 4.1.2 (Nome, Função, Valor)
* **Severidade:** Crítica
* **Descrição:** Na seção de perguntas frequentes, a navegação por leitor de tela resulta no anúncio repetitivo de *"botão recolhido"* sem associar a ação ao título da pergunta correspondente.
* **Impacto:** O usuário dependente de leitor de tela perde o contexto de qual pergunta está manipulando, tornando a interação confusa e inacessível.

### 🟢 Achado 05: Comportamento de Foco em Menus Expansíveis (*Sanfonas*)
* **Critério WCAG:** Boas Práticas de Navegação por Teclado
* **Status:** Validado / Conforme
* **Descrição:** Em testes manuais executados via teclado (teclas *Tab*, *Enter* e *Esc*), constatou-se que os menus suspensos respondem adequadamente ao comando de expansão e permitem o fechamento correto através da tecla *Esc*, devolvendo o foco ao elemento acionador.
* **Recomendação de Qualidade:** Documentar este comportamento como padrão a ser mantido em futuras atualizações de componentes de UI.

---

## 3. Recomendações de Remediação
* **Contraste:** Atualizar a paleta de cores dos elementos apontados pelo WAVE (10 erros) e pelo Axe DevTools (12 issues) para garantir conformidade estrita com o limiar WCAG AA (4.5:1).
* **Limpeza Semântica:** Remover ou preencher as tags de cabeçalho órfãs identificadas pelo WAVE.
* **Acessibilidade em Carrosséis:** Inserir um botão de controle de *Play/Pause* totalmente acessível via teclado e assegurar que todas as imagens dos slides contenham o atributo descritivo adequado.
* **Acordeões e FAQs:** Associar os botões de expansão aos seus respectivos títulos utilizando propriedades adequadas (`aria-expanded` e `aria-controls`), garantindo que o leitor de tela anuncie o contexto correto da pergunta.

---

## 4. Automação de Testes de Acessibilidade (Cypress)
*Espaço reservado para a implementação dos scripts de automação de testes voltados à validação de acessibilidade e regressão da interface do Banco do Brasil utilizando Cypress e axe-core.*
