# WMSExpert Integra
**Documentação de integração WMSExpert**

> Em todo campo de um <strong>JSON</strong> que apresentar antes dos dois pontos (:) o ponto de interrogação (?) significará que o campo não é obrigatório ser passado.

> Os campos <strong>page</strong> e <strong>size</strong> sempre que solicitados em uma requisição serão obrigatórios.

# Autenticação <br />

> É o primeiro processo que tem que ser feito para poder usar a api. Ela retornará o token de acesso fundamental para o funcionamento e segurança da aplicação.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/auth   
```

> corpo da requisição. Todos os campos não apresetação tamanho minímo ou máximo, apenas estarem cadastrados no sistema.  

```
    {
    "login" : string,
    "senha" : string,
    "filial" : interger
    }

```

# Produtos

### Lista de Produtos </br>

> O método de envio para pegar os produtos cadastros no sistema. URL de envio e o método de envio correspondente.

```
    get: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto/geral   
```

> A api retornará uma lista de produtos na seguinte estrutura.


```
[
    {
        "altura": integer,
        "codigo": string (30),
        "codigoref": string (30),
        "controlalote": boolean,
        "controlanumserie": boolean,
        "controlavalidade": boolean,
        "empresa": integer,
        "endereco": integer,
        "estoquemaximo": integer,
        "estoqueminimo": integer,
        "fornecedor": integer,
        "grupo": integer,
        "id": integer,
        "lastro": integer,
        "nome": string (100),
        "pesobruto": integer,
        "pesoliquido": integer,
        "shelflife": integer,
        "subgrupo": integer,
        "unidadepadrao": string (100)
    }
]
```

### Buscar Produto <br />

> O método de envio para pegar um produto específico cadastrado dentro do sistema. URL de envio e o método de envio correspondente.

```
    get: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto/[{idDoProdutoProcurado}]   
```

> A api retornará, caso existente, o produto na seguinte estrutura.


```
    {
        "altura": integer,
        "codigo": string (30),
        "codigoref": string (30),
        "controlalote": boolean,
        "controlanumserie": boolean,
        "controlavalidade": boolean,
        "empresa": integer,
        "endereco": integer,
        "estoquemaximo": integer,
        "estoqueminimo": integer,
        "fornecedor": integer,
        "grupo": integer,
        "id": integer,
        "lastro": integer,
        "nome": string (100),
        "pesobruto": integer,
        "pesoliquido": integer,
        "shelflife": integer,
        "subgrupo": integer,
        "unidadepadrao": string (100)
    }
```


### Filtrar Produtos <br />

> O método de envio para pegar produtos cadastrados que atendam os valores dos campos passados dentro da request. Abaixo a URL de envio e o método de envio correspondente.

```
    get: https://wmsexpert-api-55cc6cff3437.herokuapp.com/produto/geral/filtro   
```

> Tipos que poderão ser passados dentro do campo sort.

```
  [ 
    "altura", 
  "unidadepadrao", 
  "subgrupo", 
  "shelflife", 
  "pesoliquido", 
  "pesobruto", 
  "nome", 
  "lastro", 
  "id", 
  "grupo", 
  "fornecedor", 
  "estoqueminimo", 
  "endereco", 
  "empresa", 
  "controlavalidade", 
  "codigo", 
  "codigoref", 
  "controlalote", 
  "controlanumserie" 
  ]
```

> A seguir os parametros a serem passados na request: 

```
    {
        page: integer,
        size: integer,
        sort?: enum,
        idproduto?: integer,
        codigo?: string,
        descricao?: string,
        idendereco?: integer       *obs: esse idendereco é associado ao produto. Portanto, não adiantará passar endereços aleatoriamentes, pois apenas trará caso exista algum produto associado. 
    }
