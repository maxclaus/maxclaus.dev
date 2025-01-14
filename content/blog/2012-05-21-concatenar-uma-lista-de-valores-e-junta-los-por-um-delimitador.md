+++
title = "Concatenar uma lista de valores e juntá-los por um delimitador"
+++

<p>Quando trabalhamos com Stored Procedures&nbsp;para aumentar a performance, muitas vezes quando a situação permite, damos preferência por realizar a execução de uma única vez de uma Stored Procedure, ao invés de chamá-la para cada código contido em uma lista.</p>
<p>Como os parâmetros de uma Stored Procedure não aceitam um tipo List como o que existe no C#, a forma mais simples de passar uma lista a Stored Procedure seria concatenar todos os códigos separados por um delimitador e tratar o parâmetro como um tipo Varchar.</p>
<p>Por exemplo, vamos dizer que você possua uma tela de gerenciar clientes, na qual é possível alterar a situação de cada um deles. Nessa tela existe uma Gridview com Checkbox em cada linha, para que seja possível selecionar cada cliente que você deseje desabilitar.<!--more--></p>
<p>Após você selecionar todos os clientes, solicitar que sejam desabilitados e recuperar no codebehind a lista dos clientes selecionados, devesse ser preparado o parâmetro a ser enviado a Stored Procedure com o código de todos os clientes.</p>
<h3>Clientes selecionados:</h3>
<p><code lang="csharp">var clientes = new List<cliente><br />
            {<br />
                new Cliente {Id = 1, Nome = "Cliente 1"},<br />
                new Cliente {Id = 2, Nome = "Cliente 2"},<br />
                new Cliente {Id = 4, Nome = "Cliente 4"},<br />
                new Cliente {Id = 5, Nome = "Cliente 5"},<br />
                new Cliente {Id = 6, Nome = "Cliente 6"},<br />
                new Cliente {Id = 8, Nome = "Cliente 8"},<br />
                new Cliente {Id = 11, Nome = "Cliente 11"},<br />
                new Cliente {Id = 12, Nome = "Cliente 12"},<br />
                new Cliente {Id = 15, Nome = "Cliente 15"}<br />
            };</cliente></code></p>
<p>Agora como fazer a lista a cima ficar assim: "<em><span style="color: #3366ff;"><strong>1,2,4,5,6,8,11,12,15</strong></span></em>"?</p>
<h3>Funcional, mas trabalhoso:</h3>
<p>Bem talvez você tenha imaginado fazer da forma mais comum: com for e concatenando item a item.</p>
<p><code lang="csharp">string ids = string.Empty;<br />
for (int i = 0; i < clientes.Count; i++)<br />
{<br />
     ids_foreach += clientes[i].Id.ToString();<br />
     if (i + 1 < clientes.Count)<br />
        ids_foreach += ",";<br />
}</code></p>
<h3>Simplificando:</h3>
<p>Mas por que não simplificar isso e utilizar recursos fornecidos pelo próprio .NET? Com LINQ e o Join do string ficaria assim:</p>
<p><code lang="csharp">string ids = string.Join(",", clientes.Select(cliente => cliente.Id.ToString()));</code></p>
<p>O Join do string pode ser utilizado com 2 parâmetros:</p>
<ol>
<li>Valor delimitador;</li>
<li>IEnumerable de strings (A lista a ser concatenada);</li>
</ol>
<p>Com o LINQ utilizamos o Select para selecionar da lista de clientes apenas a propriedade Id convertidos para String, retornando assim a lista de IEnumerable de strings.</p>
<p>Obs: Outra forma de passar uma lista de valores a Stored Procedure seria através de uma parâmetro do tipo XML.</p>
