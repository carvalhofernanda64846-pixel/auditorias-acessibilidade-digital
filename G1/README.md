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
* <img width="667" height="210" alt="Captura de tela 2026-07-12 105824" src="https://github.com/user-attachments/assets/5ebe19e9-8d87-44e0-9529-8acbf186df9f" />


  `Exemplo: <img src="foto.jpg" alt="Satélite mostrando o planeta Terra com manchas de calor nos oceanos representando o El Niño.">`

### 🔍 Bug 02: Escudo de Seleção sem Texto Alternativo no Código
* **O Problema:** Na seção de esportes do G1, o gráfico que compõe a bandeira/escudo da Argentina e Noruega foi inserido sem a tag descritiva no sistema.
* **Linha de Código com Defeito Detectada:** `<img class="crest" src="https://globo.com" loading="lazy">`
* **Impacto no Usuário:** O leitor de tela falha ao anunciar a identidade visual do time envolvido na notícia porque o programador não inseriu o atributo de acessibilidade.
* **Diretriz Violada:** Critério de Sucesso WCAG 1.1.1 (Conteúdo Não Textual - Nível A).
* **Solução Proposta:** Adicionar a tag `alt="Escudo da Argentina"` ou aplicar o atributo vazio `alt=""` caso a sigla "ARG" logo ao lado seja considerada suficiente para o contexto.
*  ### 📸 Evidência do Erro
* <img width="896" height="707" alt="Captura de tela 2026-07-12 110135" src="https://github.com/user-attachments/assets/4b97a04b-a78a-4261-a3cf-2c22abec5f2e" />

