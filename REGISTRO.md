# Registro de decisões — frente layout

Projeto: Guia de Parques de São Paulo (index.html, detalhe.html, style.css)

**Como medi:** naveguei as duas páginas em um Chromium sem interface, variando a largura de 240 px a 1440 px em passos de 2–4 px e checando a rolagem lateral. Confirme no DevTools (Ctrl+Shift+M) arrastando a janela de forma contínua.

**Antes do conserto:** `index.html` sem rolagem lateral, mas a lateral ficava espremida em 84 px até 700 px. `detalhe.html` com rolagem lateral de 240 px até ~390 px (a causa era a tabela).

| # | Ajuste | Tipo | Por quê | Largura em que falhou |
|---|--------|------|---------|-----------------------|
| 1 | Cards da home: `grid` com `repeat(auto-fit, minmax(min(100%, 15rem), 1fr))` | **Intrínseca** | Quantidade de colunas deve seguir o espaço. O `min(100%, …)` impede card mais largo que a tela. | Original: base fixa de 280 px. Agora: 1 coluna em ~360 px, 2 em ~500–1050 px, 3 acima de ~1100 px |
| 2 | Lista de comodidades: `columns: auto 14rem` (era `columns: 2` + media query) | **Intrínseca** | O número de colunas segue a largura; some a media query. | Original: 2 colunas apertadas no celular até o ajuste de 600 px |
| 3 | Lateral da home: acima do conteúdo (linha de categorias) no celular; ao lado (220 px) a partir de **50em (800 px)** | **Deliberada** | O desenho muda de lugar. Com a lateral ao lado, 2 cards de 15rem só cabem a partir de ~800 px (220 + 2×240 + espaços). | Original: coluna de 84 px com texto apertado até 700 px |
| 4 | Cabeçalho: coluna (identidade em cima, menu embaixo) no celular; linha (identidade à esquerda, menu à direita) a partir de **40em (640 px)** | **Deliberada** | O menu da home só cabe ao lado da identidade a partir de ~640 px; abaixo disso ele quebrava em duas linhas ao lado do logo. Na detalhe, o menu com 7 links quebra em linhas (`flex-wrap`), o que é esperado. | ~600 px (home) |
| 5 | Tabelas: no celular, cada linha vira uma "ficha" (rótulos por `::before`); a partir de **30em (480 px)** voltam a ser tabelas | **Deliberada** | Mesma informação, desenho diferente. Uma tabela de 4 colunas não cabe em ~290 px. | Como tabela, estoura até ~400 px (medido) |
| 6 | Contato: rótulo em cima do valor no celular; lado a lado a partir de **30em**; `overflow-wrap: anywhere` | **Deliberada** | O e-mail longo empurrava a página. | Original: ~360 px |
| 7 | Espaçamentos (`padding`) menores na base, maiores a partir de 30em | **Deliberada** | Ganhar largura útil no celular. | — |
| 8 | Grade da home: `grid-template-columns: minmax(0, 1fr)` na base | **Intrínseca** | O `0` no mínimo impede que conteúdo largo alargue a coluna. | — |

## Ligação (HTML mínimo)
- Card do Parque do Carmo: `<a href="detalhe.html">` envolve o conteúdo do card. Ibirapuera e Villa-Lobos ficaram como estavam.
- Detalhe: o menu ganhou `Início` (`index.html`) e `Locais` (`index.html#locais`), e manteve as âncoras das seções. O rodapé mantém "Voltar à página inicial".
- Na home, `#destaques` virou `#locais`, e o link "Eventos" (que apontava para um id inexistente) agora vai para `detalhe.html#eventos`.

## O que ficou de fora (e por quê)
- **Tipografia** (fontes, tamanhos, pesos): é a segunda parte da aula.
- **Mídia** (a imagem do Unsplash e o `object-fit`): também é a segunda parte da aula.
- **Cores e sombras:** não mudei.
- **Exceção:** corrigi o texto do `.botao`, que ficava azul sobre azul (`a:link` ganhava do `.botao`). É um bug de cor, não de layout.
