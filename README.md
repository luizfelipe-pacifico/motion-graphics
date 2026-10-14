# motion-graphics

Skill para Claude Code que cria **vídeos de motion graphics** em MP4 a partir de uma ideia curta, na marca de quem pede, com trilha sintetizada. Sem fotos, vídeos de banco ou prints: tudo é desenhado em código (canvas 2D), então qualquer elemento pode ser animado. Serve para vinheta, abertura de evento, lançamento, peça para redes e explicativo, em 16:9, 9:16 ou 1:1.

Para filmes de **produto digital** (SaaS, app, sistema) com as telas de interface reconstruídas e animadas em 3D, veja a skill irmã [motion-product](https://github.com/luizfelipe-pacifico/motion-product).

## Instalação
Clone esta pasta para a pasta de skills do Claude Code:

```bash
# para todos os projetos
git clone https://github.com/luizfelipe-pacifico/motion-graphics.git ~/.claude/skills/motion-graphics
# ou só para um projeto
git clone https://github.com/luizfelipe-pacifico/motion-graphics.git <projeto>/.claude/skills/motion-graphics
```

Requisitos: Node 22 ou mais novo, Chrome ou Edge, e ffmpeg com libx264 (`node render.mjs --check` encontra e guarda em cache).

## Uso
Peça ao Claude Code um vídeo ("faça uma vinheta de 8 s para a nossa marca", "um motion de abertura para o evento"). A skill pergunta só o que faltar: o que é a peça e para quem, o que quem assiste precisa sentir, se é demonstrativa ou publicitária, formato e duração, e o design system ou a identidade visual. Depois monta o roteiro, desenha as cenas, revisa com folhas de contato e checagens automáticas, e renderiza uma vez.

## Estrutura
```
SKILL.md                  instruções que o Claude segue
modelos/
  film.html               palco em canvas: contrato seek(t), utilitários, carga de fontes e logotipo
  pecas.js                peças prontas: textos, traço de virada, número que embaralha, selo, lista, anel,
                          campo de cor com tinta, slogan com troca de palavra, flash, símbolo desenhado, fecho
  cenas.js                roteiro de exemplo (arco geral, 16 s, funciona em 16:9, 9:16 e 1:1)
  audio.mjs               trilha sintetizada; biblioteca de sons por evento; edite só o ARRANJO
  render.mjs              render com Chrome headless + ffmpeg
  config.json             formato, duração e marca
referencias/
  arcos.md                arcos de roteiro por tipo de peça
  licoes.md               o porquê de cada regra (testes comparados)
```

## Testar o modelo
```bash
mkdir -p teste/fonte && cp modelos/* teste/fonte/ && cd teste/fonte
node audio.mjs
node render.mjs --sheet ../rodadas/r1.png     # um quadro por batida
node render.mjs --marcos ../rodadas/m1.png    # quadros no meio das transições
node render.mjs --colisao 1                   # sobreposição, margem segura e corte na borda
node render.mjs                               # vídeo final em ../resultados/
```

## Contribuição
Mudanças entram só por pull request, com revisão do mantenedor. A branch `main` é protegida.

## Licença
[MIT](LICENSE).
