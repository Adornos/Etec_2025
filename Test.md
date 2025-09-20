iSobre:

A biblioteca mysqli, [faz conexao do php com um banco de dados em mySql](#MySqli_Connect), permitindo o envio de instruções (queries) e o recebimento de Objetos do Banco.

Introdução:

<table class="ck-table-resized" style="border-style:none;"><colgroup><col style="width:48.55%;"><col style="width:51.45%;"></colgroup><tbody><tr><td style="border-style:none;text-align:justify;"><p>Para iniciar uma conexão com o server mySql, é preciso especificar os parâmetros para o acesso, estes sendo:</p><ul><li data-list-item-id="e6741c1b52d6555e58e463120eb3a0569">Endereço de hospedagem</li><li data-list-item-id="efb54990cbd345d2f56d4288cabc0b2e7">Porta (opcional)</li><li data-list-item-id="eea16b70a3b2ae0903fe0923b1f260e4b">Usuário de acesso</li><li data-list-item-id="e51d921e7b8f1404e0f9c1519c097c3de">Senha de acesso</li><li data-list-item-id="e29da963f7d0159b7870f87461d47dfc4">Nome do banco</li></ul></td><td style="border-style:none;"><pre><code class="language-text-x-php">&lt;?php

	$db_server = "localhost";
	$db_user = "root";
	$db_pass = "";
	$db_name = "db_tutorial";
	$db_port = 3306;
	
?&gt;</code></pre></td></tr><tr><td style="border-style:none;"><p>Após especificar os parâmetros de acesso ao banco, aglutina-se todos eles dentro da função de conexao, da seguinte forma:</p><p>Após o código executar essa função, ele retornará um objeto que representa a conexão com o servidor mySql. Se a conexão for mal-sucedida a função retornará <span style="color:hsl(210,75%,60%);">false</span></p></td><td style="border-style:none;"><pre><code class="language-text-x-trilium-auto">&lt;?php

	$conn = mysqli_connect( 
					$db_server,
					$db_user,
					$db_pass,
					$db_name,
					$db_port 
					);

?&gt;</code></pre></td></tr></tbody></table>

Enviando Intruções:

<table class="ck-table-resized" style="border-style:none;"><colgroup><col style="width:50.94%;"><col style="width:49.06%;"></colgroup><tbody><tr><td style="border-style:none;"><p>Depois de estabelecer a conexão com o servidor MySQL, é possível enviar comandos SQL para manipular ou consultar dados dentro do banco por da função que envia as instruções (quaries).</p><p>Após o envio das instruções há 3 casos de resposta:</p><ul><li data-list-item-id="e262ae8530713d3ea5e1f431cd4b1fd3c">Se falhar: retorna false</li><li data-list-item-id="e8eddf5cb651d00fdc43605d64b251316">Se for enviado com êxito:<ul><li data-list-item-id="e7435b5b9ebf8feecc50e7e3769769a53">Para Read: retorna um <span style="color:hsl(210,75%,60%);">objeto do banco</span>, com os dados dele.</li><li data-list-item-id="e4bc1dfcce660e41ae65598192e29b848">Outras intruções: retorna <span style="color:hsl(210,75%,60%);">true.</span></li></ul></li></ul></td><td style="border-style:none;"><pre><code class="language-text-x-trilium-auto">&lt;?php

	mysqli_query($conn, $query);

?&gt;</code></pre></td></tr></tbody></table>

Inserindo, Atualizando e Deletando dados( Create, Update, Delete ):

É possível usar o retorno como forma de verificação, mas não é necessário para inserção.

```php
<?php
	
	function db_insert(){
	
		$query = "INSERT INTO tabela(nome, sobrenome)
			  VALUES ('Luis', 'Ferreira')";

		$query_result = mysqli_query($conn, $query);
		
		return $query_result;// false em caso de falha, true em caso de sucesso
		
	}
	
	function db_Update(){
	
		$query = "UPDATE tabela
				  SET nome = 'Luiz', sobrenome = 'Ferraz'
				  WHERE id = 1";

		$query_result = mysqli_query($conn, $query);
		
		return $query_result;// false em caso de falha, true em caso de sucesso
	
	}
	
		function db_Delete(){
	
		$query = "DELETE FROM tabela
				  WHERE id = 1";

		$query_result = mysqli_query($conn, $query);
		
		return $query_result;// false em caso de falha, true em caso de sucesso
	
	}
	
?>
```

* * *

Consultando dados( Read ):

Nesse caso, o retorno da função que enviará o query será um Objeto do Banco. Para que esse dado possa ser utilizado de forma útil pelo php, é preciso converte-lo para uma Lista que pode ser iterada. Como no exemplo abaixo:

<table class="ck-table-resized" style="border-style:none;"><colgroup><col style="width:45.26%;"><col style="width:54.74%;"></colgroup><tbody><tr><td style="border-style:none;text-align:center;vertical-align:top;"><p><span style="color:hsl(210,75%,60%);">Objeto do Banco</span>&nbsp;</p><figure class="image"><img style="aspect-ratio:243/127;" src="api/attachments/Ux9jftyx7GXE/image/image.png" width="243" height="127"></figure></td><td style="border-style:none;text-align:center;vertical-align:top;"><p><span style="color:hsl(210,75%,60%);">Array Associativo</span></p><pre><code class="language-text-x-trilium-auto">$lista = [ 
	[ 
        "id" =&gt; "1",
        "nome" =&gt; "Maria",
        "sobrenome" =&gt; "Almeida"
    ],
    [
        "id" =&gt; "2",
        "nome" =&gt; "Luiz",
        "sobrenome" =&gt; "Ferraz"
    ]
]</code></pre></td></tr></tbody></table>

<table class="ck-table-resized" style="border-style:none;"><colgroup><col style="width:38.37%;"><col style="width:61.63%;"></colgroup><tbody><tr><td style="border-style:none;text-align:justify;vertical-align:top;"><p>Para realizar essa conversão, primeiramente é preciso mandar as instruções de consulta para o banco de dados:</p><p>Isto retornara os dados do banco como <span style="color:hsl(210,75%,60%);">Objeto do Banco</span></p></td><td style="border-style:none;"><pre><code class="language-text-x-trilium-auto">&lt;?php
function db_read($conn) {

  $query = "SELECT * FROM tabela";
  $query_result = mysqli_query($conn, $query);
    

}
?&gt;</code></pre></td></tr></tbody></table>

<table class="ck-table-resized" style="border-style:none;"><colgroup><col style="width:25.27%;"><col style="width:74.73%;"></colgroup><tbody><tr><td style="border-style:none;">Com o <span style="color:hsl(210,75%,60%);">Objeto do Banco</span> em mãos, é preciso iterar sobre ele com a função que converte-o automaticamente para um <span style="color:hsl(210,75%,60%);">array associativo</span>, armazenando cada uma sessas iterações num array.</td><td style="border-style:none;"><pre><code class="language-text-x-trilium-auto">&lt;?php
if ($query_result) {
	while ($linha = mysqli_fetch_assoc($query_result)) {
            	$dados[] = $row; 
            	// cada $row é um array associativo
        	}
    	}
}

return $dados
?&gt;</code></pre></td></tr></tbody></table>
