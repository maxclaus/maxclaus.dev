+++
title = "Utilizando Replace em uma query de UPDATE"
+++

<img class="size-thumbnail wp-image-193" title="Replace SQL" src="/assets/reforma-ortogr&#225;fica-150x150.jpg" alt="Replace SQL" width="150" height="150" />

<p>Depois de passar um tempo sem escrever nenhum artigo, após a transferência do servidor do blog, estou retomando as atividades por aqui.</p>
<p>E este artigo envolve exatamente esta transferência de servidor.</p>
<p>Por algum motivo, todos os caractéres com acentos especiais no banco, se transformaram em símbolos. Para resolver esse problema, utilizei o REPLACE, substituido todos estes carácters inválidos pelos acentos originais.</p>
<p><!--more--></p>
<p>O <span style="color: #ff0000;">REPLACE</span> funciona da seguinte forma:</p>
<p>[sourcecode language="sql"]<br />
--Definicao<br />
replace(`texto_original`, 'valor_atual', 'novo_valor');</p>
<p>--Exemplo pratico<br />
replace(`papagaio`, 'a', '-');<br />
--O retoro -&gt; p-p-g-io<br />
[/sourcecode]</p>
<p>Como demonstrado o REPLACE retorna a cópia do texto passado com a  substituição dos caractéres definidos.</p>
<p>Para salvar esse retorno, faremos assim:</p>
<p>[sourcecode language="sql"]<br />
--Definicao<br />
UPDATE `nome_tabela`<br />
SET    `nome_coluna` = replace(`nome_coluna`, 'valor_atual', 'novo_valor')<br />
WHERE  `nome_coluna` LIKE '%valor_atual%';</p>
<p>--Exemplo pratico<br />
UPDATE `usuarios`<br />
SET    `nome` = replace(`nome`, 'Maria', 'Mariana')<br />
WHERE  `nome` LIKE '%Maria%';<br />
--Atualiza todos os registros da tabela usuarios, na coluna nome,<br />
--substituindo Maria por Mariana<br />
[/sourcecode]</p>
