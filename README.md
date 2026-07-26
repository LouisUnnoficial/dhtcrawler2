## dhtcrawler2

O dhtcrawler é um *crawler* de DHT escrito em Erlang. Ele pode ingressar em uma rede DHT e rastrear diversos torrents P2P. O programa salva todas as informações dos torrents em um banco de dados e disponibiliza uma interface HTTP para pesquisar torrents por palavra-chave.

![screenshot](https://raw.github.com/kevinlynx/dhtcrawler/master/screenshot.png)

O dhtcrawler2 é uma versão estendida do [dhtcrawler](https://github.com/kevinlynx/dhtcrawler). Ele apresenta uma velocidade de rastreamento muito superior e é bem mais estável. 

Esta branch do Git mantém arquivos Erlang pré-compilados para iniciar o dhtcrawler2 diretamente. Assim, você não precisa compilá-lo por conta própria; basta baixá-lo e executá-lo para coletar torrents e pesquisar torrents por palavra-chave. 

Apreciá-lo!

## Uso

* instale o Erlang R16B ou mais recente
* baixe o MongoDB e inicie o MongoDB primeiro.

        mongod --dbpath your-database-path --setParameter textSearchEnabled=true

* ara iniciar o **crawler** no Windows, basta clicar. `win_start_crawler.bat`
* para iniciar o **hash_reader** no Windows, basta clicar. `win_start_hash.bat`
* para iniciar o **httpd** no Windows, basta clicar. `win_start_http.bat`
* aguarde alguns minutos e finalize a compra. `localhost:8000`

Você também pode compilar o código-fonte e executá-lo manualmente. O código-fonte está na branch `src` deste repositório..

Você também pode conferir mais informações técnicas no meu blog (em chinês). [codemacro.com](http://codemacro.com)

## Código-fonte

O dhtcrawler é totalmente de código aberto e pode ser utilizado para qualquer finalidade; no entanto, peço que mantenha meu nome e os direitos autorais associados a mim. Você pode conferir o código-fonte do dhtcrawler2 no repositório Git, na branch **src**.

## Configuração

A maior parte das configurações encontra-se em `priv/dhtcrawler.config`; esse arquivo é gerado automaticamente na primeira execução do dhtcrawler. Os demais parâmetros de configuração são passados ​​como argumentos para funções do Erlang. Na maioria dos casos, não é necessário alterar essas configurações, exceto pelos endereços de rede.

## Conjunto de réplicas do MongoDB

Não tem relação com o dhtcrawler, mas apenas com o MongoDB; tente descobrir por conta própria.

## Mais um front-end HTTP

Sim, claro, você pode criar outra interface HTTP baseada no banco de dados de torrents; se tiver interesse, posso ajudar com informações sobre o formato do banco de dados.

## Sphinx

Sim, o dhtcrawler2 oferece suporte à busca via **Sphinx**. Existe uma ferramenta chamada `sphinx-builder` que carrega torrents do banco de dados e cria o índice do Sphinx. O `crawler-http` também pode realizar buscas de texto utilizando o Sphinx.. 

O dhtcrawler2 utiliza a busca de texto do MongoDB por padrão; para usar o Sphinx, siga os passos abaixo:

* baixe o Sphinx; a versão testada é um *fork* chamado `coreseek`, que oferece suporte a caracteres chineses. [coreseek4.1](http://www.coreseek.cn/news/14/52/)
* descompacte o arquivo binário e adicione o diretório `bin` à variável de ambiente `PATH`, para que o dhtcrawler possa invocar a ferramenta `indexer`.
* arquivo de configuração `etc/csft.conf`
    * adicione um índice delta, isto é:
        
            source delta:xml
            {
                type = xmlpipe2
                xmlpipe_command = cat g:/downloads/coreseek-4.1-win32/var/test/delta.xml
            }
            index delta:xml
            {
                source = delta
                path = g:/downloads/coreseek-4.1-win32/var/data/delta
            }

    * altere os outros diretórios; é melhor usar caminhos absolutos.
* execute `win_init_sphinx_index.bat` para gerar um arquivo de configuração padrão do sphinx-builder e encerrar `win_init_sphinx_index.bat`
* no arquivo de configuração `priv/sphinx_builder.config`, especifique os nomes dos arquivos de origem dos índices `main` e `delta` do Sphinx, os nomes dos índices `main` e `delta` e o arquivo de configuração do Sphinx; esses nomes de arquivo devem corresponder às configurações que você definir. `etc/csft.conf`
* execute `win_init_sphinx_index.bat` novamente para inicializar o arquivo de índice do Sphinx, encerre o `win_init_sphinx_index.bat` e, se ele inicializar o índice com sucesso, nunca mais o execute.
* execute o servidor `searchd` do Sphinx
* execute `win_start_sphinx_builder` para iniciar o sphinx-builder; ele lerá os torrents do seu banco de dados de torrents e criará o índice no Sphinx.
* altere o `search_method` em `priv/hash_reader.config` para `sphinx`, de modo que o `hash_reader` não construa mais o índice de busca de texto do MongoDB.
* altere o `search_method` em `priv/httpd.config` para `sphinx`, de modo que o `crawler-http` realize a busca por palavras-chave utilizando o Sphinx.

Muitos detalhes! E é bom você conhecer bem o Sphinx.

## LICENÇA

Consulte o arquivo LICENSE.txt
