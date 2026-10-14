---
name: motion-graphics
description: Cria vídeos de motion graphics (MP4 com trilha sintetizada) a partir de uma ideia curta, na marca de quem pede, desenhando tudo em código. Use quando pedirem motion, vídeo animado, vinheta, abertura de evento, lançamento, peça para redes sociais ou animação explicativa, com ou sem vídeo de referência. Para filme de produto digital com telas de interface em 3D, prefira a skill motion-product.
---

# Motion graphics (v1.1.1)

Da ideia ao MP4 sem fotos, vídeos ou prints. Cada elemento é **reconstruído em código** (canvas 2D), na paleta e na tipografia da marca, e o filme é uma função pura do tempo. As regras vêm de testes comparados; o porquê de cada uma está em `referencias/licoes.md`.

**Não use HyperFrames** nem outro framework ou serviço de vídeo pronto (Remotion, Motion Canvas, After Effects, geradores de vídeo por IA). O pipeline é só o desta skill: `film.html` em canvas, `pecas.js`, `render.mjs` (Chrome headless + ffmpeg) e `audio.mjs`.

## 1. Briefing: pergunte só o que faltar (uma mensagem, sem rodadas extras)
A skill não conhece a marca, o projeto nem o público de quem pede: tudo vem do briefing. Se não estiver no pedido, pergunte de uma vez:
1. **"O que é a peça e para quem?"** (marca, evento, produto, campanha; quem vai assistir e onde: telão, redes, site, apresentação)
2. **"Em uma frase: o que quem assiste precisa sentir ou entender ao final?"**
3. **"É demonstrativa (mostrar como algo funciona) ou publicitária (vender uma sensação)?"**
4. **"Qual o formato (16:9, 9:16, 1:1) e a duração?"**
5. **"Qual o design system ou a identidade visual?"** Peça o material: documento de marca, guia de estilo, site, arquivos de fonte e logo (SVG). Se não houver, pergunte cores, fontes e onde encontrar o logo. O motion se adapta à marca **sem mudar nada dela**.

Se mandarem referência (vídeo, link, imagem) **sem dizer o que gostaram**, pergunte também: **"O que você gostou nela: as animações, os cards, a paleta, a tipografia, o ritmo, as transições?"** Só isso será extraído.

Padrões quando não disserem: publicitária, 15 s em 16:9 ou 10 s em 9:16, 60 fps, trilha sintetizada, textos no idioma do pedido. Não peça aprovação de roteiro; mostre o roteiro na resposta e siga.

Se pedirem **várias opções**, cada uma muda de propósito pelo menos dois eixos (arco, câmera, ritmo, tratamento de cor). Uma "mistura" de opções aprovadas parte da mais bem construída e traz momentos pontuais das outras.

## 2. Marca: extraia tokens, não imagens
- Do material recebido, tire **só valores**: fundo, fundo profundo, superfície, borda, texto, apoio, **um acento**, tinta legível sobre o acento, fonte display e de interface. Num site, leia o HTML/CSS (cores e `font-family` computados); **não tire prints para usar no filme**.
- **Logo:** SVG oficial. O símbolo vai em `marca.simbolo.tracos` (paths para desenhar por traço) e o logotipo em `marca.logo`. Sem imagem, a peça monta símbolo + nome. Nunca recorte logo de foto ou de print.
- **Fonte:** o arquivo oficial (`woff2`, licença que permita uso) em `assets/fontes/`, declarado em `marca.fontes`. Sem o arquivo, a fonte de sistema mais próxima, avisando.
- Grave tudo em `config.json` (`marca`). Respeite as regras da marca (grafia do nome, cores exatas, proibições).
- **Dados sempre fictícios.** Nomes, números e pessoas inventados; nunca dados reais de clientes ou pessoas.

