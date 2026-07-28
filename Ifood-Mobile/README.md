# 📱 Auditoria e Testes de Acessibilidade Digital Mobile (WCAG 2.1/2.2)

## 🎯 Alvo da Análise: Aplicativo iFood (Android)
*   **Varredura Automatizada:** Executada na **Página Inicial (Home)** usando o Scanner de Acessibilidade do Google.
*   **Testes Manuais Assistivos:** Executados na **Página de Busca** usando o Leitor de Tela TalkBack.  
*   **Dispositivo de Teste:** Samsung Galaxy (Android Nativo).

---

## 📋 1. Visão Geral do Projeto
Este repositório documenta a auditoria técnica de acessibilidade digital realizada no aplicativo móvel do **iFood** para Android. A análise foi dividida estrategicamente em duas etapas: uma validação automatizada na porta de entrada do app (Página Inicial) e um teste manual focado na experiência de navegação do usuário (Página de Busca).

O objetivo é identificar barreiras de uso para pessoas com deficiência visual ou baixa visão, mapear as excelentes práticas encontradas e garantir a conformidade com las diretrizes da **WCAG 2.1/2.2 (Nível AA)** e com a **Lei Brasileira de Inclusão (Lei nº 13.146/2015, Art. 63)**.

---

## 📊 2. Resumo das Métricas por Tela

| Tela Analisada | Método Utilizado | Status / Avaliação | Impacto na Experiência |
| :--- | :--- | :--- | :--- |
| **Página Inicial (Home)** | Scanner de Acessibilidade (Google) | 🟡 Regular | 16 Sugestões de Melhoria mapeadas e agrupadas por categorias de falhas. |
| **Página de Busca** | Leitor de Tela (TalkBack) | 🟢 Excelente | Estrutura nativa impecável, leitura lógica e navegação fluida. |

---

## 🔎 3. Achados da Varredura Automatizada (Na Página Inicial)

A ferramenta automatizada do Google gerou **16 sugestões de melhoria** na interface da Home. Na engenharia de QA, essas 16 ocorrências brutas são agrupadas em **3 categorias de falhas técnicas principais**:

### A. Rótulo de Tipo de Item Redundante (Categorias de Imagens e Banners)
*   **O Bug:** No banner promocional principal, o desenvolvedor incluiu a instrução de ação física do sistema (*"...ou toque duas vezes para ver mais detalhes"*) direto no texto descritivo do componente.
*   **O Problema:** Como o TalkBack já adiciona automaticamente a frase *"toque duas vezes para ativar"* ao final de elementos clicáveis, a fala fica repetitiva e confusa para o usuário cego.
*   **Critério WCAG Afetado:** 4.1.2 (Name, Role, Value).
  
  ### Evidência:
  
<img width="540" height="1204" alt="WhatsApp Image 2026-07-27 at 9 48 00 AM" src="https://github.com/user-attachments/assets/f6598ae4-176a-42ab-9281-a2aabffc4129" />


### B. Múltiplas Ocorrências de Baixo Contraste Crítico (Textos e Alertas)
*   **O Bug:** Textos de cupons premiados e detalhes de frete/distância utilizam cores que competem com o fundo ou com ilustrações da tela.
*   **O Problema:** A proporção de cor quebra a regra de contraste mínimo de **4.5:1**, gerando fadiga visual e dificultando o acesso de pessoas com baixa visão. O Scanner detecta cada elemento com cor fraca de forma individual, inflando o número total de alertas.
*   **Critério WCAG Afetado:** 1.4.3 (Contrast - Minimum).

  ### Evidência:
  
<img width="540" height="1204" alt="WhatsApp Image 2026-07-27 at 9 42 21 AM" src="https://github.com/user-attachments/assets/59987770-3ec9-4612-9074-eab98f30a33d" />


### C. Elementos de Interface com Zona de Toque Reduzida (Botões Pequenos)
*   **O Bug:** Múltiplos ícones de atalhos e botões menores de serviços parceiros possuem uma área de clique inferior ao recomendado pelo Google.
*   **O Problema:** Viola as boas práticas de usabilidade física, dificultando a navegação de usuários com tremores nas mãos, dificuldades motoras ou que usam o celular em movimento.
*   **Critério WCAG Afetado:** 2.5.5 (Target Size - Nível AAA, mas avaliado como melhoria contínua).

---

## 🌟 4. Achados dos Testes Manuais & Casos de Sucesso (Na Página de Busca)

Ao contrário da página inicial, a Tela de Busca do iFood apresentou um **padrão de excelência e alta conformidade** na experiência real com o TalkBack:

### A. Campo de Busca Comunicativo
*   **Comportamento:** O campo anuncia perfeitamente a sua função (*"Caixa de edição, pesquise por prato ou restaurante"*). Ao ser ativado com dois toques, ele expande a experiência informando *"O que vai pedir hoje?"* e abre o teclado do Android de forma 100% nativa.
*   **Critério Atendido:** WCAG 4.1.2 (Name, Role, Value).

### B. Descrição Perfeita de Elementos Não-Textuais (Banner Coca-Cola)
*   **Comportamento:** O banner interno da Coca-Cola na aba de buscas descreve com precisão cirúrgica a imagem, o símbolo e as frases promocionais escritas na peça gráfica, dando total autonomia para o usuário cego.
*   **Critério Atendido:** WCAG 1.1.1 (Non-text Content).

### C. Menu de Navegação Inferior (Bottom Navigation) e Filtros
*   **Comportamento:** O leitor de tela anuncia as abas informando a posição lógica exata (ex: *"Busca, aba 2 de 4, tocar duas vezes para selecionar"*). Os botões de filtros ("Árabes", "Pizza") também são lidos na sequência correta de leitura.
*   **Critério Atendido:** WCAG 1.3.2 (Meaningful Sequence).

---

## 📜 5. Diretrizes WCAG e Legislação Impactada

| Critério WCAG | Nome da Regra | Nível | Contexto Temático no App |
| :---: | :--- | :---: | :--- |
| **1.1.1** | Non-text Content | A | Cumprido na Busca (Coca-Cola), mas falha na Página Inicial (Rock in Rio). |
| **1.4.3** | Contrast (Minimum) | AA | Alerta de cupons da Página Inicial com proporção abaixo de 4.5:1. |
| **4.1.2** | Name, Role, Value | A | Rótulo do banner da Página Inicial inserindo texto manual de ação física. |

⚖️ **Legislação Brasileira:** Os pontos de sucesso mapeados na Busca mostram o forte compromisso do iFood com a **Lei nº 13.146/2015 (LBI), Art. 63**, restando apenas pequenos ajustes finos na camada de desenvolvimento da Página Inicial para zerar as barreiras.

---

## 💡 6. Sugestões de Melhoria (Como Corrigir)

1.  **Ajuste no Código da Página Inicial (Banner):**
    No código nativo do Android (`XML` ou `Jetpack Compose`), remova o texto *"toque duas vezes"* do atributo `contentDescription`. Deixe apenas o texto informativo do banner (ex: `android:contentDescription="Promoção iFood Rock in Rio: seu pedido no app pode virar ingressos"`). O sistema operacional cuida da instrução de clique sozinho.
    
3.  **Correction de Contraste na Página Inicial:**
    Modificar a cor da fonte ou aplicar um fundo sólido de alto contraste atrás do texto de alerta de cupons na Home para atingir a taxa mínima de 4.5:1.
    
5.  **Expansão da Zona de Clique:**
    Garantir que todos os componentes interativos do menu da Home possuam uma área de toque mínima de **48x48 dp**, inserindo espaçamentos (*paddings*) invisíveis se necessário.

---
