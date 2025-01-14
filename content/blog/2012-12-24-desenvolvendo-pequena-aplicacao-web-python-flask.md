+++
title = "Desenvolvendo uma pequena aplicação web com Python e Flask"
+++

<p>Neste artigo será explicado como configurar o seu ambiente de desenvolvimento, desenvolver uma aplicação web em python modularizada e no final publicá-la em um servidor free.</p>
<img class="size-full wp-image-836" title="Python-Code" src="/assets/Python-Code.png" alt="" width="480" height="333" />
<p>
    <!--more-->
</p>
<p>Tópicos abordados:</p>
<ul>
    <li><a href="#virtualenv">Virtualenv – Ambientes Virtuais Independentes</a></li>
    <li><a href="#flask">Flask – Micro Framework de desenvolvimento web para Python</a></li>
    <li><a href="#pythonanywhere">Python Any Where – Publicando de maneira simples e rápida</a></li>
</ul>
<h2><a name="virtualenv"></a>O que é o Virtualenv?</h2>
<p><img style="display: block; float: none; margin-left: auto; margin-right: auto;" src="/assets/Virtualenv.jpg" alt="" /></p>
<p>Virtualenv é um software que permite a criação de ambientes virtuais com total independência dos outros ambientes criados no Virtualenv. Isso permite que cada ambiente tenha autonomia para instalar plug-ins e bibliotecas de forma que a configuração de um ambiente não impacte nos restantes. Um exemplo prático seria a possibilidade de ter várias versões do Python, diferente para cada projeto, instalado na mesma máquina.</p>
<h3>&nbsp;</h3>
<h3>Instalando o Virtualenv</h3>
<p>Para facilitar nossa vida vamos utilizar um módulo Python chamado <strong>easy_install</strong> que gerencia pacotes Python e possui ferramentas de instalação que realiza automaticamente download, build e instalação dos pacotes disponíveis (no quais são muitos).</p>
<pre class="brush: bash; toolbar: false">sudo easy_install virtualenv</pre>
<blockquote>
    <p>Caso você não tenha o easy_install configurado em sua máquina ainda, execute o seguinte comando no Terminal:</p>
    <div id="scid:f32c3428-b7e9-4f15-a8ea-c502c7ff2e88:2df1208b-85eb-4691-a492-53210d4979e4" class="wlWriterEditableSmartContent" style="margin: 0px; display: inline; float: none; padding: 0px;">
        <pre class="brush: bash;">sudo apt-get install python-setuptools python-dev build-essential</pre>
    </div>
</blockquote>
<p>A mensagem de sucesso deverá ser algo parecida com a seguinte:</p>
<pre class="brush: shell; toolbar: false">Searching for virtualenv
Best match: virtualenv 1.8.4
Adding virtualenv 1.8.4 to easy-install.pth file
Installing virtualenv script to /usr/local/bin
Installing virtualenv-2.7 script to /usr/local/bin

Using /usr/local/lib/python2.7/dist-packages
Processing dependencies for virtualenv
Finished processing dependencies for virtualenv</pre>
<h3>Criando o Primeiro Ambiente Virtual</h3>
<p>Antes de criar o primeiro ambiente virtual vamos separar um diretório para centralizar todos os documentos, códigos-fontes, configurações e outros assuntos relacionados a Desenvolvimento em um diretório chamado Development na Home do seu usuário no Linux:</p>
<pre class="brush: bash; toolbar: false">cd ~/
mkdir Development</pre>
<p>Para manter os ambientes virtuais bem organizados, vamos criar um diretório chamado virtualenvs dentro de Development:</p>
<pre class="brush: bash; toolbar: false">cd ~/Development
mkdir virtualenvs</pre>
<p>Agora sim vamos criar nosso primeiro ambiente virtual dentro do diretório virtualenvs. Como mais pra frente nesse post irei explicar como desenvolver uma pequena aplicação, esse ambiente virtual será focado para esse projeto. Então meu ambiente virtual se chamará i-sweated-yesterday:</p>
<pre class="brush: bash; toolbar: false">cd virtualenvs
virtualenv i-sweated-yesterday</pre>
<p>A mensagem de sucesso deverá ser algo parecida com a seguinte:</p>
<pre class="brush: bash; toolbar: false">New python executable in i-sweated-yesterday/bin/python
Installing setuptools............done.
Installing pip...............done. </pre>
<blockquote>
    <p>Caso você desejasse criar um ambiente que não utilize qualquer biblioteca pré instalada no sistema operacional, deveria ser executado da forma a baixo:</p>
    <pre class="brush: bash; toolbar: false">virtualenv i-sweated-yesterday --no-site-packages</pre>