## 3. Referência (opcional): extraia a gramática, nunca o conteúdo
- Uma folha de contato (1 quadro por segundo, `tile`); leia no máximo 3 imagens.
- 5 a 8 linhas de gramática **só na dimensão de que a pessoa gostou**: como o texto entra e sai, corte, câmera, cards, ritmo, luz.
- Pessoas, rostos, cenas filmadas, texturas fotográficas e logos de terceiros não se traduzem em código: descarte. Se a referência gira em torno de pessoas, avise e proponha a versão com tipografia, formas e cards.

## 4. Roteiro: história com verbo, uma ideia por tela
- Uma **história com verbo**: algo acontece, muda de estado e termina (pedido confirmado, contador zera, ingresso esgota). Nunca palavras-conceito soltas.
- **Uma ideia por tela.** Um título, um elemento principal e no máximo um detalhe.
- Parta de um arco de `referencias/arcos.md` (lançamento, abertura de evento, vinheta, explicativo, corte para redes). O geral é: **tensão → virada → revelação → prova → resultado → respiro de cor → slogan → fecho com silêncio**.
- Tabela de marcos (`const A = {...}` em `cenas.js`): gancho até 2 s e algo novo a cada 2 a 4 s. A mesma tabela vai para o ARRANJO do áudio e para `window.MARCOS`.
- Elementos em cena são **assets programados**: tipografia, formas da marca, cards, contadores, gráficos, mapas, notificações, cursor, ícones em `Path2D`. Pessoas, quando a ideia pedir, viram avatar com iniciais, ícone ou silhueta geométrica.

## 5. Montagem
1. Copie `modelos/` para `<projeto>/fonte/`. **Não reescreva o render, o áudio nem as peças.**
2. Ajuste `config.json` (formato: 1920x1080, 1080x1920 ou 1080x1080; `dur`; `saida`; `marca`).
3. `node render.mjs --check`: detecta Chrome e ffmpeg com libx264 e guarda em cache. Se faltar algo, peça autorização para instalar `ffmpeg-static` numa pasta temporária.
4. Escreva as cenas em `cenas.js` (array `SCENES` com `{ a, z, draw(t) }`). O modelo já traz o arco geral funcionando nos três formatos; troque textos e tempos. Posições relativas a `W` e `H`, tamanhos em `U`. Peças de `pecas.js`:
   - texto: `frase`, `linhaMascara`, `tituloGrande` (2 linhas com rótulo), `decodifica`, `palavraGigante`, `embaralha`;
   - marca e momentos: `traco` (virada), `seloOk`, `listaMarcada`, `anelProgresso`, `campoCor` + `tinta`, `sloganTroca`, `flash`, `simbolo` (desenhado por traço), `logo`, `cenaFecho`;
   - checagem: `heroi(x0, y0, x1, y1, nome, conteudo)` marca o elemento principal; `decorativo(fn)` desenha sem checar; `cobreCaixas` quando uma camada opaca cobre a tela.
5. Edite só a seção ARRANJO de `audio.mjs`. A BIBLIOTECA DE EVENTOS tem um som para cada momento: `tensao`, `revelacao`, `entrada`, `pousa`, `varre`, `vira`, `contagem`, `campo`, `slogan`, `fecho`, `leito`, `decod`. `node audio.mjs` mede a grade em `beats.json`.
6. Edite arquivos com a ferramenta de edição ou por script Node, nunca por `sed` com template strings (aspas e crases quebram). No Git Bash do Windows, use `MSYS_NO_PATHCONV=1` antes de comandos com caminhos que começam por `/`.

## 6. Regras do estúdio
**Contrato de render**
- `window.seek(t)` pinta o quadro t. Sem transição CSS, `setTimeout`, `requestAnimationFrame` no render ou estado entre quadros. Ruído só por mulberry32 com semente, nunca `Math.random`.
- H.264 yuv420p, CRF 16, 60 fps, áudio a -14 LUFS (o render normaliza).

