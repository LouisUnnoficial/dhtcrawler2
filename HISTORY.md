## 08.03.2013

* o Sphinx Search está estável no momento; você pode configurá-lo para uso.
* modificar a biblioteca Giza para permitir a obtenção de estatísticas de busca do Sphinx a partir da resposta.
* adicionar navegação de página ao http

## 07.30.2013

* adicionar o Sphinx (Coreseek, baseado no Sphinx) para auxiliar na busca; em fase experimental.

## 07.21.2013

* reescreva o hash_reader; agora ele manterá um cache wait_download.
* alterar hash_writer(crawler) para inserir um hash único

## 07.19.2013

* adicionado uma API simples de busca JSON ao HTTP.

## 07.15.2013

* o crawler agora manterá um cache de hashes e mesclará hashes idênticos dentro dele; isso faz com que o hash_reader processe menos hashes.

## 07.08.2013

* adicionado um importador de torrents capaz de importar torrents locais para o banco de dados de torrents.

## 07.05.2013

* adicionado um baixador de torrents que baixe torrents e os armazene em um banco de dados ou no sistema de arquivos local.
* o hash_reader agora prioriza o uso de torrents locais; caso contrário, ele fará o download e, dependendo da configuração, também poderá salvar o arquivo.

