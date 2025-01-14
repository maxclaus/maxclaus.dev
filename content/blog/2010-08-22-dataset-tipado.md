+++
title = "Uma simples aplicação com DataSet Tipado"
+++

<p>Um tutorial simples de como trabalhar com DataSet Tipado no Windows Form.</p>
<p>F cil e r pido!</p>
<p><!--more--></p>
<p>Neste artigo foi feito:</p>
<ol>
<li>Criei uma tabela cliente no banco</li>
<li>Criei um formul rio Principal WindowsForm com funcionalidades de INSERT, DELETE e UPDATE</li>
<li>Criei outro formul rio Pesquisa WindowsForm com funcionalidade de SELECT e com possibilidade de selecionar o cliente desejado, para edit -lo no formul rio Principal.</li>
<li>Criei um DataSet com os métodos de SELECT, INSERT, DELETE e UPDATE.</li>
<li>Criei uma classe est tica para guardar temporariamente o cliente selecionado.</li>
</ol>
<p>Segue o video tutorial:</p>
<p>[vimeo]http://vimeo.com/14344312[/vimeo]</p>
<p>Arquivos:</p>
<p><a title="Sql do banco" href="http://www.4shared.com/document/OH6B484i/sqlCliente.html" target="_blank">Sql do Banco</a>, <a title="Projeto no Visual Studio" href="http://www.4shared.com/file/XnKZb7oR/MinhaAplicacao.html" target="_blank">Projeto no Visual Studio</a>, <a href="http://www.4shared.com/video/NwKgnKd-/VideoTutorial.html" target="_blank">Video do desenvolvimento</a></p>
<p>Como o projeto est em Visual Studio 10, aqui vão os código do formul rio principal e pesquisa.</p>
<p>frmPrincipal:</p>
<p>[sourcecode language="csharp"]<br />
using System;<br />
using System.Collections.Generic;<br />
using System.ComponentModel;<br />
using System.Data;<br />
using System.Drawing;<br />
using System.Linq;<br />
using System.Text;<br />
using System.Windows.Forms;<br />
//INCLUI O NOSSO DATASET<br />
using MinhaAplicacao.dsDadosTableAdapters;</p>
<p>namespace MinhaAplicacao<br />
{<br />
    public partial class frmPrincipal : Form<br />
    {<br />
        //Objeto TableAdapter da tabela cliente no dataset<br />
        ClienteTableAdapter clienteTA = new ClienteTableAdapter();</p>
<p>        //Limpar todos os campos<br />
        public void Limpar()<br />
{<br />
txtCodigo.Text = string.Empty;<br />
txtCodigo.Enabled = false;<br />
txtNome.Text = string.Empty;<br />
txtEmail.Text = string.Empty;<br />
cSelecinado.codigoSelecionado = 0;<br />
MessageBox.Show(&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;quot;Operação realizada com sucesso&amp;amp;amp;amp;amp;amp;amp;amp;amp;amp;quot;);<br />
}</p>
<p>        public frmPrincipal()<br />
        {<br />
            InitializeComponent();<br />
        }</p>
<p>        private void btnGravar_Click(object sender, EventArgs e)<br />
        {<br />
            try<br />
            {<br />
                if (txtCodigo.Text == string.Empty)<br />
                {<br />
                    //INSERIR NOVO CLIENTE<br />
                    clienteTA.Insert(txtNome.Text, txtEmail.Text);<br />
                }<br />
                else<br />
                {<br />
                    int codigo = Convert.ToInt32(txtCodigo.Text);<br />
                    //ATUALIZAR CLIENTE SELECIONADO<br />
                    clienteTA.UpdateCliente(txtNome.Text, txtEmail.Text, codigo);<br />
                }<br />
                Limpar();<br />
            }<br />
            catch { }</p>
<p>        }</p>
<p>        private void btnPesquisar_Click(object sender, EventArgs e)<br />
        {<br />
            frmPesquisa fPesquisa = new frmPesquisa();<br />
            //ABRIR JANELA DE PESQUISA<br />
            fPesquisa.ShowDialog();</p>
<p>            //APÃ“S FECHAR A JANELA PESQUISA, SE TIVER ALGUM CLIENTE SELECIONADO<br />
            if (cSelecinado.codigoSelecionado != 0)<br />
            {<br />
                //BUSCA OS VALORES DO CLIENTE SELECIONADO E PREENCHE OS CAMPOS<br />
                txtCodigo.Text = clienteTA.BuscarPorCodigo(cSelecinado.codigoSelecionado)[0].idCliente.ToString();<br />
                txtNome.Text = clienteTA.BuscarPorCodigo(cSelecinado.codigoSelecionado)[0].nome;<br />
                txtEmail.Text = clienteTA.BuscarPorCodigo(cSelecinado.codigoSelecionado)[0].email;<br />
            }<br />
        }</p>
<p>        private void btnDeletar_Click(object sender, EventArgs e)<br />
        {<br />
            try<br />
            {<br />
                if (txtCodigo.Text != string.Empty)<br />
                {<br />
                    //DELETA O CLIENTE SELECIONADO<br />
                    clienteTA.DeleteCliente(Convert.ToInt32(txtCodigo.Text));<br />
                }<br />
                Limpar();<br />
            }<br />
            catch { }<br />
        }<br />
    }<br />
}</p>
<p>[/sourcecode]</p>
<p>frmPesquisa</p>
<p>[sourcecode language="csharp"]<br />
using System;<br />
using System.Collections.Generic;<br />
using System.ComponentModel;<br />
using System.Data;<br />
using System.Drawing;<br />
using System.Linq;<br />
using System.Text;<br />
using System.Windows.Forms;<br />
//INCLUI O NOSSO DATASET<br />
using MinhaAplicacao.dsDadosTableAdapters;</p>
<p>namespace MinhaAplicacao<br />
{<br />
    public partial class frmPesquisa : Form<br />
    {<br />
        //Objeto TableAdapter da tabela cliente no dataset<br />
        ClienteTableAdapter clienteTA = new ClienteTableAdapter();</p>
<p>        public frmPesquisa()<br />
        {<br />
            InitializeComponent();<br />
        }</p>
<p>        private void frmPesquisa_Load(object sender, EventArgs e)<br />
        {<br />
            // TODO: This line of code loads data into the 'dsDados.Cliente' table. You can move, or remove it, as needed.<br />
            this.clienteTableAdapter.FillTodos(this.dsDados.Cliente);</p>
<p>        }</p>
<p>        private void btnPesquisar_Click(object sender, EventArgs e)<br />
        {<br />
            if (txtCodigo.Text != string.Empty)<br />
            {<br />
                int codigo = Convert.ToInt32(txtCodigo.Text);<br />
                //BUSCA CLIENTE PELO CODIGO<br />
                dataGridView1.DataSource = clienteTA.BuscarPorCodigo(codigo);<br />
            }<br />
            else if (txtNome.Text != string.Empty)<br />
            {<br />
                //BUSCA O CLIENTE PELO NOME<br />
                dataGridView1.DataSource = clienteTA.BuscarPorNome(txtNome.Text);<br />
            }<br />
            else<br />
            {<br />
                //BUSCA O CLIENTE PELO EMAIL<br />
                dataGridView1.DataSource = clienteTA.BuscarPorEmail(txtEmail.Text);<br />
            }</p>
<p>        }</p>
<p>        private void btnSelecionar_Click(object sender, EventArgs e)<br />
        {<br />
            //PEGA O CODIGO DO CLIENTE NA LINHA SELECIONADA<br />
            int codigoSelecionado = Convert.ToInt32(dataGridView1.CurrentRow.Cells[0].Value);</p>
<p>            //GUARDA ESSE CODIGO EM UMA VARIAVEL ESTATICA, PARA PODERMOS ACESSÃ-LA NO OUTRO FORMULÃRIO<br />
            cSelecinado.codigoSelecionado = codigoSelecionado;</p>
<p>            //FECHA A JENALA DE PESQUISA<br />
            this.Close();<br />
        }</p>
<p>    }<br />
}</p>
<p>[/sourcecode]</p>
<p>cSelecionado:</p>
<p>[sourcecode language="csharp"]<br />
using System;<br />
using System.Collections.Generic;<br />
using System.Linq;<br />
using System.Text;</p>
<p>namespace MinhaAplicacao<br />
{<br />
    static class cSelecinado<br />
    {<br />
        static public int codigoSelecionado = 0;<br />
    }<br />
}</p>
<p>[/sourcecode]</p>