```

> A api retornará, caso existente, os produtos na seguinte estrutura.

```
   [
     {
        "altura": integer,
        "codigo": string (30),
        "codigoref": string (30),
        "controlalote": boolean,
        "controlanumserie": boolean,
        "controlavalidade": boolean,
        "empresa": integer,
        "endereco": integer,
        "estoquemaximo": integer,
        "estoqueminimo": integer,
        "fornecedor": integer,
        "grupo": integer,
        "id": integer,
        "lastro": integer,
        "nome": string (100),
        "pesobruto": integer,
        "pesoliquido": integer,
        "shelflife": integer,
        "subgrupo": integer,
        "unidadepadrao": string (100)
    }
   ]
```

### Busca de Produto Por Embalagem

> O método de envio para pegar produtos cadastrados que atendam os valores dos campos passados dentro da request. Abaixo a URL de envio e o método de envio correspondente.

```
    get: https://wmsexpert-api-55cc6cff3437.herokuapp.com/produto/geral/consulta   
```

> Há apenas um parametro a ser passado nessa request:

```
    {
        codbarraprod: string
    }
```

> A api retornará, caso existente, os produtos na seguinte estrutura.

```
   [
     {
        "altura": integer,
        "codigo": string (30),
        "codigoref": string (30),
        "controlalote": boolean,
        "controlanumserie": boolean,
        "controlavalidade": boolean,
        "empresa": integer,
        "endereco": integer,
        "estoquemaximo": integer,
        "estoqueminimo": integer,
        "fornecedor": integer,
        "grupo": integer,
        "id": integer,
        "lastro": integer,
        "nome": string (100),
        "pesobruto": integer,
        "pesoliquido": integer,
        "shelflife": integer,
        "subgrupo": integer,
        "unidadepadrao": string (100)
    }
   ]
```


### Salvar Produto

> O método de gravação de produto. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto   
```

> A estrutura do produto precisa seguir as seguinte regra.

```
    {
        "altura": integer,
        "codigo": string (30),
        "codigoref": string (30),
        "controlalote": boolean,
        "controlanumserie": boolean,
        "controlavalidade": boolean,
        "embalagens": [
            {
                "altura": integer,
                "ativo": boolean,
                "codbarra": string (20),
                "codigo": string (30),
                "embalagem": string (20),
                "largura": integer,
                "m3": integer,
                "pesobruto": integer,
                "pesoliquido": integer,
                "profundidade": integer,
                "quantidade": integer,
                "tipo": integer
            }
        ],
        "endereco": integer,
        "estoquemaximo": integer,
        "estoqueminimo": integer,
        "fornecedor": integer,
        "grupo": integer,
        "lastro": integer,
        "nome": string (100),
        "pesobruto": numeric(10,4),
        "pesoliquido": numeric(10,4),
        "shelflife": integer,
        "subgrupo": integer,
        "unidadepadrao": string(100)
    }
```

### Editar Produto

> O método de envio para pegar um produto específico cadastrado e atualizar. URL de envio e o método de envio correspondente.

```
    put: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto/geral/{[idproduto]}   
```

> A estrutura do produto precisa seguir as seguinte regra.

```
    {
        "altura": integer | null,
        "codigo": string,
        "codigoref": string,
        "controlalote": boolean,
        "controlanumserie": boolean,
        "controlavalidade": boolean,
        "endereco": integer | null,
        "estoquemaximo": integer,
        "estoqueminimo": integer,
        "fornecedor": integer,
        "grupo": integer | null,
        "lastro": integer,
        "nome": string,
        "pesobruto": integer | null,
        "pesoliquido": integer | null,
        "shelflife": integer | null,
        "subgrupo": integer | null,
        "unidadepadrao": string
    }
```

### Deletar Produto

> O método de envio para deletar um produto. URL de envio e o método de envio correspondente.

```
    delete: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto/{[idproduto]}   
```

# Embalagem

> As embalagens cadastras no sistema.


### Salvar Embalagem

> O método de envio gravar uma embalagem. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto/embalagem   
```

> A estrutura do produto precisa seguir as seguinte regra.

```
    {
        "codigo" : string (30),
        "produto" : integer, * obs => Aqui é o id do produto existente no sistema.
        "codbarra" : string (20),
        "embalagem" : string (20),
        "quantidade" : double,
        "ativo" : boolean,
        "tipo" : integer,   * obs => Precisa ser um id de tipo cadastrado no sistema.
        "largura" : numeric(10,4) | null,
        "altura" : numeric(10,4) | null,
        "profundidade" : numeric(10,4) | null,
        "m3" : numeric(10,4) | null,
        "pesobruto" : numeric(10,4) | null,
        "pesoliquido" : numeric(10,4) | null 
    }
