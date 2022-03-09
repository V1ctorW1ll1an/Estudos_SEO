# ESTUDO

## Por que o desempenho é importante

O desempenho afeta diretamente a experiencia do usuário, ou seja, um desempenho ruim gera sites lentos, que demoram carregar ou que demoram quando se trata em interação com o usuário, isso leva a uma maior taxa de abandono do mesmo.
Atualmente o número de pessoas utilizando dispositivos moveis é maior que o número de pessoas utilizando desktops, logo a probabilidade do site ser acessado por um 3g ou 4g é muito maior do que o acesso por redes cabeadas ou wi-fi, e por que isso é importante, ou, onde o desempenho entra nisso? É simples, quando acessamos um site utilizando um 3g ou 4g estamos preocupados não so com o tempo de resposta do site mas também com a quantidade de dados que o site vai consumir para ser carregado completamente, quanto mais tempo ele demorar mais ele consome os dados disponíveis em nosso 3g/4g o que afeta diretamente o bolso do usuário.

## Ferramentas utilizadas para medir o desempenho

Uma ótima ferramenta para medir a performance dos sites é a ferramenta do google PSI ou [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/).
Esta ferramenta nos da não apenas um feedback da nossa performance mas também fornece dicas para que possamos melhorar e aprimorar a performance do nosso site.

## Multimídias

