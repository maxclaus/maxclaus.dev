+++
title = "Validação com REGEX Compiled"
+++

<p>Uma classe simples de expressões regulares com vários tipos de validações.</p>
<p><span style="text-decoration: underline;">Antes dos código, um pouco da definição da "Regex"<br />
</span></p>

<img class="size-thumbnail wp-image-136" style="border: 1px solid black; margin: 3px;" title="regex" src="/assets/regex-150x150.jpg" alt="" width="150" height="150" />

<p><strong>Expressão Regular:</strong> <em>Uma composição de símbolos, caracteres com funções especiais, que, agrupados entre si e com caracteres literais, formam uma sequência, uma expressão. Essa expressão é interpretada como uma regra, que indicaría sucesso se uma entrada de dados qualquer casar com essa regra, ou seja, obedecer exatamente a todas as suas condições.</em></p>
<p>Segundo testes publicados neste artigo <a href="http://dotnetperls.com/regex-performance">http://dotnetperls.com/regex-performance</a> o Regex Compiled toma 10x mais tempo na partida, mas os rendimentos de tempo de execução são 30% melhor.</p>
<p><!--more--></p>
<p>Primeiro crie a classe de validação:</p>
<p>[csharp title="Validate.cs"]<br />
using System;<br />
using System.Collections.Generic;<br />
using System.Linq;<br />
using System.Web;<br />
using System.Text.RegularExpressions;</p>
<p>/// summary<br />
/// Classe de validação<br />
/// summary<br />
public static class ValidateField<br />
{<br />
    /// summary<br />
    /// Enum com os tipos de Validacoes<br />
    /// summary<br />
    public static enum TipoValidacao { CPF, CNPJ, Data, Tempo, Email, CEP, Telefone, Decimal, URL };</p>
<p>    /// summary<br />
    /// Expressão regular com as regras do CPF<br />
    /// summary<br />
    protected static Regex _cpf = new Regex(@&quot;^d{3}.?d{3}.?d{3}-?d{2}$&quot;, RegexOptions.Compiled);</p>
<p>    /// &lt;summary&gt;<br />
    /// Expressão regular com as regras de cnpj<br />
    /// &lt;/summary&gt;<br />
    protected static Regex _cnpj = new Regex(@&quot;(^(d{2}.d{3}.d{3}/d{4}-d{2})|(d{14})$)&quot;);</p>
<p>    /// &lt;summary&gt;<br />
    /// Expressão regular com as regras de data Ex: 23/09/2011<br />
    /// &lt;/summary&gt;<br />
    protected static Regex _data = new Regex(@&quot;^((0[1-9]|[12]d)/(0[1-9]|1[0-2])|30/(0[13-9]|1[0-2])|31/(0[13578]|1[02]))/d{4}$&quot;, RegexOptions.Compiled);</p>
<p>    /// &lt;summary&gt;<br />
    /// Expressão regular com as regras de tempo Ex: 12:35<br />
    /// &lt;/summary&gt;<br />
    protected static Regex _tempo = new Regex(@&quot;(([0-1][0-9])|([2][0-3])):([0-5][0-9])&quot;);</p>
<p>    /// &lt;summary&gt;<br />
    /// Expressão regular com as regras de e-mail Ex: nickname@email.com<br />
    /// &lt;/summary&gt;<br />
    protected static Regex _email = new Regex(@&quot;^[A-Za-z0-9](([_.-]?[a-zA-Z0-9]+)*)@([A-Za-z0-9]+)(([.-]?[a-zA-Z0-9]+)*).([A-Za-z]{2,})$&quot;);</p>
<p>    /// &lt;summary&gt;<br />
    /// Expressão regular com as regras de cep Ex: 87094-132<br />
    /// &lt;/summary&gt;<br />
    protected static Regex _cep = new Regex(@&quot;^[0-9]{5}-[0-9]{3}$&quot;);</p>
<p>    /// &lt;summary&gt;<br />
    /// Expressão regular com as regras de telefone Ex: (44)3344-4332<br />
    /// &lt;/summary&gt;<br />
    protected static Regex _telefone = new Regex(@&quot;^(d{2})d{4}-d{4}$&quot;);</p>
<p>    /// &lt;summary&gt;<br />
    /// Expressão regular com as regras de telefone Ex: 405,00 ou 405.00<br />
    /// &lt;/summary&gt;<br />
    protected static Regex _decimal = new Regex(@&quot;^(?=d+)d{0,4}([.,]d{0,2})?$&quot;);</p>
<p>    /// &lt;summary&gt;<br />
    /// Expressão regular com as regras de url Ex: http://www.maxcnunes.com<br />
    /// &lt;/summary&gt;<br />
    protected static Regex _url = new Regex(@&quot;^(ht|f)tp(s?)://[0-9a-zA-Z]([-.w]*[0-9a-zA-Z])*(:(0-9)*)*(/?)([a-zA-Z0-9-.?,'/+&amp;amp;amp;%$#_]*)?$&quot;);</p>
<p>    /// &lt;summary&gt;<br />
    /// Método de validação<br />
    /// &lt;/summary&gt;<br />
    /// &lt;param name=&quot;value&quot;&gt;Valor string a ser validado&lt;/param&gt;<br />
    /// &lt;param name=&quot;type&quot;&gt;Tipo enum da validação&lt;/param&gt;<br />
    /// &lt;returns&gt;False se estiver inv lido&lt;/returns&gt;<br />
    public static bool ValidateField(string value, TipoValidacao type)<br />
    {<br />
        bool validate = false;</p>
<p>        switch (type)<br />
        {<br />
            case TipoValidacao.CPF: validate = _cpf.IsMatch(value) ? true : false;<br />
                break;<br />
            case TipoValidacao.CNPJ: validate = _cnpj.IsMatch(value) ? true : false;<br />
                break;<br />
            case TipoValidacao.Data: validate = _data.IsMatch(value) ? true : false;<br />
                break;<br />
            case TipoValidacao.Tempo: validate = _tempo.IsMatch(value) ? true : false;<br />
                break;<br />
            case TipoValidacao.Email: validate = _email.IsMatch(value) ? true : false;<br />
                break;<br />
            case TipoValidacao.CEP: validate = _cep.IsMatch(value) ? true : false;<br />
                break;<br />
            case TipoValidacao.Telefone: validate = _telefone.IsMatch(value) ? true : false;<br />
                break;<br />
            case TipoValidacao.Decimal: validate = _decimal.IsMatch(value) ? true : false;<br />
                break;<br />
            case TipoValidacao.URL: validate = _url.IsMatch(value) ? true : false;<br />
                break;<br />
            default: validate = false;<br />
                break;<br />
        }<br />
        return validate;<br />
    }<br />
}<br />
[/csharp]</p>
<p>Utilizar a classe onde desejar, exemplo ao disparar o evento click do botão em uma p gina ASP.NET:</p>
<p>[sourcecode language="csharp"]<br />
protected void ButtonValidate_Click(object sender, EventArgs e)<br />
 {<br />
     if (!Validate(TextBoxCPF.Text, ValidateField.TipoValidacao.CPF))<br />
     {<br />
         Response.Write(&quot;CPF est  em um formato inv lido!&quot;);<br />
         return;<br />
     }<br />
     if (!Validate(TextBoxDataNascimento.Text, ValidateField.TipoValidacao.Data))<br />
     {<br />
         Response.Write(&quot;Data de nascimento est  em um formato inv lido!&quot;);<br />
         return;<br />
     }<br />
 }<br />
[/sourcecode]</p>
