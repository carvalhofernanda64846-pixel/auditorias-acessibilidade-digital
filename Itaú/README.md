# Relatório de Auditoria de Acessibilidade - Banco Itaú

## 1. Introdução
Este relatório documenta uma auditoria técnica de acessibilidade realizada na página inicial do Itaú (segmento Uniclass). O objetivo é identificar barreiras digitais que impedem a navegação de usuários que utilizam tecnologias assistivas ou navegação exclusiva por teclado.

## 2. Metodologia
A análise foi conduzida através de métodos manuais e automatizados:
* **Teste Funcional de Teclado:** Verificação da ordem de foco e navegabilidade sequencial.
* **Avaliação Automatizada:** Utilização da ferramenta de acessibilidade WAVE para identificação de erros de semântica e código.

## 3. Descobertas e Bugs Identificados

### ⚠️ Bug 01: Falha na Navegação por Teclado (Ordem de Foco)
**Descrição:** Ao utilizar a tecla `Tab` para navegar na página, o foco ignora seções inteiras de benefícios e ofertas (cards do Uniclass). O fluxo de navegação é interrompido, tornando o conteúdo inacessível para usuários que não utilizam mouse.
**Impacto:** Usuários com deficiência motora ou visual são excluídos de informações importantes sobre produtos e vantagens do banco.
**Diretrizes Violadas:** WCAG 2.1 - Critério de Sucesso 2.4.3 (Ordem de Foco - Nível A).

**Sugestão de Melhoria:** Revisar a hierarquia do DOM e garantir que todos os elementos interativos possuam `tabindex="0"` ou estejam posicionados corretamente na ordem lógica da página.

### ❌ Bug 02: Botões sem descrição acessível (Empty Buttons)
**Descrição:** Foram identificados 4 botões interativos (`ot-floating-button`) que não possuem conteúdo textual ou rótulos, sendo classificados como "Empty buttons". Estes elementos servem para ações de suporte/chat.

**Evidência:📸**

<img width="1879" height="623" alt="Captura de tela 2026-07-13 082755" src="https://github.com/user-attachments/assets/8586d9b2-271b-4a08-82ae-0e57410cccd9" />

**Evidência Técnica:**
html
`<button type="button" class="ot-floating-button_open"></button>
<button type="button" class="ot-floating-button_close"></button>`

Impacto: Leitores de tela não conseguem identificar a função desses botões, anunciando apenas "Botão", o que impede a interação do usuário.
Diretrizes Violadas: WCAG 2.1 - Critério de Sucesso 4.1.2 (Nome, Função, Valor - Nível A).
Sugestão de Melhoria: Adicionar o atributo aria-label para fornecer o contexto da ação.

Exemplo de correção:
`<button type="button" class="ot-floating-button_open" aria-label="Abrir chat de ajuda"></button>`

4. Conclusão
​A auditoria revelou que, embora o site apresente uma estrutura base sólida, existem falhas críticas de acessibilidade que podem ser corrigidas com ajustes pontuais de semântica no código (HTML) e organização de foco. A implementação dessas melhorias garantirá uma experiência mais inclusiva para todos os usuários do Banco Itaú.
