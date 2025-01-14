+++
title = "Substituindo propriedade estáticas no ASP.NET"
+++

<p>Utilizar variáveis estática no ASP.NET é um sério problema, porque objetos estáticos possuem apenas uma estância em toda aplicação.</p>
<p>Ou seja, se eu estivesse em um e-commerce e começasse a adicionar itens ao meu carrinho, e um outro usuário logo a após eu, acesse a página de itens do carrinho dele. Estaria todos os meus itens visíveis para ele.</p>
<p><!--more--></p>
<h3>Para escopo de toda a aplicação: Utilize SESSION</h3>
<p><span style="color: #ff0000;"><strong>ERRADO</strong></span></p>
<p>Onde estava um atributo estático:</p>
<p><code lang="csharp">public static int nomeVariavel;</code></p>
<p><span style="color: #00ff00;"><strong>CERTO</strong></span></p>
<p>Deverá ser refatorado em uma propriedade que servirá apenas de acesso para o valor.</p>
<p>Ou seja, ao definir um valor para essa propriedade, será armazenado em uma Session.</p>
<p>E ao recuperar um valor dessa propriedade, ela irá buscar na mesma Session.</p>
<p><code lang="csharp">public int nomeVariavel<br />
{<br />
    get { return (Session["NOME_SESSAO"] == null) ? 0 : int.Parse(Session["NOME_SESSAO"].ToString()); }<br />
    set { Session["NOME_SESSAO"] = value; }<br />
}</code></p>
<p>No exemplo a cima, utilizei if ternário. Se a session estiver nula, então retorna um valor padrão. Se não, converte a session para tipo correto e retorna o valor em seguida.</p>
<p>No caso de uma variável do tipo Lista devemo sempre inicializar a lista caso ela ainda seja nula, poderíamos fazer assim:</p>
<p><code lang="csharp">public List<tipoobjeto> nomeVariavel<br />
{<br />
    get { </p>
<p>        if(Session["NOME_SESSAO"] == null)<br />
            Session["NOME_SESSAO"]  = new List<tipoobjeto>();<br />
        return (Session["NOME_SESSAO"] as List<tipoobjeto>);<br />
    }<br />
    set { Session["NOME_SESSAO"] = value; }<br />
}</tipoobjeto></tipoobjeto></tipoobjeto></code></p>
<h3>Para escopo de apenas uma página: Utilize ViewState</h3>
<p>Caso o escopo dessa variável seja apenas de uma tela, ou seja esse valor deixará de existir quando for deixado a página, poderia ser utilizado uma ViewState no lugar da Session.</p>
<p><code lang="csharp">public List<tipoobjeto> nomeVariavel<br />
{<br />
    get { </p>
<p>        if(ViewState["NOME_SESSAO"] == null)<br />
            ViewState["NOME_SESSAO"] = new List<tipoobjeto>();<br />
        return (ViewState["NOME_SESSAO"] as List<tipoobjeto>);<br />
    }<br />
    set { ViewState["NOME_SESSAO"] = value; }<br />
}</tipoobjeto></tipoobjeto></tipoobjeto></code></p>