```

### Editar Embalagem 

> O método de envio para pegar e gravar os campos alterados de uma embalagem. URL de envio e o método de envio correspondente.

```
    put: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto/embalagem/[{idEmbalagem}]   
```

> A estrutura da embalagem precisa seguir as seguinte regra.

```
    {
        "codigo" : string,
        "produto" : integer, * obs => Aqui é o id do produto existente no sistema.
        "codbarra" : string,
        "embalagem" : string,
        "quantidade" : double,
        "ativo" : boolean,
        "tipo" : integer,   * obs => Precisa ser um id de tipo cadastrado no sistema.
        "largura" : double | null,
        "altura" : double | null,
        "profundidade" : double | null,
        "m3" : double | null,
        "pesobruto" : double | null,
        "pesoliquido" : double | null 
    }
```

### Deletar Embalagem

> O método de envio para deletar um produto. URL de envio e o método de envio correspondente.

```
    delete: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto/embalagem/{[idEmbalagem]}   
```

# Fornecedores

> As fornecedores cadastros no sistema.


### Salvar Fornecedor

> O método de envio gravar uma embalagem. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/fornecedor  
```

> A estrutura do fornecedor precisa seguir as seguinte regra.

```
    {
        "codigo" : string (30),
        "nome" : string (100),
        "nomefantasia" : string (100),
        "cpf" : string (11),
        "ie" : string (10),
        "estado" : string (2),
        "codcidade" : string (10),
        "bairro" : string (100),
        "endereco" : string (150),
        "telefone" : string (12)
    }
```

### Editar Fornecedor

> O método de envio para pegar e gravar os campos alterados de uma fornecedor. URL de envio e o método de envio correspondente.

```
    put: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/fornecedor/[{idFornecedor}]   
```

> A estrutura do fornecedor precisa seguir as seguinte regra.

```
    {
        "codigo" : string (30),
        "nome" : string (100),
        "nomefantasia" : string (100),
        "cpf" : string (11),
        "ie" : string (10),
        "estado" : string (2),
        "codcidade" : string (10),
        "bairro" : string (100),
        "endereco" : string (150),
        "telefone" : string (12)
    }
```

### Deletar Fornecedor

> O método de envio para deletar um fornecedor. URL de envio e o método de envio correspondente.

```
    delete: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/fornecedor/{[idFornecedor]}   
```


# Cliente

> Os clientes cadastros no sistema.


### Salvar Cliente

> O método de envio gravar um cliente. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/cliente/geral  
```

> A estrutura do json cliente precisa seguir as seguinte regra.

```
    {
        "codigo" : string (30),
        "rota" : integer,  * obs => id da rota cadastrado no sistema.
        "cpfcnpj" : string (14),
        "nome" : string (100),
        "ie" : string (10),
        "codcidade" : integer,
        "nomecidade" : string (100),
        "endereco" : string (150),
        "complemento" : string (150),
        "numero" : integer,
        "bairro" : string (120),
        "cep" : string (8),  * obs => 8 numeros obrigatório 
        "telefone" : string (12),  * obs => minimo de 12 digítos, maximo de 14 minimos. 
        "email" : string (50),
        "ativo" : boolean,
        "latitude" : string (100),
        "longetude" : string (100),
        "shelflife" : string (100)
    }
```

### Editar Cliente

> O método de envio para pegar e gravar os campos alterados de um cliente. URL de envio e o método de envio correspondente.

```
    put: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/cliente/geral/[{idCliente}]   
