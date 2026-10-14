# Histórico

## v1.1 (14/10/2026)
Aprendizados de mais de dez filmes completos levados para a skill geral, sem nada específico de produto.

- **Briefing** pergunta o que é a peça e para quem, o que quem assiste precisa sentir ou entender, se é demonstrativa ou publicitária, e pede o design system ou a identidade visual. Nada de caminhos ou marcas fixas.
- **`pecas.js`** (novo): textos por máscara e decodificação, título de 2 linhas com rótulo, palavra gigante, traço de virada, número que embaralha, selo, lista que marca, anel, campo de cor com tinta, slogan com troca de palavra (em duas linhas no vertical), flash curto, símbolo desenhado por traço e fecho com logotipo.
- **Marca no `config.json`:** tokens, fontes (`marca.fontes`), símbolo em paths e logotipo; sem imagem, a peça monta símbolo + nome.
- **`cenas.js`** separado do `film.html`, com o arco geral de exemplo nos três formatos.
- **`render.mjs`:** `--marcos` (quadros no meio das transições), `--colisao` (texto sobre o elemento principal, texto sobre texto, margem segura, corte na borda), gravação em `.parcial` com renomeação no fim, folha com o tempo de cada quadro.
- **`audio.mjs`:** biblioteca de sons por evento (tensão, revelação, entrada, pousa, varre, vira, contagem, campo, slogan, fecho, leito, decodificação).
- **Referências:** `arcos.md` (arcos por tipo de peça) e `licoes.md` (os resultados dos testes, com números).
- Regras novas: uma ideia por tela, sem partículas, minimalismo pontual, flash curto, título e elemento principal nunca se cruzam, dados fictícios, tempo realista (15 a 30 min).

## v0.1 (13/10/2026)
Protótipo: canvas 2D, `render.mjs`, `audio.mjs`, regras do estúdio e ciclo de rodadas, a partir de cinco testes comparados.