**Visual**
- Proibidos: partículas e confete, título centralizado sobre degradê, tudo entrando em fade, rótulos de canto e moldura, brilho em elementos de interface, véu cinza longo.
- O "nascer do nada" vem de texto que decodifica, linha que sobe por máscara, traço que se desenha, forma que toma a tela.
- Uma fonte display e uma de interface (podem ser a mesma). **Um acento** só.
- Texto entra por máscara, deslocamento, desfoque curto ou decodificação. A cada 2 a 4 s algo novo acontece.
- **Minimalismo pontual:** momentos de tela quase vazia (uma frase, um número grande, o slogan) entre os momentos densos.
- **Flash** só curto e na camada de cima (`flash`), nunca um véu longo.
- **Título e elemento principal nunca se cruzam, nem no meio do movimento.** Palavra gigante testada contra a borda.
- Leitura no celular: texto principal com no mínimo 6% da altura em 9:16 e 5% em 16:9; nada importante a menos de 6% da borda. No 9:16, quebre o slogan em duas linhas.
- Câmera com intenção: seguir o objeto, aproximar no detalhe, chicote entre planos.
- **Proibido no filme:** foto ou vídeo de pessoas, vídeo de banco de imagens, print de site, textura fotográfica, quadros extraídos de vídeo real.

**Som**
- Trilha e efeitos sintetizados, salvo trilha fornecida. Um som para cada evento, na grade medida. Respiro (`mute`) antes do clímax e silêncio no fecho.

## 7. Ciclo antes de mostrar (no máximo 3 rodadas)
1. `node render.mjs --sheet rodadas/rodada-N.png` (um quadro por batida) **e** `node render.mjs --marcos rodadas/marcos-N.png` (quadros a +0,25, +0,6, +1,0 e +1,6 s de cada marco). Olhe as duas: **os defeitos aparecem no meio do movimento, não na batida.**
2. `node render.mjs --colisao 1`: reprova texto sobre o elemento principal, texto sobre texto, texto fora da margem segura e elemento principal cortado na borda.
3. **Checagens objetivas, que reprovam sozinhas** (a nota da própria IA é otimista; nos testes deu 8 até no vídeo reprovado):
   - `--colisao` acusou algo? Algo cortado na borda em `--marcos`?
   - Há foto, vídeo, print, pessoa real ou dado real? Mais de um acento? Texto entrando só por fade?
   - Algum trecho de 4 s sem mudança? O gancho existe até 2 s?
   - A peça diz o que o briefing pediu que a pessoa sentisse ou entendesse?
   - Algum texto ilegível na miniatura (tamanho de celular)? Cores, fonte e logo batem com a marca?
4. Notas de 1 a 10: gancho, leitura no celular, movimento, variedade, fidelidade à marca, sincronia do som. Corrija os 3 piores problemas e repita até tudo ter 8 ou mais e nenhuma checagem reprovar. Para um trecho, `--stills t1,t2 --dir <pasta>`.
5. Só então o render completo, **uma vez**, em segundo plano. Para conferir movimento antes, `--draft 1` (30 fps).

## 8. Entrega
- O render grava `<saida>.parcial` e renomeia só no fim. **Não diga que o vídeo está pronto antes de o arquivo final existir** (um MP4 em gravação parece corrompido).
- Confira o MP4: duração, resolução, codec, áudio a -14 LUFS, zero erro de decodificação (`ffmpeg -v error -i x.mp4 -f null -`) e 4 a 6 quadros extraídos do próprio arquivo, pelo menos um no meio de uma transição.
- Entregue o caminho do arquivo, a estrutura do filme em lista curta e a tabela de notas.
- Não sobrescreva arquivos existentes (`--force 1` só para os deste projeto); cada versão em pasta ou arquivo novo. Se o projeto tiver um arquivo de instruções ou de memória, leia antes e registre o resultado ao terminar.

## Orçamento de tempo
Briefing e marca 3 min · roteiro 3 min · cenas 5 a 10 min · rodadas 5 min · render 1 a 3 min. **Total de 15 a 30 min** (mais 5 a 10 min com referência). Se o render estimar mais de 10 min, pare e procure a camada cara (`filter: blur` grande, `mix-blend-mode`, imagem enorme, grão ligado).