```

> A estrutura do cliente precisa seguir as seguinte regra.

```
    {
        "codigo" : string (30),
        "rota" : integer,  * obs => id da rota cadastrado no sistema.
        "cpfcnpj" : string (14),
        "nome" : string (100),
        "ie" : string (10),
        "codcidade" : integer,
        "nomecidade" : string (100),
        "endereco" : string (150),
        "complemento" : string (150),
        "numero" : integer,
        "bairro" : string (120),
        "cep" : string (8),  * obs => 8 numeros obrigatório 
        "telefone" : string (12),  * obs => minimo de 12 digítos, maximo de 14 minimos. 
        "email" : string (50),
        "ativo" : boolean,
        "latitude" : string (100),
        "longetude" : string (100),
        "shelflife" : string (100)
    }
```

### Deletar Cliente

> O método de envio para deletar um cliente. URL de envio e o método de envio correspondente.

```
    delete: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/cliente/geral/[{idCliente}]   
```

# Rota

> As rotas cadastras no sistema.

### Salvar Rotas

> O método de envio gravar uma rota. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/cliente/rota  
```

> A estrutura da rota precisa seguir as seguinte regra.

```
    {
       "codigo" : string (30),
        "regiao" : integer,  * obs => id da região que foi cadastrado no sistema.
        "nome" : string (100),
        "ativo" : boolean
    }
```

### Editar Rota

> O método de envio para pegar e gravar os campos alterados de uma rota. URL de envio e o método de envio correspondente.

```
    put: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/cliente/rota/[{idRota}]   
```

> A estrutura do produto precisa seguir as seguinte regra.

```
   {
       "codigo" : string (30),
        "regiao" : integer,  * obs => id da região que foi cadastrado no sistema.
        "nome" : string (100),
        "ativo" : boolean
    }
```

### Deletar Rota

> O método de envio para deletar um rota. URL de envio e o método de envio correspondente.

```
    delete: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/cliente/rota/[{idCliente}]   
```

# Transportadora

> As transportadoras cadastras no sistema.

### Salvar Transportadora

> O método de envio gravar uma transportadora. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/transportadora/geral  
```

> A estrutura da rota precisa seguir as seguinte regra.

```
    {
        "tipo" : integer,
        "nome" : string (100),
        "nomefantasia" : string (100),
        "cpfcnpj" : string (14),
        "ie" : string (10),
        "estado" : string (2),
        "codcidade" : interger,
        "endereco" : string (150),
        "complemento" : string (150),
        "numero" : integer,
        "bairro" : string (100),
        "cep" : string (8),    *obs => necessário ter 8 digítos.
        "telefone" : string (12),
        "contato" : string (50),
        "ativo" : boolean,
        "obs" : string (150),
        "email" : string (100)
    }
```

### Editar Transportadora

> O método de envio para pegar e gravar os campos alterados de uma transportadora. URL de envio e o método de envio correspondente.

```
    put: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/transportadora/geral/[{idTransportadora}]   
```

> A estrutura da transportadora precisa seguir as seguinte regra.

```
   {
        "tipo" : integer,
        "nome" : string (100),
        "nomefantasia" : string (100),
        "cpfcnpj" : string (14),
        "ie" : string (10),
        "estado" : string (2),
        "codcidade" : interger,
        "endereco" : string (150),
        "complemento" : string (150),
        "numero" : integer,
        "bairro" : string (100),
        "cep" : string (8),    *obs => necessário ter 8 digítos.
        "telefone" : string (12),
        "contato" : string (50),
        "ativo" : boolean,
        "obs" : string (150),
        "email" : string (100)
    }
```

### Deletar Transportadora

> O método de envio para deletar um transportadora. URL de envio e o método de envio correspondente.

```
    delete: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/transportadora/geral/[{idTransportadora}]   
```


# Veículos

> Os veiculos das transportadoras cadastrados no sistema.

### Salvar Veículos

> O método de envio gravar uma transportadora. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/transportadora/veiculo  
```

> A estrutura do json veículo precisa seguir as seguinte regra.

```
    {
       "codigo" : string,
        "nome" : string (100),
        "nomefantasia" : string (100),
        "chassi" : string (100),
        "transportadora" : integer,  * obs => obrigatóriamente, precisa ser o id de uma transportadora cadastrada.
        "taraveiculo" : numeric(10,4),
        "pesominimo" : numeric(10,4),
        "pesomaximo" : numeric(10,4),
        "lastro" : numeric(10,4),
        "altura" : numeric(10,4),
        "profundidade" : numeric(10,4),
        "m3" : numeric(10,4),
        "ativo" : boolean
    }
```

