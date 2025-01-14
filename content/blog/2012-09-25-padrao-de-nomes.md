+++
title = "Padrão de nomes"
+++


<img class="size-thumbnail wp-image-724" title="organizado" src="/assets/organizado-150x150.jpg" alt="" width="150" height="150" />

<p>Em projetos que existem um time de desenvolvimento e um desenvolvedor depende de outros para construir um sistema, uma padronização no código deve ser tomada como regra para o bem comum do projeto.</p>
<p>Não estou dizendo que os desenvolvedores devem ficar moldados a regras e não podem experimentar novas possibilidades. Mas que se necessário e possível, seja feito com o consentimento de todos.</p>
<p><!--more--></p>
<h2>Caso do Problema</h2>
<p>Vamos usar um exemplo, que com certeza ocorre em muitas empresas. Um desenvolvedor, que cumpria todas as tarefas muito bem, dentro do prazo e funcionalidades exigidas. O qual, nunca passou pela sua cabeça sair da empresa, em um momento inesperado precisa sair da mesma. Até ai tudo bem, mas logo após deste fato, ocorre algum problema em umas das tarefas desenvolvidas por ele e você como desenvolvedor foi encarregado de corrigir esse pequeno bug.</p>
<p>Ao abrir o código para manutenção, você nota que aquilo que estava funcionando muito bem, na verdade estava uma completa bagunça.</p>
<ul>
<li>Métodos com letras todas em maiúscula e outros em minúscula.</li>
<li>Algumas variáveis em inglês e outras em português.</li>
<li>Algumas variáveis e métodos abreviados.</li>
<li>Nenhum comentário e summary sobre as funcionalidades. (É desconsiderável&nbsp;se estiver bem estruturado, refatorado e com nomes corretos)</li>
<li>Métodos repetidos que realizavam exatamente a mesma funcionalidade.</li>
</ul>
<p>Imaginem como uma simples correção pode se tornar tão complicado, que é possível pensar que seja mais fácil refazer esta tarefa, do que entender toda essa bagunça para conseguir corrigir o bug.</p>
<h2>Solução</h2>
<p>Desde o .NET Framework 1.1 a Microsoft disponibiliza no MSDN um Guia de Nomenclaturas, que indica uma série de padrões para nomes.</p>
<p><a href="http://msdn.microsoft.com/en-us/library/xzf533w0(v=vs.71).aspx#feedback" target="_blank">http://msdn.microsoft.com/en-us/library/xzf533w0(v=vs.71).aspx#feedback</a></p>
<h3>Estilos de Capitalização</h3>
<p>Utilize o seguinte 3 estilos de convenções para as capitalizações.</p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="2">
<tbody>
<tr>
<td style="width: 100px;">Pascal case</td>
<td>A primeira letra do identificador e a primeira letra de cada palavra concatenada subsequente forem capitalizados. Você pode usar caso Pascal para identificadores de três ou mais caracteres. Por exemplo: BackColor</td>
</tr>
<tr>
<td>Camel case</td>
<td>A primeira letra de um identificador é minúscula ea primeira letra de cada palavra concatenada subsequente é maiúscula. Por exemplo: backColor</td>
</tr>
<tr>
<td>Uppercase</td>
<td>Todas as letras no identificador são capitalizados. Use esta convenção apenas para identificadores que consistem em duas ou menos letras. Por exemplo: System.IO</p>
<p>System.Web.UI</td>
</tr>
</tbody>
</table>
<p>A seguinte tabela resume as regras de capitalização e disponibiliza exemplos de diferentes tipos de capitalização.</p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="2">
<tbody>
<tr>
<td><span style="color: #00cc00;"><strong>Identificador</strong></span></td>
<td><span style="color: #00cc00;"><strong>Case</strong></span></td>
<td><span style="color: #00cc00;"><strong>Exemplo</strong></span></td>
</tr>
<tr>
<td>&nbsp;Classes</td>
<td>&nbsp;Pascal</td>
<td>&nbsp;OrdemDeServico</td>
</tr>
<tr>
<td>&nbsp;Enum</td>
<td>&nbsp;Pascal</td>
<td>&nbsp;Situacao</td>
</tr>
<tr>
<td>&nbsp;Eventos</td>
<td>&nbsp;Pascal</td>
<td>&nbsp;AlteracaoDoValor</td>
</tr>
<tr>
<td>&nbsp;Read-only, Estático</td>
<td>&nbsp;Pascal</td>
<td>&nbsp;ValorVermelho</td>
</tr>
<tr>
<td>&nbsp;Interfaces</td>
<td>&nbsp;Pascal</td>
<td>&nbsp;IRepositorio (Sempre com prefixo 'I')</td>
</tr>
<tr>
<td>&nbsp;Métodos</td>
<td>&nbsp;Pascal</td>
<td>&nbsp;BuscarPeloNome</td>
</tr>
<tr>
<td>&nbsp;Namespace</td>
<td>&nbsp;Pascal</td>
<td>&nbsp;Projeto.Dados.Repositorio</td>
</tr>
<tr>
<td>&nbsp;Parâmetro</td>
<td>&nbsp;Camel</td>
<td>&nbsp;dataNascimento</td>
</tr>
<tr>
<td>&nbsp;Propriedade</td>
<td>&nbsp;Pascal</td>
<td>&nbsp;DataNascimento</td>
</tr>
<tr>
<td>&nbsp;Atributo</td>
<td>&nbsp;Camel</td>
<td>&nbsp;dataCadastro</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>
<h3>Abreviações</h3>
<p>Para evitar confusão, siga estas regras relativa a utilização de abreviaturas:</p>
<ul>
<li>Não use abreviações ou contrações de partes de nomes identificadores. Por exemplo, use<span style="color: #0099ff;"> ObterAltura</span> ao invés de <span style="color: #74d217;"><span style="color: #0099ff;">ObterAlt</span><span style="color: #000000;">.</span></span></li>
<li><span style="color: #74d217;"><span style="color: #000000;">Não utilize siglas que não são geralmente aceitados no campo da computação.</span></span></li>
<li><span style="color: #74d217;"><span style="color: #000000;">Quando apropriado, use o bom conhecimento de siglas para substituir frases e nomes compridos. Pro exemplo, use <span style="color: #0099ff;">UI</span> ao invés de<span style="color: #0099ff;"> User Interface</span>.</span></span></li>
<li><span style="color: #74d217;"><span style="color: #000000;">Quando utilizar siglas, use Pascal case ou Camel case para siglas com mais de 2 caracteres. E quando for apenas 2 caracteres, mantena tudo em maiúsculo.</span></span></li>
</ul>
<h3>&nbsp;</h3>
<h3>Evitando a Confusão com Nomes e Tipos</h3>
<p>Use nomes que descrevem o significado de um tipo ao invés de nomes que descrevem o tipo. No caso raro que um parâmetro não tem significado semântico para além do seu tipo, usar um nome genérico. Por exemplo:</p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="2">
<tbody>
<tr>
<td>Errado</td>
<td>Certo</td>
</tr>
<tr>
<td>&nbsp;public Pessoa BuscarPessoa(string stringNome);</td>
<td>&nbsp;public Pessoa BuscarPessoa(string nome);</td>
</tr>
<tr>
<td>&nbsp;public int CalcularImc(int intPeso, double doubleAltura);</td>
<td>&nbsp;public int CalcularImc(int peso, double altura);</td>
</tr>
</tbody>
</table>
<h3>Namespace</h3>
<p>Uma regra comum para a nomenclatura de namespaces é utilizar o nome da empresa seguido pelo nome da tecnologia ou camada de um projeto e opcionalmente pela funcionalidade e design.</p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="2">
<tbody>
<tr>
<td>NomeEmpresa.NomeTecnologia[.Funcionalidade][.Design]</td>
</tr>
</tbody>
</table>
<p>Por exemplo:</p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="2">
<tbody>
<tr>
<td>Tam.Dados</td>
</tr>
<tr>
<td>Tam.Dados.Repositorios</td>
</tr>
</tbody>
</table>
<p>Não utilize o mesmo nome para um namespace e uma classe. Um namespace chamado <span style="color: #0099ff;">Tam.Dados</span> e uma classe chamada <span style="color: #0099ff;">Dados<span style="color: #000000;">.</span></span></p>
<h3>Nome de Classes</h3>
<ul>
<li>Utilize um substantivo como nome de classes.</li>
<li>Utilize Pascal case.</li>
<li>Utilize abreviações com moderação.</li>
<li>Não utilize prefixos como <span style="color: #0099ff;">c <span style="color: #000000;">para classes. Por exemplo, utilize <span style="color: #0099ff;">Pessoa</span> ao invés de <span style="color: #0099ff;">cPessoa<span style="color: #000000;">.</span></span></span></span></li>
<li><span style="color: #0099ff;"><span style="color: #000000;"><span style="color: #0099ff;"><span style="color: #000000;">Não utilize '<span style="color: #0099ff;">_</span>' para separar nomes.</span></span></span></span></li>
<li>Quando apropriado, utilize uma palavra composta para nomear uma classe derivada. A segunda parte do nome da classe derivada deve ter o nome da classe base. Por exemplo, <span style="color: #0099ff;">ArgumentException</span>.</li>
</ul>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="2">
<tbody>
<tr>
<td>public class Pessoa</td>
</tr>
</tbody>
</table>
<h3>Nome de Interfaces</h3>
<ul>
<li>Nome de interfaces com substantivos ou adjetivos que descrevam um comportamento. Por exemplo, a interface com o nome <span style="color: #0099ff;">IRepositorio</span>&nbsp;descrevendo um substantivo. E a interface <span style="color: #0099ff;">IValidador</span> com uma adjetivo.</li>
<li>Utilize Pascal case.</li>
<li>Utilize abreviações com moderação.</li>
<li>Não utilize '_' para separar nomes.</li>
<li>Utilize o prefixo '<span style="color: #0099ff;">I</span>' em maiúsculo para indicar que é uma interface.</li>
<li>Utilize similaridade de nomes quando você definiu uma classe/interface par onde a classe é um padrão da implementação da interface. O nomes devem serem diferenciados somente pela letra I como prefixo no nome da interface.</li>
</ul>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="2">
<tbody>
<tr>
<td>public interface IValidador</td>
</tr>
</tbody>
</table>
<h3>Nome de Enums</h3>
<ul>
<li>Use Pascal case para Enums e seus valores</li>
<li>Utilize abreviações com moderação.</li>
<li>Não utilize <span style="color: #0099ff;">Enum</span> como sufixo ou prefixo.</li>
</ul>
<h3>Nome de Campos Estáticos</h3>
<div>
<ul>
<li>Utilize substantivos ou abreviações de substantivos para campos estáticos.</li>
<li>Utilize Pascal case.</li>
<li>Não utilize a notação Hungara para nomes de campos estáticos.</li>
<li>É recomendado que utilize propriedades estáticas ao invés de campos estáticos.</li>
</ul>
</div>
<div>&nbsp;</div>
<div>Referências:</div>
<div><a href="http://msdn.microsoft.com/en-us/library/ab6a8y1b(v=vs.71).aspx">http://msdn.microsoft.com/en-us/library/ab6a8y1b(v=vs.71).aspx</a></div>
<div><a href="http://msdn.microsoft.com/en-us/library/4df752aw(v=vs.71).aspx">http://msdn.microsoft.com/en-us/library/4df752aw(v=vs.71).aspx</a></div>
<div><a href="http://msdn.microsoft.com/en-us/library/fzcth91k(v=vs.71).aspx">http://msdn.microsoft.com/en-us/library/fzcth91k(v=vs.71).aspx</a></div>
<div><a href="http://msdn.microsoft.com/en-us/library/h0eyck3s(v=vs.71).aspx">http://msdn.microsoft.com/en-us/library/h0eyck3s(v=vs.71).aspx</a></div>
<div><a href="http://msdn.microsoft.com/en-us/library/04xykw57(v=vs.71).aspx">http://msdn.microsoft.com/en-us/library/04xykw57(v=vs.71).aspx</a></div>
<div><a href="http://msdn.microsoft.com/en-us/library/426s83c3(v=vs.71).aspx">http://msdn.microsoft.com/en-us/library/426s83c3(v=vs.71).aspx</a></div>
<div><a href="http://msdn.microsoft.com/en-us/library/9cws5bzd(v=vs.71).aspx">http://msdn.microsoft.com/en-us/library/9cws5bzd(v=vs.71).aspx</a></div>
<div><a href="http://msdn.microsoft.com/en-us/library/czefa0ke(v=vs.71).aspx">http://msdn.microsoft.com/en-us/library/czefa0ke(v=vs.71).aspx</a></div>