</blockquote>
<h3>&nbsp;</h3>
<h3>Utilizando o Ambiente Virtual Criado</h3>
<h4>Ativando</h4>
<p>Para utilizar o ambiente virtual você deve ativá-lo antes de realizar qualquer configuração, como instalar ou utilizar alguma biblioteca instalada no mesmo. O comando para ativar o ambiente virtual criado anteriormente é o seguinte:</p>
<pre class="brush: bash; toolbar: false">source i-sweated-yesterday/bin/activate</pre>
<p>Sempre que o ambiente virtual estiver ativado irá exibir o nome do ambiente virtual no lado esquerdo das linhas de comando no Terminal (Prompt). No meu caso fica da seguinte forma:</p>
<pre class="brush: bash; toolbar: false">(i-sweated-yesterday)max@Max-Xub-VM:~$</pre>
<p>A partir de agora qualquer configuração realizada estará associada apenas ao ambiente virtual ativo no momento.</p>
<h4>Desativando</h4>
<p>Quando não existir mais a necessidade de utilizar o ambiente virtual no momento, você pode voltar para o ambiente do sistema operacional desativando o ambiente virtual atual:</p>
<pre class="brush: bash; toolbar: false">(i-sweated-yesterday)max@Max-Xub-VM:~$ deactivate </pre>
<h4>&nbsp;</h4>
<h4>Visualizar os Pacotes Instalados no Ambiente Virtual Atual</h4>
<p>Com o ambiente virtual ativado vamos instalar o pacote chamado yolk, que possui a funcionalidade de listar os pacotes já instalados no ambiente atual:</p>
<pre class="brush: bash; toolbar: false">sudo easy_install yolk</pre>
<p>Após instalado execute o seguinte comando para visualizar os pacotes instalados:</p>
<pre class="brush: bash; toolbar: false">yolk -l</pre>
<h2><a name="flask"></a>O que é o Flask?</h2>
<p><img style="display: block; float: none; margin-left: auto; margin-right: auto;" src="/assets/Flask.jpg" alt="" /></p>
<p>Flask é um micro framework de desenvolvimento web para Python baseado em duas bibliotecas externas: O Jinja2 e o Werkzeug. Por mais que seja considerado “micro”, Flask suporta extensões de diversas funcionalidades para a sua aplicação, como integração de ORM, validação de formulários, open autenticações e outras diversas extensões.</p>
<h3>&nbsp;</h3>
<h3>Configurações</h3>
<h4>Instalando o Flask</h4>
<p>Para utilizar o Flask precisamos instalá-lo primeiro (não esqueça de ativar o ambiente virtual antes):</p>
<pre class="brush: bash; toolbar: false">pip install Flask</pre>
<p>Vamos aproveitar que estamos instalando o Flask e já vamos instalar alguns outros pacotes para estender as funcionalidades do Flask e deixar o ambiente configurado para nosso aplicativo.</p>
<h4>Instalando SQLAlchemy</h4>
<p>SQLAlchemy é uma poderosa ferramenta ORM que possibilita aos desenvolvedores trabalhar com dados armazenados no banco de dados de maneira flexível e simplificada.</p>
<pre class="brush: bash; toolbar: false">pip install SQLAlchemy</pre>
<h4>&nbsp;</h4>
<h4>Instalando o Flask-SQLAlchemy</h4>
<p>Flask-SQLAlchemy adiciona funcionalidades ao Flask que facilitam algumas tarefas comuns ao utilizar o SQLAlchemy.</p>
<pre class="brush: bash; toolbar: false">pip install flask-sqlalchemy </pre>
<h3>&nbsp;</h3>
<h4>Instalando o Flask-WTF</h4>
<p>Flask-WTF integra de maneira simples o WTForms ao Flask, fornecendo uma maneira fácil de lidar com a apresentação de dados do usuário.</p>
<pre class="brush: bash; toolbar: false">pip install Flask-WTF</pre>
<h4>Instalando o SQLite3</h4>
<p>SQLite é um pacote que disponibiliza um Sistema Gerenciador de Banco de Dados Relacional e permite ser executado através de linha de comando, possibilitando executar qualquer query SQL básica de maneira simples. (Nossa aplicação não dependerá desse pacote para ser executada, mas seria bom já instalá-lo caso surja a necessidade de executar alguma query SQL no banco)</p>
<pre class="brush: bash;">sudo apt-get install sqlite3 libsqlite3-dev</pre>
<h3>Criando uma Aplicação Flask para Teste</h3>
<p>Antes de continuar com a nossa aplicação vamos criar uma aplicação em Flask o mais simples possível, apenas para verificar se o Flask foi instalado corretamente e está funcionando da maneira esperada.</p>
<p>Crie um arquivo chamado hello.py em qualquer diretório dentro de ~/Development:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=hello.py"></script>
<p>Os parâmetros debug e port são opcionais mas facilita muito que o debug esteja ativado para visualizar erros que ocorram durante a codificação e utilizando uma porta diferente do padrão 80 possibilita que você rode mais de uma aplicação ao mesmo tempo sem ocorrer o conflito de portas.</p>
<blockquote>
    <p><strong>Definição do __name__</strong> :</p>
    <ul>
        <li>Se o módulo é executado diretamente o __name__ é __main__</li>
        <li>Se o módulo é importado por outro módulo então __name__ é o nome do próprio módulo</li>
    </ul>
