+++
title = "Ordernar aleatoriamente uma lista"
+++

<p><strong>LINQ</strong> <em>(Language Integrated Query)</em>, além de oferecer um modelo consistente para trabalhar com dados em vários tipos de fontes de dados e formatos, outra importante característica, é facilidade em criar consultas, desde simples <em>selects</em> à outas mirabolantes expressões que uma query possa conter.</p>
<p>Neste exemplo demonstrarei como é fácil,<strong><span style="color: #000000;"> utilizando LINQ</span></strong>, aplicar uma consulta aletória em uma <span style="color: #339966;">List</span>&lt;<span style="color: #3366ff;">int</span>&gt;.</p>
<p>O mesmo poderia ser feito em uma lista de objetos do tipo Pessoa ou qualquer outro do seu domínio.</p>
<p>Isto porque o <strong>LINQ</strong> oferece suporte ao <span style="color: #3366ff;">IEnumerable(Of T)</span> ou interfaces derivadas, como o genérico <span style="color: #3366ff;">IQueryable(Of T)</span> -  <em>chamados de tipos consultáveis</em>.</p>
<p><!--more--></p>
<p>[sourcecode language="csharp"]<br />
            //Lista de exemplo<br />
            var lista = new List&lt;int&gt;()<br />
            {<br />
                0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10<br />
            };<br />
[/sourcecode]</p>
<p>Passando a expressão <span style="color: #3366ff;">OrderBy(i =&gt; Guid.NewGuid())</span> a lista retornará aletória.</p>
<p>[sourcecode language="csharp"]<br />
            //Retorna a lista aletória<br />
            var lista_aleatoria = lista.OrderBy(i =&gt; Guid.NewGuid());<br />
[/sourcecode]</p>
<p>Agora, por que isto acontece?<br />
Basta saber três coisas para entender:</p>
<ol>
<li><strong><span style="color: #008000;">GUID</span></strong>:  Representa um Globally Unique Identifier, ou seja, um Identificador Único Universal.</li>
<li><strong><span style="color: #008000;">LINQ - Variável de Consulta</span></strong> :  Quando você cria uma query com LINQ, o formato dessa consulta será armazenado nessa variável. Mas a consulta ainda não será realizada.</li>
<li><strong><span style="color: #008000;">LINQ - Consulta Adiada</span></strong> : A real execução da consulta é adiada até que você faça a iteração pela variável de consulta em uma instrução foreach. Esse conceito é conhecido como execução adiada.</li>
</ol>
<p>Sendo assim, cada linha na consulta, a expressão de ordernação será diferente.<br />
<em><strong>Obs:</strong> No LINQ é possível forçar a execução imediata de uma consulta. Para entender mais sobre LINQ eu indico <a href="http://msdn.microsoft.com/pt-br/library/bb397906.aspx" target="_blank">Introdução às consultas do LINQ (C#)</a> .</em></p>