### Editar Veículo

> O método de envio para pegar e gravar os campos alterados de uma Veículo. URL de envio e o método de envio correspondente.

```
    put: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/transportadoraveiculo/[{idVeiculo}]   
```

> A estrutura da transportadora precisa seguir as seguinte regra.

```
      {
       "codigo" : string,
        "nome" : string (100),
        "nomefantasia" : string (100),
        "chassi" : string (100),
        "transportadora" : integer,  * obs => obrigatóriamente, precisa ser o id de uma transportadora cadastrada.
        "taraveiculo" : numeric(10,4),
        "pesominimo" : numeric(10,4),
        "pesomaximo" : numeric(10,4),
        "lastro" : numeric(10,4),
        "altura" : numeric(10,4),
        "profundidade" : numeric(10,4),
        "m3" : numeric(10,4),
        "ativo" : boolean
    }
```

### Deletar Veículo

> O método de envio para deletar um veículo. URL de envio e o método de envio correspondente.

```
    delete: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/transportadoraveiculo/[{idVeiculo}]   
```


# Pedido

> Integração com pedidos cadastrados no sistema.

### Salvar Pedidos

> O método de envio gravar um pedido. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/integracao/pedido 
```

> A estrutura do json pedido precisa seguir as seguinte regra.

```
    {
       "codigo" : string (30),
        "cliente" : integer,  * obs => id do cliente cadastrado no sistema.
        "vendedor" : string (100),
        "tipo" : integer,
        "dataimportacao" : datetime,  * obs => formato "20/05/2023 00:00:00".
        "totalpedido" : numeric(10,4),
        "qtditens" : numeric(10,4),
        "ordempedido" : integer,
        "status" : integer,
        "dtexportacao" : datetime,  * obs => formato "20/05/2023 00:00:00".
        "itens" : [
            {
                "produto" : integer,
                "quantidade" : numeric(10,4),
                "qtdseparada" : numeric(10,4),
                "qtdconferida" : numeric(10,4),
                "qtdcortada" : numeric(10,4),
                "itempedido" : string (10)
            }
        ]
        }
```

### Editar Pedido

> O método de envio para pegar e gravar os campos alterados de um pedido. URL de envio e o método de envio correspondente.

```
    put: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/integracao/pedido/[{idVeiculo}]   
```

> A estrutura do pedido precisa seguir as seguinte regra.

```
    {
       "codigo" : string (30),
        "cliente" : integer,  * obs => id do cliente cadastrado no sistema.
        "vendedor" : string (100),
        "tipo" : integer,
        "dataimportacao" : datetime,  * obs => formato "20/05/2023 00:00:00".
        "totalpedido" : numeric(10,4),
        "qtditens" : numeric(10,4),
        "ordempedido" : integer,
        "status" : integer,
        "dtexportacao" : datetime,  * obs => formato "20/05/2023 00:00:00".
        "itens" : [
            {
                "produto" : integer,
                "quantidade" : numeric(10,4),
                "qtdseparada" : numeric(10,4),
                "qtdconferida" : numeric(10,4),
                "qtdcortada" : numeric(10,4),
                "itempedido" : string (10)
            }
        ]
      
    }
```

### Deletar Pedido

> O método de envio para deletar um pedido. URL de envio e o método de envio correspondente.

```
    delete: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/pedido/geral/[{idPedido}]   
```



# Nota Fiscal

> Integração com as Notas Fiscais cadastradas no sistema.

### Salvar Nota Fiscal Entrada

> O método de envio gravar um nota fiscal e seus itens. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/integracao/nfentrada/nota
```

> A estrutura do json nota fiscal precisa seguir as seguinte regra.

