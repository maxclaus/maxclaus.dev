+++
title = "POO JSON JavaScript"
+++

<p>Quando começamos a trabalhar mais com javascript, aproveitando as vantagens de uma linguagem client-side e o código começar a crescer e ficar mais complexo, surge nessecidade de seguir algum padrão.</p>
<p>E nada melhor, do que implementar algo que você já esteja acostumado a utlizar, como o Paradígma Orientado a Objetos(<strong>POO</strong>).</p>
<p>Trantando como uma <strong>CLASSE</strong>, as informações manipuladas no código, torna-o mais legível, organizado e de fácil manutenção.</p>
<p><!--more--></p>
<p><span style="color: #000000;"><strong>Declarando uma classe em javascript:</strong></span></p>
<p>[sourcecode language="javascript"]<br />
            //Declaração da classe Pessoa<br />
            function Pessoa() {<br />
                //Definição dos atributos<br />
                this.nome = &quot;&quot;;<br />
                this.idade = 0;<br />
                this.formado = false;<br />
            }</p>
<p>            //Instaciação de um objeto da classe Pessoa<br />
            var _fulano = new Pessoa();</p>
<p>            //Acessando e alterando o valor de um atributo<br />
            _fulano.idade = 15;<br />
[/sourcecode]</p>
<p><strong><span style="color: #000000;">Supondo que possuímos o seguinte formulário:</span></strong></p>
<p>[sourcecode language="html"]<br />
        &lt;!-- :: JQUERY :: --&gt;<br />
        &lt;script type=&quot;text/javascript&quot; src=&quot;jquery-1.4.1.js&quot;&gt;&lt;/script&gt;<br />
        Nome:<br />
        &lt;input id=&quot;txtNome&quot; type=&quot;text&quot; /&gt;<br />
        Idade:<br />
        &lt;input id=&quot;txtIdade&quot; type=&quot;text&quot; /&gt;<br />
        Formado:<br />
        &lt;input id=&quot;chkFormado&quot; type=&quot;checkbox&quot; /&gt;Sim</p>
<p>        &lt;input id=&quot;btnEnviar&quot; type=&quot;button&quot; value=&quot;Enviar&quot; /&gt;<br />
[/sourcecode]</p>
<p><span style="color: #000000;"><strong>Com a classe declarada, fica mais legível e organizado manipular seus dados:</strong></span></p>
<p>[sourcecode language="javascript"]<br />
      $(function () {<br />
            //Evento click do botão Enviar<br />
            $('#btnEnviar').click(function () {</p>
<p>                //Instaciação de um objeto da classe Pessoa<br />
                var _pessoa = new Pessoa();</p>
<p>                //Acessando e alterando os valores dos atributos<br />
                _pessoa.nome = $('#txtNome').val();<br />
                _pessoa.idade = $('#txtIdade').val();<br />
                _pessoa.formado = $('#chkFormado').attr('checked');</p>
<p>                alert(<br />
                        'Meu nome é  ' + _pessoa.nome +<br />
                        ', tenho ' + _pessoa.idade +<br />
                        ' anos e ' +<br />
                        (_pessoa.formado ? 'já' : 'ainda não') + ' sou formado'<br />
                    );<br />
            });<br />
        });<br />
[/sourcecode]</p>
<p>Com o objeto definido e os valores dos seus atributos preenchidos, podemos aproveitar esta estrutura e converte-lo para o formato JSON, com a finalidade de passar esses dados para o code behind, através de um ajax, _doPostBack ou outra necessidade. Para desfrutar dessa vantagem, de maneira fácil e simples, vamos utilizar o plugin <a href="http://code.google.com/p/jquery-json/">Jquery JSON</a>.</p>
<p><strong>Adicionando referência do plugin à pagina:</strong></p>
<p>[sourcecode language="html"]<br />
        &lt;!-- :: JQUERY-JSON  :: --&gt;<br />
        &lt;script type=&quot;text/javascript&quot; src=&quot;jquery.json-2.2.js&quot;&gt;&lt;/script&gt;<br />
[/sourcecode]</p>
<p><strong>Realizando a conversão do objeto para o formato JSON:</strong></p>
<p>[sourcecode language="javascript"]<br />
        //Converte o objeto '_pessoa' para o formato Json<br />
        var string_Json = $.toJSON(_pessoa);<br />
[/sourcecode]</p>
<p><strong>Realizando a conversão de uma string no formato JSON para um objeto:</strong></p>
<p>[sourcecode language="javascript"]<br />
        //Converte uma string no formato Json para objeto<br />
        var obj = $.parseJSON(string_Json);<br />
[/sourcecode]</p>
<p>Este artigo abordou conceitos básicos do POO, mas caso você tenha mas interesse sobre esse assunto, eu indico os artigos dessa <a href="http://joaopedropereira.com/blog/2009/01/13/javascript-oop-1/">série em PT/BR</a> e dessa <a href="http://www.1stwebdesigner.com/design/object-oriented-basics-javascript/">série em EN</a> .<br />
Que são muito bons!</p>
