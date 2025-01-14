+++
title = "Consultar valores dentro de uma estrutura XML no banco"
+++

<p>Acredito que hoje em dia a maioria dos bancos de dados possui suporte para estruturas XML, sendo um formato de fácil manipulação, leitura e bem organizado por possuir uma estrutura formada por nós e elementos.</p>
<p>Já participei de um projeto no qual ao invés de criarem uma tabela específica para relacionar uma lista de ações de um usuário em um sistema, foi utilizado uma coluna do tipo XML para manter esta lista de ações, o que já atendia perfeitamente a este requisito e eliminando assim a necessidade de possuir mais uma tabela física dentro do schema no banco.</p>
<p>Participei também de outro projeto no qual utilizavam a estrutura XML para enviar uma lista de informações como parâmetro de uma procedure ao banco. O que vejo como uma prática muito melhor, do que enviar a mesma lista separando valores por algum tipo de carácter (,;#$%…). Passando os valores em uma estrutura XML, mantêm as informações mais claras e organizadas, facilitando em muito tratá-las no banco e posterior manutenção do código.<!--more--></p>
<p>Uma vez que você esteja trabalhando com estruturas XMLs, provavelmente em alguma situação será necessário realiza alguma consulta nas informações contidas na mesma.</p>
<h3>sql:variable</h3>
<p>Expõe uma variável que contém um valor SQL dentro de uma expressão XQuery.</p>
<h3>exists</h3>
<p>Verifica a existência de uma cláusula específica e retorna um bit que representa uma das seguintes condições:</p>
<ul>
<li>1 – representando Verdadeiro, se a expressão XQuery em uma consulta retornar um resultado nonempty. Quer dizer, retorna no mínimo um nó XML.</li>
<li>0 – representando Falso, se retornar um resultado vazio.</li>
<li>NULL se a instância de tipo de dado xml na qual a consulta foi executada contiver NULL.</li>
</ul>
<p>Como forma de demonstrar essas funções, vamos supor que um sistema de venda é mantido um histórico de todas as vendas na seguinte tabela:</p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="1">
<tbody>
<tr>
<td><strong>Nome Coluna</strong></td>
<td><strong>Tipo Dado</strong></td>
</tr>
<tr>
<td>HistoricoId</td>
<td>int</td>
</tr>
<tr>
<td>VendedorId&nbsp;</td>
<td>int</td>
</tr>
<tr>
<td>DataVenda&nbsp;</td>
<td>datetime</td>
</tr>
<tr>
<td>VendaId&nbsp;</td>
<td>int</td>
</tr>
<tr>
<td>ProdutosVendidos&nbsp;</td>
<td>xml</td>
</tr>
</tbody>
</table>
<p>Como pode ser visto a cima, será mantido os produtos vendidos em cada venda na seguinte estrutura XML:</p>
<p><code lang="xml"><venda><br />
  
<produto>1</produto>
  
<produto>3</produto>
  
<produto>88</produto>
</venda></code></p>
<p>Agora, digamos que um dos diretores da empresa solicitou que fosse levantado um relatório de todas as vendas realizadas por certo vendedor, no qual continha o produto com o código 88. Como fazer isso, sendo que os códigos dos produtos estão contidos dentro da estrutura XML?</p>
<p>Dessa forma:</p>
<p><code lang="sql">DECLARE @VendedorId INT = 10<br />
DECLARE @Consulta_XML VARCHAR = CAST(@Codigo_Produto AS VARCHAR)</p>
<p>SELECT VendaId<br />
FROM HistoricoVenda <br />
WHERE        <br />
     VendedorId =  @VendedorId<br />
     AND<br />
     ProdutosVendidos.exist('(//Venda/Produto)[. = sql:variable("@Consulta_XML")]') = 1</code></p>
<p>Para que fosse possível realizar a busca dentro do XML foi necessário declarar uma variável, na qual a mesma foi exposta dentro XML através da função sql:variable. Também foi utilizada a função exists para verificar a existência de uma informação, definindo a caminho da mestra na estrutura XML.&nbsp; Note também que foi utilizado // antes da Venda, para especificá-la que está na raiz do XML.</p>
