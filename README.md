# PLANEJAMENTO

0 - Fazer o planejamento das tarefas.

1 - Criar um template para escrever o estudo no confluence

2 - Ler as documentações anotar as referencias

3 - Escrever rascunho sobre o que estou lendo

4 - Escrever as dúvidas

5 - Preparar um exemplo com código sobre o que foi estudado

6 - Preparar um workshop (treinamento para a apresentação para o estado de minas)

<br>

# REFERENCIAS

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
elementos html que são considerados ao medir p LCP: <img>, <video> e blocos de textos ou nós contendo textos.
obs: margens, paddings e borders não são incluídos no calculo do LCP.

[FID](https://web.dev/fid/): O fid mede a interatividade do usuário com a página, ou seja, o tempo desde que o usuário realizou a ação até o momento em que o navegador foi capaz de começar a processar manipuladores de eventos em resposta a essa interação.
Um fid considerado bom deve ter cerca de 100 milissegundos ou menos.
As Consequências desse atraso é um usuário frustrado pois ele interage com a página e nada acontece. Geralmente esse atraso ocorre pois a main-thread (lembrando que js é singleThread) está ocupada processando algum arquivo javascript
