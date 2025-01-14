+++
title = "Replace All JavaScript"
+++

<p>Dica rápida:</p>
<p>Para você que precisa substituir vários caracteres repetidos em um texto javascript. E já percebeu que o &nbsp;simples "replace" não funciona. No caso do javascript, o replace substitui apenas o 1º caracter encontrado.</p>
<p>Basta utilizar split + join ao invés do replace:&nbsp;</p>
<p><code lang="javascript">.split(CaracterAntigo).join(CaracterNovo);</code></p>
<p>Exemplo:</p>
<p><code lang="javascript">var texto = '1. 2. 3. 4. 5';<br />
var textoFormatado = texto.split('.').join('');<br />
//Ficaria assim: 1 2 3 4 5</code></p>