Imagens e vídeos são um dos desafios da web, imagens consomem muita banda, uma das estratégias para contornar o problema das imagens é utilizar o lazy load que faz o carregamento das imagens por baixo do pano e sob demanda, isso previne que todas as imagens sejam baixadas de uma só vez e atrapalhe na performance da página.
Podemos usar a lib [lazysizes](https://github.com/aFarkas/lazysizes) ou utilizar o atributo loading.

```html
<img src="image.jpg" alt="..." loading="lazy" />
<iframe src="video-player.html" title="..." loading="lazy"></iframe>
```

Sobre tipagem de imagens podemos consultar o [link](https://developer.mozilla.org/en-US/docs/Learn/Performance/Multimedia#loading_strategy)

## Web Vitals

ref: [Web Vitals](https://web.dev/learn-web-vitals/)

Os três principais pilares do Core Web Vitals se resumem em LCP (Largest Contentful Paint), FID (First Input Delay) e CLS (Cumulative Layout Shift).

[LCP](https://web.dev/lcp/): Em resumo o lcp é o tempo loading do maior conteúdo mostrado ao usuário, segundo as documentações do [google](https://developers.google.com/) uma boa experiência ao usuário é fornecida quando o lcp ocorre dentro de 2,5 segundos, ou seja, o carregamento da maior imagem ou bloco de texto visível na viewport em relação a quando a página começou a carregar pela primeira vez deve ser de no máximo 2,5 segundos.
elementos html que são considerados ao medir o LCP: \<img>, \<video> e blocos de textos ou nós contendo textos.
obs: margens, paddings e borders não são incluídos no calculo do LCP.

[FID](https://web.dev/fid/): O fid mede a interatividade do usuário com a página, ou seja, o tempo desde que o usuário realizou a ação até o momento em que o navegador foi capaz de começar a processar manipuladores de eventos em resposta a essa interação.
Um fid considerado bom deve ter cerca de 100 milissegundos ou menos.
As Consequências desse atraso é um usuário frustrado pois ele interage com a página e nada acontece. Geralmente esse atraso ocorre pois a main-thread (lembrando que js é singleThread) está ocupada processando algum arquivo javascript.
Por que medir a primeira entrada do usuário?
1 - A primeira entrada do usuário é a primeira impressão que o mesmo terá em relação a página.
2 - Os maiores problemas de interatividades ocorrem durante o carregamento da página.
3 - As primeiras entradas são ações como cliques, toques ou pressionamentos de teclas, cliques em inputs, botões e etc, zoom ou scroll não entram nessa lista.

[CLS](https://web.dev/cls/): O cls ou cumulative layout shift é a métrica que mede os deslocamentos dos elementos das páginas, um cls baixo significa que a página é estável e agradável.
exemplo de cls desagravável: https://storage.googleapis.com/web-dev-assets/layout-instability-api/layout-instability2.webm
A pontuação do layout é medida pela seguinte formula: cls = fi \* fd
Ou seja, o cls é o produto da fração de impacto e da fração de distância, sendo a fração de impacto toda a area ocupada pelo elemento antes e depois do [deslocamento](https://web-dev.imgix.net/image/tcFciHGuF3MxnTr1y5ue01OGLBn2/BbpE9rFQbF8aU6iXN1U6.png?auto=format&w=964) (toda a area pontilhada de vermelho) e a fração da distância é a area que foi [deslocada](https://web-dev.imgix.net/image/tcFciHGuF3MxnTr1y5ue01OGLBn2/ASnfpVs2n9winu6mmzdk.png?auto=format&w=964) (seta azul).
Dicas de animações:

1. Em vez de alterar as propriedades height e width, use transform: scale().
2. Para mover os elementos, evite alterar as propriedades top , right , bottom ou left e, em vez disso, use transform: translate().
3. aspect-ratios https://css-tricks.com/aspect-ratio-boxes/

## Técnicas de otimização ([video muito bom falando sobre](https://youtu.be/AQqFZ5t8uNc))

### LCP

<img src="https://web-dev.imgix.net/image/tcFciHGuF3MxnTr1y5ue01OGLBn2/elqsdYqQEefWJbUM2qMO.svg" height="96" width="384">

Algumas técnicas nos permite acelerar o tempo que o maior conteúdo será renderizado na tela:

1. Estabelecer pré conexões para links de terceiros
    ```html
    <link rel="preconnect" href="https://example.com" />
    ```
2. Utilizando estrategias de carregamento assíncrono de javascript e css de arquivos não críticos para a renderização da página.

3. Minificando arquivos js e css (ex [webpack](https://github.com/NMFR/optimize-css-assets-webpack-plugin))

4. Podemos incluir qualquer css crítico para o carregamento da página no próprio \<head> usando a tag \<style>

5. Podemos utilizar o plugin [Critters Webpack plugin](https://github.com/GoogleChromeLabs/critters) para embutir o nosso css crítico caso não possamos adiciona-los manualmente.

6. [Comprimir e minificar arquivos js](https://web.dev/reduce-network-payloads-using-text-compression/)

7. [Adiar js não utilizado](https://web.dev/reduce-javascript-payloads-with-code-splitting/)

8. [Minimizando polyfills não usados](https://web.dev/serve-modern-code-to-modern-browsers/)

9. Utilizar imagens responsivas e de formato moderno.

10. Utilizar [CDNs](https://web.dev/image-cdns/)

11. Utilize pré-load para recursos importantes

```html
<!-- retirado da doc da webDev -->
<link rel="preload" as="script" href="script.js" />
<link rel="preload" as="style" href="style.css" />
<link rel="preload" as="image" href="img.png" />
<link rel="preload" as="video" href="vid.webm" type="video/webm" />
<link rel="preload" href="font.woff2" as="font" type="font/woff2" crossorigin />
```

12. [Serviços adaptáveis](https://web.dev/optimize-lcp/#servico-adaptavel)

As documentações do [webDev](https://web.dev) nos indicam alguns passos extras relacionados a recursos:

<ul>
    <li>Otimização e compressão de imagens </li>
    <li>Pré-carregamento de recursos importantes</li>
    <li>Compactação de arquivos de texto</li>
    <li>Entrega de diferentes ativos com base na conexão de rede (serviço adaptável)</li>
    <li>Ativos de cache usando um service worker</li>
</ul>

### FID

<img src="https://web-dev.imgix.net/image/tcFciHGuF3MxnTr1y5ue01OGLBn2/eXyvkqRHQZ5iG38Axh1Z.svg" height="96" width="384">

Segundo as documentações da webDev, os principais responsáveis pelo grande atraso ou delay nas tarefas de input do usuário são tarefas javascript pesadas, de acordo com a documentação, qualquer bloco/arquivo/tarefa que leve mais de 50ms pode ser caracterizado como uma tarefa longa, e dividir essas tarefas pode reduzir o atraso nas entradas do usuário ao nosso site.

Por que 50ms?

De acordo com o modelo de desempenho centrado no usuário chamado [RAIL](https://web.dev/rail/) se a resposta às ações do usuário ocorrerem dentro do espaço de tempo de 0 a 100ms eles iram sentir um resultado imediato e uma suavidade em suas ações, logo se cada tarefa da nossa página leva no máximo 50ms podemos concluir que é possível realizar duas tarefas dentro dos limites do RAIL, 50ms para a tarefa em execução e 50ms para a nova tarefa requisitada pela entrada do usuário.

Resumindo algumas dicas importantes:

1. Utilizar código sobe demanda, afim de minimizar o impacto na main-thread e agilizar a analise e compilação de scripts realmente necessários para a página, também podemos carregar os anúncios que estão escondidos nas partes mais inferiores das páginas sob demanda (considere utilizar essa estrategia para códigos de terceiros também).

2. Priorizar o carregamento de scripts que oferece maiores valores para a renderização da página.

3. Utilizar webWorks para a execução de js em uma thread em segundo plano (js não relacionados a interface do usuário).

4. Utilizar laze-loading, js e css async e se necessário a técnica de importação de módulos js sob demanda (alterar rotas, exibir modais e etc).

```js
// Importação Dinâmica sob demanda
import("module.js").then((module) => {
    // Do something with the module.
});
```

```html
<!-- Carregamento async do js -->
<script defer src="…"></script>
<script async src="…"></script>
```

As documentações da webDev recomendam carregar todos scripts de terceiros utilizando defer e async por padrão, exceto aqueles que realmente precisam ser carregando de forma sync.

5. Utilizar padrões como "module" e "nomodule" para fornecer pacotes separados para navegadores modernos e legados.

```js
<script type="module" src="modern.js"></script>
<script nomodule src="legacy.js" defer></script>
```

### CLS

<img src="https://web-dev.imgix.net/image/tcFciHGuF3MxnTr1y5ue01OGLBn2/9mWVASbWDLzdBUpVcjE1.svg" height="96" width="384">