</blockquote>
<p>Com o virtualenv ativado, rode a linha de comando a baixo e em seguida abra o navegador no endereço “http://localhost:8085 ”:</p>
<pre class="brush: bash; toolbar: false">python hello.py</pre>
<p>Caso esteja tudo correto então você deverá visualizar uma página com a mensagem “Hello World”.</p>
<h3>Desenvolvendo a Aplicação “I Sweated Yesterday”</h3>
<h4>I Sweated Yesterday</h4>
<p>É uma aplicação pequena e simples para controlar a frequência&nbsp; de dias que um usuário realiza exercícios físicos. É chamado “Yesterday” porque na empresa em que trabalho, sempre marcamos o exercício físico ao chegarmos na empresa no dia seguinte. Foi baseada na aplicação exemplificada por Armin Ronacher&nbsp;nesta <a href="https://github.com/mitsuhiko/flask/wiki/Large-app-how-to" target="_blank">página no Github</a>.</p>
<blockquote>
    <p>O código fonte da versão dessa aplicação&nbsp;exemplificada nesse post está disponível para download <a href="https://github.com/maxcnunes/i-sweated-yesterday/tree/v1.0">aqui</a>&nbsp;e a versão mais atual está <a href="https://github.com/maxcnunes/i-sweated-yesterday">aqui</a>, qual ainda darei mais alguns retoques.</p>
</blockquote>
<h4>Visão Geral da Estrutura do Projeto</h4>
<p>Minha dica aqui é que você crie os arquivos e diretórios abaixo para facilitar quando formos codificar ou faça o download do código fonte a cima.</p>
<h5>Diretório Base</h5>
<p><em>Possui arquivos comuns para toda aplicação</em></p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="1">
    <tbody>
        <tr>
            <td colspan="2" align="center" valign="top" width="296">/i-sweated-yesterday</td>
        </tr>
        <tr>
            <td valign="top" width="296">/i-sweated-yesterday/initialize-db.py</td>
            <td valign="top" width="293">Configurações para inicializar o banco de dados</td>
        </tr>
        <tr>
            <td valign="top" width="296">/i-sweated-yesterday/config.py</td>
            <td valign="top" width="293">Variáveis globais da aplicação</td>
        </tr>
        <tr>
            <td valign="top" width="296">/i-sweated-yesterday/app.db</td>
            <td valign="top" width="293">Arquivo de banco de dados</td>
        </tr>
        <tr>
            <td valign="top" width="296">/i-sweated-yesterday/run.py</td>
            <td valign="top" width="293">Roda a aplica cação</td>
        </tr>
    </tbody>
