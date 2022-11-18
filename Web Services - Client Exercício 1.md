# WSDL

A especificação WSDL (Web Services Description Language) é uma linguagem baseada em XML que descreve de forma padronizada e independente de plataforma como e onde os serviços podem ser conectados e utilizados através da rede.  
Um documento WSDL possui o mesmo papel que a IDL da OMG nos ambientes distribuídos (WSDL, 2001), representando um contrato entre o provedor de serviços e seus clientes e definindo os serviços como uma coleção de portas na rede. Os documentos WSDL apresentam uma dicotomia entre a definição da mensagem (parte abstrata) e sua implementação (parte concreta), o que permite o reuso das definições das mensagens e port types.  
Um documento WSDL é composto por sete elementos XML que representam as partes abstrata e concreta.  
Na parte abstrata temos quatro elementos:  
1-types - fornece a definição dos tipos de dados para descrever as mensagens trocadas entre aplicações, normalmente representadas por um documento XSD (XML Schema Definition);  
2-message - representa a informação que será trocada através das definições dos tipos de dados;  
3-porttype - é um conjunto de operações suportadas por um ou mais end points, onde cada operação se refere a uma mensagem de entrada, saída ou erro;  
4-operation - descreve a ação suportada pelo serviço.  
Na parte concreta temos os outros três elementos:  
1-binding - define uma especificação de protocolo e formato de dados para as mensagens definidas em um port type;  
2-port - é um end point, representa a combinação de um binding e um endereço de rede;  
3-service - é uma coleção de portas. Cada elemento port se relaciona com um elemento binding particular, indicando qual interface e qual protocolo de comunicação estão sendo utilizados nessa implementação.


# HTTP - Métodos


## Método GET
Uma solicitação GET recupera dados de um servidor da Web especificando parâmetros na parte da URL da solicitação. Este é o principal método usado para recuperação de documentos. O exemplo a seguir usa o método GET para buscar hello.htm:

	GET /hello.htm HTTP/1.1
	User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
	Host: www.tutorialspoint.com
	Accept-Language: en-us
	Accept-Encoding: gzip, deflate
	Connection: Keep-Alive

A resposta do servidor em relação à solicitação GET acima será a seguinte:

	HTTP/1.1 200 OK
	Date: Mon, 27 Jul 2009 12:28:53 GMT
	Server: Apache/2.2.14 (Win32)
	Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
	ETag: "34aa387-d-1568eb00"
	Vary: Authorization,Accept
	Accept-Ranges: bytes
	Content-Length: 88
	Content-Type: text/html
	Connection: Closed
________________
	<html>  
	<body>  
	<h1>Hello, World!</h1>  
	</body>  
	</html>
	
## Método HEAD
O método HEAD é funcionalmente semelhante ao GET, exceto que o servidor responde com uma linha de resposta e cabeçalhos, mas sem corpo de entidade. O exemplo a seguir usa o método HEAD para buscar informações de cabeçalho sobre hello.htm:

	HEAD /hello.htm HTTP/1.1
	User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
	Host: www.tutorialspoint.com
	Accept-Language: en-us
	Accept-Encoding: gzip, deflate
	Connection: Keep-Alive

A resposta do servidor em relação à solicitação HEAD acima será a seguinte:

	HTTP/1.1 200 OK
	Date: Mon, 27 Jul 2009 12:28:53 GMT
	Server: Apache/2.2.14 (Win32)
	Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
	ETag: "34aa387-d-1568eb00"
	Vary: Authorization,Accept
	Accept-Ranges: bytes
	Content-Length: 88
	Content-Type: text/html
	Connection: Closed

Observe que aqui o servidor não envia nenhum dado após o cabeçalho.

## Método POST
O método POST é usado quando você deseja enviar alguns dados para o servidor, por exemplo, atualização de arquivo, dados de formulário, etc. O exemplo a seguir utiliza o método POST para enviar dados de formulário ao servidor, que serão processados por um process.cgi e, finalmente, uma resposta será retornada:

	POST /cgi-bin/process.cgi HTTP/1.1
	User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
	Host: www.tutorialspoint.com
	Content-Type: text/xml; charset=utf-8
	Content-Length: 88
	Accept-Language: en-us
	Accept-Encoding: gzip, deflate
	Connection: Keep-Alive
_____
	<?xml version="1.0" encoding="utf-8"?>  <string  xmlns="http://clearforest.com/">string</string>

