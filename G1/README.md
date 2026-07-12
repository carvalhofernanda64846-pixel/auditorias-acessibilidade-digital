## 💻 Auditoria 01: Portal G1 (Globo)
* **Tipo:** Web Desktop
* **Ferramenta utilizada:** WAVE Evaluation Tool & Inspeção de Código
* **Foco do Teste:** Conteúdo Não Textual e Hierarquia
  
* ## ⚖️ Conformidade e Base Legal
Esta auditoria fundamenta-se nas diretrizes internacionais de acessibilidade **WCAG 2.1 (Web Content Accessibility Guidelines)** e no modelo nacional **eMAG (Modelo de Acessibilidade em Governo Eletrônico)**. O laudo está em total conformidade com o **Artigo 63 da Lei Brasileira de Inclusão (Lei nº 13.146/2015)**, que estabelece a obrigatoriedade de acessibilidade nos sítios da internet mantidos por empresas com sede ou representação comercial no País.

### 🔍 Bug 01: Imagem de Notícia sem Texto Alternativo (Falta de Atributo ALT)
* **O Problema:** Na página inicial do Portal G1, a imagem que ilustra a notícia *"Seria possível 'desarmar' um super El Niño..."* foi publicada sem a tag descritiva de acessibilidade.
* **Impacto no Usuário:** Pessoas com deficiência visual completa que utilizam leitores de tela (como o NVDA) não conseguem compreender o conteúdo visual. O sintetizador de voz anuncia apenas o nome técnico do arquivo de imagem, gerando uma experiência inacessível.
* **Diretriz Violada:** Critério de Sucesso WCAG 1.1.1 (Conteúdo Não Textual - Nível A).
* **Solução Proposta:** Adicionar o atributo `alt` descrevendo a foto.
* ### 📸 Evidência do Erro
<img width="667" height="210" alt="Captura de tela 2026-07-12 105824" src="https://github.com/user-attachments/assets/c1e2fb83-1ddc-4bfd-8048-368da1ab04bb" />

**Solução Proposta:**
O time de desenvolvimento do G1 deve adicionar o atributo `alt` preenchido com uma descrição clara e concisa dentro da tag da imagem. Exemplo de correção: `<img src="link-da-imagem.jpg" alt="Mapa do Brasil mostrando o aquecimento das águas devido ao fenômeno El Niño.


  
### 🔍 Bug 02: Escudo de Seleção sem Texto Alternativo no Código
* **O Problema:** Na seção de esportes do G1, o gráfico que compõe a bandeira/escudo da Argentina e Noruega foi inserido sem a tag descritiva no sistema.
* **Linha de Código com Defeito Detectada:** `<img class="crest" src="https://globo.com" loading="lazy">`
* **Impacto no Usuário:** O leitor de tela falha ao anunciar a identidade visual do time envolvido na notícia porque o programador não inseriu o atributo de acessibilidade.
* **Diretriz Violada:** Critério de Sucesso WCAG 1.1.1 (Conteúdo Não Textual - Nível A).
* **Solução Proposta:** Adicionar a tag `alt="Escudo da Argentina"` ou aplicar o atributo vazio `alt=""` caso a sigla "ARG" logo ao lado seja considerada suficiente para o contexto.
*  ### 📸 Evidência do Erro
<img width="896" height="707" alt="Captura de tela 2026-07-12 110135" src="https://github.com/user-attachments/assets/4b97a04b-a78a-4261-a3cf-2c22abec5f2e" />

**Solução Proposta:**
Como as siglas "ARG" e "NOR" já aparecem escritas em texto logo ao lado dos escudos, as imagens das bandeiras são consideradas decorativas (redundantes). A melhor prática de desenvolvimento é adicionar o atributo alt vazio (`alt=""`). Dessa forma, o leitor de tela ignora as imagens e lê apenas o texto das siglas, evitando que o usuário cego ouça informações repetidas.


*   **Infração Legal:** Desconformidade com o Art. 63 da LBI por criar barreiras digitais no acesso à informação e comunicação.