</table>
<h5>Diretório da Aplicação</h5>
<p><em>Possui o arquivo main, responsável por toda aplicação </em>&nbsp;</p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="1">
    <tbody>
        <tr>
            <td colspan="2" align="center" valign="top" width="302">/i-sweated-yesterday/app</td>
        </tr>
        <tr>
            <td valign="top" width="302">/i-sweated-yesterday/app/__init__.py</td>
            <td valign="top" width="288">Faz com que o Python trate o diretório como um módulo, realiza a inicialização do Flask, SQLAlchemy e realiza a configuração de rotas básicas</td>
        </tr>
    </tbody>
</table>
<h5>Diretório – Módulo Users</h5>
<p><em>Possui arquivos relacionados ao módulo Users, como formulários, classes modelos (entidade/mapeamento banco), páginas htmls…</em></p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="1">
    <tbody>
        <tr>
            <td colspan="2" align="center" valign="top" width="275">/i-sweated-yesterday/app/users</td>
        </tr>
        <tr>
            <td valign="top" width="275">/i-sweated-yesterday/app/users/__init__.py</td>
            <td valign="top" width="315">Faz com que o Python trate o diretório como um módulo</td>
        </tr>
        <tr>
            <td valign="top" width="275">/i-sweated-yesterday/app/users/views.py</td>
            <td valign="top" width="315">Onde será tratado as requisições (Similar a Controller no MVC)</td>
        </tr>
        <tr>
            <td valign="top" width="275">/i-sweated-yesterday/app/users/forms.py</td>
            <td valign="top" width="315">Definição formulários</td>
        </tr>
        <tr>
            <td valign="top" width="275">/i-sweated-yesterday/app/users/constants.py</td>
            <td valign="top" width="315">Definição de variáveis Constantes</td>
        </tr>
        <tr>
            <td valign="top" width="275">/i-sweated-yesterday/app/users/models.py</td>
            <td valign="top" width="315">Definição de Modelos</td>
        </tr>
        <tr>
            <td valign="top" width="275">/i-sweated-yesterday/app/users/decorators.py</td>
            <td valign="top" width="315">Definição de Decorators</td>
        </tr>
        <tr>
            <td valign="top" width="275">/i-sweated-yesterday/app/users/requests.py</td>
            <td valign="top" width="315">Definição de Requisições Comuns</td>
        </tr>
    </tbody>
</table>
<h5>Diretório – Módulo Exercises</h5>
<p><em>Possui arquivos relacionados ao módulo Exercises, como formulários, classes modelos (entidade/mapeamento banco), páginas htmls…</em></p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="1">
    <tbody>
        <tr>
            <td colspan="2" align="center" valign="top" width="295">/i-sweated-yesterday/app/exercises</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/exercises/__init__.py</td>
            <td valign="top" width="295">Faz com que o Python trate o diretório como um módulo</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/exercises/helpers.py</td>
            <td valign="top" width="295">Definição de algumas funções uteis</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/exercises/views.py</td>
            <td valign="top" width="295">Onde será tratado as requisições (Similar a Controller no MVC)</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/exercises/forms.py</td>
            <td valign="top" width="295">Definição formulários</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/exercises/constants.py</td>
            <td valign="top" width="295">Definição de variáveis Constantes</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/exercises/models.py</td>
            <td valign="top" width="295">Definição de Modelos</td>
        </tr>
    </tbody>
</table>
<h5>Diretório Static</h5>
<p><em>Possui arquivos estáticos como css, imagens&nbsp; e javascripts</em></p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="1">
    <tbody>
        <tr>
            <td colspan="2" align="center" valign="top" width="295">/i-sweated-yesterday/app/static</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/static/css</td>
            <td valign="top" width="295">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/static/css/reset.css</td>
            <td valign="top" width="295">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/static/css/main.css</td>
            <td valign="top" width="295">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/static/js</td>
            <td valign="top" width="295">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/static/js/main.js</td>
            <td valign="top" width="295">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="295">/i-sweated-yesterday/app/static/img</td>
            <td valign="top" width="295">&nbsp;</td>
        </tr>
    </tbody>