O script do lado do servidor process.cgi processa os dados passados e envia a seguinte resposta:

	HTTP/1.1 200 OK
	Date: Mon, 27 Jul 2009 12:28:53 GMT
	Server: Apache/2.2.14 (Win32)
	Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
	ETag: "34aa387-d-1568eb00"
	Vary: Authorization,Accept
	Accept-Ranges: bytes
	Content-Length: 88
	Content-Type: text/html
	Connection: Closed
____
	<html>  <body>  <h1>Request Processed Successfully</h1>  </body>  </html>

## Método PUT
O método PUT é usado para solicitar ao servidor que armazene o corpo da entidade incluído em um local especificado pelo URL fornecido. O exemplo a seguir solicita que o servidor salve o corpo da entidade fornecido em hello.htm na raiz do servidor:

	PUT /hello.htm HTTP/1.1
	User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
	Host: www.tutorialspoint.com
	Accept-Language: en-us
	Connection: Keep-Alive
	Content-type: text/html
	Content-Length: 182
___
	<html>  <body>  <h1>Hello, World!</h1>  </body>  </html>


O servidor armazenará o corpo da entidade fornecido no arquivo hello.htm e enviará a seguinte resposta de volta ao cliente:

	HTTP/1.1 201 Created
	Date: Mon, 27 Jul 2009 12:28:53 GMT
	Server: Apache/2.2.14 (Win32)
	Content-type: text/html
	Content-length: 30
	Connection: Closed
___
	<html>  <body>  <h1>The file was created.</h1>  </body>  </html>

## Método DELETE
O método DELETE é usado para solicitar ao servidor que exclua um arquivo em um local especificado pelo URL fornecido. O exemplo a seguir solicita que o servidor exclua o arquivo hello.htm fornecido na raiz do servidor:

	DELETE /hello.htm HTTP/1.1
	User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
	Host: www.tutorialspoint.com
	Accept-Language: en-us
	Connection: Keep-Alive


O servidor excluirá o arquivo mencionado hello.htm e enviará a seguinte resposta de volta ao cliente:

	HTTP/1.1 200 OK
	Date: Mon, 27 Jul 2009 12:28:53 GMT
	Server: Apache/2.2.14 (Win32)
	Content-type: text/html
	Content-length: 30
	Connection: Closed
___
	<html>  <body>  <h1>URL deleted.</h1>  </body>  </html>

## Método CONNECT
O método CONNECT é usado pelo cliente para estabelecer uma conexão de rede com um servidor web por HTTP. O exemplo a seguir solicita uma conexão com um servidor da Web em execução no host tutorialspoint.com:

	CONNECT www.tutorialspoint.com HTTP/1.1
	User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)

A conexão é estabelecida com o servidor e a seguinte resposta é enviada de volta ao cliente:

	HTTP/1.1 200 Connection established
	Date: Mon, 27 Jul 2009 12:28:53 GMT
	Server: Apache/2.2.14 (Win32)

## Método OPTIONS 
O método OPTIONS é utilizado pelo cliente para conhecer os métodos HTTP e outras opções suportadas por um servidor web. O cliente pode especificar uma URL para o método OPTIONS ou um asterisco (*) para se referir a todo o servidor. O exemplo a seguir solicita uma lista de métodos suportados por um servidor web executado em tutorialspoint.com:

	OPTIONS * HTTP/1.1
	User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)


O servidor enviará uma informação baseada na configuração atual do servidor, por exemplo:
	
	HTTP/1.1 200 OK
	Date: Mon, 27 Jul 2009 12:28:53 GMT
	Server: Apache/2.2.14 (Win32)
	Allow: GET,HEAD,POST,OPTIONS,TRACE
	Content-Type: httpd/unix-directory

## Método TRACE 

O método TRACE é usado para ecoar o conteúdo de uma solicitação HTTP de volta ao solicitante, que pode ser usado para fins de depuração no momento do desenvolvimento. O exemplo a seguir mostra o uso do método TRACE:

	TRACE / HTTP/1.1
	Host: www.tutorialspoint.com
	User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)

O servidor enviará a seguinte mensagem em resposta à solicitação acima:

	HTTP/1.1 200 OK
	Date: Mon, 27 Jul 2009 12:28:53 GMT
	Server: Apache/2.2.14 (Win32)
	Connection: close
	Content-Type: message/http
	Content-Length: 39

	TRACE / HTTP/1.1
	Host: www.tutorialspoint.com
	User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)

## Referências

As respostas para estes exercícios foi retiradas das seguintes fontes:

http://www.nce.ufrj.br/conceito/artigos/2005/01p2-1.htm
https://www.tutorialspoint.com/http/http_methods.htm