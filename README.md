# 🚧 Portfólio de Auditoria de Acessibilidade Digital

Olá! Seja bem-vindo ao meu portfólio especializado. Sou Analista de Qualidade (QA) focada em conformidade legal, regras de negócio e inclusão digital. 

Este repositório está sendo alimentado diariamente com laudos técnicos práticos de auditoria manual e funcional (Web e Mobile), utilizando as diretrizes globais da **WCAG** e o modelo nacional **eMAG**.

---

## 💻 Auditoria 01: Portal G1 (Globo)
* **Tipo:** Web Desktop
* **Ferramenta utilizada:** WAVE Evaluation Tool & Inspeção de Código
* **Foco do Teste:** Conteúdo Não Textual e Hierarquia

### 🔍 Bug 01: Imagem de Notícia sem Texto Alternativo (Falta de Atributo ALT)
* **O Problema:** Na página inicial do Portal G1, a imagem que ilustra a notícia *"Seria possível 'desarmar' um super El Niño..."* foi publicada sem a tag descritiva de acessibilidade.
* **Impacto no Usuário:** Pessoas com deficiência visual completa que utilizam leitores de tela (como o NVDA) não conseguem compreender o conteúdo visual. O sintetizador de voz anuncia apenas o nome técnico do arquivo de imagem, gerando uma experiência inacessível.
* **Diretriz Violada:** Critério de Sucesso WCAG 1.1.1 (Conteúdo Não Textual - Nível A).
* **Solução Proposta:** Adicionar o atributo `alt` descrevendo a foto.
* ### 📸 Evidência do Erro
*![print-el-nino](print-noticias-g1.png)
  `Exemplo: <img src="foto.jpg" alt="Satélite mostrando o planeta Terra com manchas de calor nos oceanos representando o El Niño.">`

### 🔍 Bug 02: Escudo de Seleção sem Texto Alternativo no Código
* **O Problema:** Na seção de esportes do G1, o gráfico que compõe a bandeira/escudo da Argentina e noruega foi inserido sem a tag descritiva no sistema.
* **Linha de Código com Defeito Detectada:** `<img class="crest" src="https://globo.com" loading="lazy">`
* **Impacto no Usuário:** O leitor de tela falha ao anunciar a identidade visual do time envolvido na notícia porque o programador não inseriu o atributo de acessibilidade.
* **Diretriz Violada:** Critério de Sucesso WCAG 1.1.1 (Conteúdo Não Textual - Nível A).
* **Solução Proposta:** Adicionar a tag `alt="Escudo da Argentina"` ou aplicar o atributo vazio `alt=""` caso a sigla "ARG" logo ao lado seja considerada suficiente para o contexto.
*  ### 📸 Evidência do Erro
*  ![Print do Placar da Copa](print-copa-g1.png)
*