</table>
<h5>Diretório Templates</h5>
<p><em>Possui arquivos de templates, ou seja, todas as páginas htmls puras ou com definições Jinja2</em></p>
<table class="table_post_max" border="1" cellspacing="1" cellpadding="1">
    <tbody>
        <tr>
            <td colspan="2" align="center" valign="top" width="332">/i-sweated-yesterday/app/templates</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/base.html</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/users</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/users/register.html</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/users/profile.html</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/users/login.html</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/forms</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/forms/macros.html</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/404.html</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/exercises</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
        <tr>
            <td valign="top" width="332">/i-sweated-yesterday/app/templates/exercises/i_did.html</td>
            <td valign="top" width="258">&nbsp;</td>
        </tr>
    </tbody>
</table>
<h4>Configuração</h4>
<p>O arquivo <strong>run.py</strong> será utilizando durante o desenvolvimento para inicializar a aplicação e disponibilizar o acesso pelo browser no endereço <a href="http://localhost:8090">http://localhost:8090</a>:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=run.py"></script>
<p>O arquivo <strong>config.py</strong> será utilizado para definição de valores comuns de toda aplicação. Mantendo essas informações centralizadas nesse arquivo facilitará durante a publicação para o ambiente de produção ou de testes, que essas informações sejam alteradas de acordo com a necessita de cada ambiente:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=config.py"></script>
<blockquote>
    <p><strong>_basedir</strong> : mantém o caminho de onde os scripts são executados</p>
    <p><strong>DEBUG</strong> : utilizado como <em>True</em> em ambientes de desenvolvimento, permite que seja exibido detalhadamente a requisição, caso ocorra algum erro durante o processo</p>
    <p><strong>SECRET_KEY</strong> : utilizado na criação dos cookies</p>
    <p><strong>ADMINS</strong> : email do Administrador responsável pelo site</p>
    <p><strong>SQLALCHEMY_DATABASE_URI</strong> e <strong>DATABASE_CONNECT_OPTIONS</strong> : opções de conexão do SQLAlchemy</p>
    <p><strong>CSRF_ENABLED</strong> e <strong>CSRF_SESSION_KEY</strong> : proteção contra fraude de posts</p>
</blockquote>
<p>O arquivo <strong>initialize-db.py</strong> será utilizado para criar a estrutura de tabelas que iremos configurar mais adiante em nossas Models:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=initialize-db.py"></script>
<h4>Main</h4>
<p>O arquivo <strong>__init__.py</strong> será o main da aplicação, nele estará a definição do Flask, SQLAlchemy e as rotas comuns:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=__init__.py"></script>
<blockquote>
    <p><strong>Blueprint</strong> basicamente permite que um módulo estenda a aplicação principal e funcione similarmente a aplicação Flask. Sendo esta uma das grandes vantagem para aplicações maiores, por permitir a modularização de uma aplicação, o que facilita em muito a organização, desenvolvimento e manutenções do código fonte.</p>
    <p>Veja mais sobre <a href="http://flask.pocoo.org/docs/blueprints/">Blueprints</a>.</p>