```
    {
       "codigo" : string (30),
        "fornecedor" : integer,  * obs => id do fornecedor necessariamente cadastrado no sistema.
        "tipo" : integer,  * obs => id do tipo necessariamente cadastrado no sistema.
        "dataemissao" : date, * obs => formato "dd/mm/yyyy".
        "quantidade" : numeric(10,4),
        "numeronotafiscal" : string (50),
        "serie" : string (50),
        "quantidadevolume" : integer,
        "valtotalproduto" : numeric(10,4),
        "valtotalnota" : numeric(10,4),
        "pesobruto" : numeric(10,4),
        "pesoliquido" : numeric(10,4),
        "situacao" : integer,
        "qtdvolumeconf" : integer,
        "itens" : [
            {
                "produto" : integer,
                "fornecedor" : integer,
                "quantidade" : numeric(10,4),
                "valunitario" : numeric(10,4),
                "item" : string(50),
                "validade" : date,  * obs => formato "dd/mm/yyyy".
                "fabricacao" :  date,  * obs => formato "dd/mm/yyyy".
                "lote" : string (50),
                "numserie" : string (50)
            }
        ]
    }
```

### Salvar Carga Fiscal Entrada

> O método de envio gravar um nota fiscal e seus itens. URL de envio e o método de envio correspondente.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/integracao/nfentrada/carga
```

> A estrutura do json carga fiscal precisa seguir as seguinte regra.

```
    {
        "deposito" : integer,  * obs => id de deposito cadastrado no sistema.
        "datainicioconf" : datetime,  * obs => formato "20/02/2023 00:00:00"
        "dataexportacaoerp" : datetime,  * obs => formato "20/02/2023 00:00:00"
        "qtdvolumes" : integer,
        "nome" : string (100),
        "datafimconf" : datetime,  * obs => formato "20/02/2023 00:00:00"
        "situacao" : integer,
        "notas" : [
            {
                "codigo" : string (30),
                "fornecedor" : integer < maior que 0 >,
                "tipo" : integer < maior que 0 >,
                "dataemissao" : date,  * obs => formato  "30/06/2023"
                "quantidade" : numeric(10,4),
                "numeronotafiscal" : string (50),
                "serie" : string (50),
                "quantidadevolume" : integer,
                "valtotalproduto" : numeric(10,4),
                "valtotalnota" : numeric(10,4),
                "pesobruto" : numeric(10,4),
                "pesoliquido" : numeric(10,4),
                "situacao" : integer,
                "qtdvolumeconf" : integer,
                "itens" : [
                    {
                        "produto" : integer < maior que 0 >,  * obs => id do produto existente no sistema.
                        "fornecedor" : integer < maior que 0 >,  * obs => id do fornecedor existente no sistema.
                        "quantidade" : numeric(10,4),
                        "valunitario" : numeric(10,4),
                        "item": string (50) | null,
                        "validade": date | null,  * obs => formato  "30/06/2023"
                        "fabricacao": date | null,  * obs => formato  "30/06/2023"
                        "lote" : string (50) | null,
                        "numserie" : string (50) | null
                    }
                ]
            }
        ]
    }
```

### Editar Nota Fiscal

> O método de envio para pegar e gravar os campos alterados de uma nota fiscal. URL de envio e o método de envio correspondente.

```
    put: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/nfentrada/geral/[{idNotaFiscal}]   
```

> A estrutura da nota fiscal do tipo <strong>entrada</strong> precisa seguir as seguinte regra.

```
    {
        "codigo" : string,
        "fornecedor" : integer,
        "tipo" : integer,  * obs => id do tipo.
        "carga" : integer, * obs => id da carga.
        "dataemissao" : date,  * obs => formato da date "07/12/2023"
        "quantidade" : double,
        "numeronotafiscal" : string,
        "serie" : string,
        "quantidadevolume" : integer,
        "valtotalproduto" : double,
        "valtotalnota" : double,
        "pesobruto" : double,
        "pesoliquido" : double,
        "situacao" : integer,
        "qtdvolumeconf" : integer
    }
```

### Deletar Nota Fiscal Tipo Entrada

> O método de envio para deletar uma nota fiscal entrada. URL de envio e o método de envio correspondente.

```
    delete: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/nfentrada/geral/[{idPedido}]   
```