</blockquote>
<h4>Módulo Usuário</h4>
<p>Como este será um módulo estendido da aplicação principal, o nosso arquivo <strong>__init__.py</strong> estará vazio, pois objetos que precisamos já foram inicializados pela Main.</p>
<p>O arquivo <strong>constants.py</strong> é simples e contêm apenas valores Constantes, centralizados todos no mesmo arquivo para priorizar a organização e facilitar caso surja a necessidade de alguma manutenção futura:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=constants.py"></script>
<p>O <strong>models.py</strong> contém a definição da model User, sendo basicamente estruturada pela definições de propriedades, mapeamentos model/database, construtores da classe e métodos GET e SET:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=models.py"></script>
<p>O <strong>forms.py</strong>&nbsp; utiliza o módulo <em>WTForms</em> para gerar formulários de maneira fácil e simples, como campos associados a labels e propriedades <em>Required</em>, caso seja obrigatório:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=forms.py"></script>
<p>O <strong>decorators.py</strong> possui a declaração para o decorator requires_login, no qual verifica se o usuário está logado, caso não esteja redireciona o usuário para a página de login:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=decorators.py"></script>
<blockquote>
    <p><strong>flask.g</strong> : é um objeto no Flask que possui a responsabilidade de armazenar e compartilhar dados através do tempo de execução de uma requisição</p>
    <p><strong>*args</strong> : o <strong>*</strong> é utilizado para permitir que um parâmetro aceite um número não definido de argumentos para sua função (parecido com a keyword <em>params</em> no C#)</p>
    <p><strong>**kwargs</strong> : Da mesma forma, <strong>**</strong> permite lidar com argumentos nomeados que não foram previamente definidos (parecido com a keyword <em>params+dictonary</em> no C#)</p>
</blockquote>
<p>O <strong>requests.py</strong> possui a declaração de uma função comum a várias páginas na aplicação. No qual se existir um usuário logado na requisição atual será recuperado o Id do usuário na sessão, então recupera-rá o objeto usuário no banco e será mantido até o final da requisição no objeto <strong>flask.g.user</strong>:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=requests.py"></script>
<p>O <strong>views.py</strong>, para quem está acostumado com MVC funciona como uma Controller, é onde será definido as requisições possíveis para esse módulo, associando as rotas existentes as funcionalidades específicas de cada uma. Como dito anteriormente esse módulo não será uma aplicação e sim um módulo estendido da aplicação principal. Então ao invés de utilizarmos um objeto do tipo <strong>Flask</strong>, como para a definição de rotas, iremos utilizar o <strong>Blueprint</strong>.</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=views.py"></script>
<blockquote>
    <p><strong>validate_on_submit</strong> : função do WTForm, no qual verifica se o formulário é valido durante uma requisição do tipo POST ou PUT</p>
    <p><strong>render_template</strong> : retorna um documento renderizado, no nosso caso todos html, de acordo com o arquivo template e o formulário passado</p>
    <p><strong>flash</strong> : possibilita que mensagens declaradas na view sejam recuperadas no template e exibidas para o usuário</p>
    <p><strong>@mod.route('/login/', methods=['GET', 'POST'])</strong>&nbsp; : associa uma rota a uma função que estiver após sua definição. O primeiro parâmetro define por qual caminho será executado e o segundo parâmetro quais os métodos REST serão aceitos por essa rota.</p>
</blockquote>
<h4>Templates</h4>
<p>Como Flask já possui integrado o Jinja, vamos utilizar em nossos templates algumas de suas funcionalidades disponíveis, como estruturas de condições, laços de repetições, blocos de conteúdos. Permitindo um alto nível de reutilização e fácil desenvolvimento.</p>
<p>O <strong>base.html</strong> será o template base, do qual será herdado pelos outros templates. Nesse template teremos a definição do corpo <em>HTML, HEAD, BODY</em> e blocos de conteúdo que poderão ser substituídos com outros conteúdos pelos templates que o herdarem.</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=base.html"></script>
<p>O <strong>macros.html</strong> possuirá definições de macros. No nosso caso criamos um macro chamado <strong>render_field</strong> no qual será responsável por criar uma estrutura <em>HTML</em> para os campos dos nossos formulários. Um detalhe importante desse macro é que caso exista alguma validação que não tenha passado durante a execução do <em>validate_on_submit</em> na view, então as mensagens de erro serão adicionados no <em>HTML</em> gerado.</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=macros.html"></script>
<p>O <strong>register.html</strong> herda o base.html e substitui os blocos de conteúdo <em>logout, content e footer</em>. Este template será responsável pelo <em>HTML</em> utilizado no registro de um novo usuário, por isso o método utilizado é o POST e action referencia a url atual sem o nome da página, no qual se verificarmos na view estará apontando para a função <em>register</em>:</p>
<script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=register.html"></script>
<p>A partir de agora será melhor que você siga o resto da aplicação analisando e copiando direto do código fonte disponibilizado mais a cima nesse tutorial, se não este artigo irá ficar muito maior do que já está.</p>
<h4>Executando a Aplicação</h4>
<p>No primeiro momento que executarmos a aplicação é necessário inicializar o banco de dados, para isso abra o Terminal do sistema operacional, acesse o diretório da aplicação e execute a linha de comando a baixo (não esqueça de antes ativar o ambiente virtual):</p>
<pre class="brush: bash;">python initialize-db.py</pre>
<p>Após executado a linha de comando a cima, só a execute novamente caso você deseje resetar o banco de dados, pois será criado as tabelas novamente e perderá todos os dados existentes.</p>
<p>Para inicializar a aplicação execute a linha de comando a baixo:</p>
<pre class="brush: bash;">python run.py</pre>
<p>Se a aplicação não possuir nenhuma falha grave será exibido a seguinte mensagem no Terminal:</p>
<pre class="brush: bash;"> * Running on http://127.0.0.1:8090/
 * Restarting with reloader</pre>
<p>Para visualizar a aplicação abra qualquer browser com a seguinte URL: <a title="http://127.0.0.1:8090/ " href="http://127.0.0.1:8090/">http://127.0.0.1:8090/</a>.</p>
<h2><a name="pythonanywhere"></a>O que é o Python Any Where?</h2>
<p><img style="display: block; float: none; margin-left: auto; margin-right: auto;" src="/assets/PythonAnywhere.png" alt="" /></p>
<p>O <a href="https://www.pythonanywhere.com" target="_blank">Python Any Where</a> é uma IDE online e serviço de hospedagem baseado em Python. No qual disponibiliza a hospedagem web de aplicações python e acesso ao um console online possibilitando desenvolvimento em python com várias bibliotecas disponíveis de maneira online, fácil e gratuita para o plano mais simples.</p>
<h3>Publicando</h3>
<ol>
    <li>Crie um cadastro no Python Any Where</li>
    <li>Selecione a opção <em><strong>I want to create a web application</strong></em></li>
    <li>Selecione a aba <strong><em>Web</em></strong> e em seguida a opção <em><strong>Add a new web app</strong></em></li>
    <li>Selecione <strong><em>Next</em></strong> na primeira janela</li>
    <li>Selecione <strong><em>Flask</em></strong> para definir o Framework Web Python a ser utilizado</li>
    <li>Selecione <strong><em>Next</em></strong> para confirmar o caminho físico da sua aplicação</li>
    <li>Após criada a opção <em><strong>It is configured via WSGI file stored at</strong></em> para editar arquivo wsgi</li>
    <li>
        Edite o arquivo wsgi, atualizando o valor da variável projec_home com o caminho físico correto da sua aplicação (abra a aba Files para confirmar o caminho correto) e na última linha certifique-se de estar realizando a importação correta, caso você tenha deixado a variável instanciado do Flask no arquivo __init__.py da aplicação como “app”, então você deixará a última linha da forma que está:<strong><em>/ &gt; var &gt; www &gt; YOUR-USER-NAME_pythonanywhere_com_wsgi.py</em> :</strong>
        <script src="https://gist.github.com/maxcnunes/719d948e4dd1f15c97a2.js?file=wsgi.py"></script>
    </li>
    <li>Salve o arquivo anterior</li>
    <li>Acesse a aba <strong>Files</strong> e em seguida o diretório : <strong><em>/ &gt; home &gt;&nbsp; YOUR-USER-NAME</em></strong></li>
    <li>Clique no botão <strong>Escolher Arquivo</strong></li>
    <li>Selecione o seu projeto compactado como .zip</li>
    <li>Clique em Upload</li>
    <li>Acesse a aba <strong>Consoles</strong> e selecione a opção <strong>Bash</strong></li>
    <li>
        Execute o seguinte comando no console:
        <pre class="brush: bash;">unzip SEU-PROJETO-COMPACTADO.zip </pre>
    </li>
    <li>
        Para inicializar o banco de dados execute o seguinte comando no console:
        <pre class="brush: bash;">python YOUR-PROJECT-DIRECTORY/initialize-db.py </pre>
    </li>
    <li>Acesse a aba Web e clique em <strong>Reload web app</strong></li>
    <li>Finalmente para visualizar o aplicativo rodando clique no link <strong>You can see your web app at</strong> disponível na aba Web (caso ocorra algum erro ao abrir a aplicação, veja a descrição mais detalhada do problema nos logs de erros disponíveis também na aba Web)</li>
</ol>
<blockquote>
    <p><strong>Wsgi</strong> (Web Server Gateway Interface): Define uma simples interface entre Servidores Web e Aplicações Web ou Frameworks para Python.</p>
    <p><strong>Dica</strong> : Utilizamos a função de Upload para enviar o código fonte da nossa aplicação do computador local para o servidor web. Mas seria ainda mais fácil quando utilizado o Dropbox ou melhor ainda o Github. De uma olhada nisso, vai facilitar ainda mais o deploy quando realizado várias vezes.</p>
</blockquote>