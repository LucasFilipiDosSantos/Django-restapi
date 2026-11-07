# django-rest-api
Meu primeiro projeto Django utilizando rest-framework.

## Instalações
- Se você deseja executar o projeto, primeiro certifique-se de ter o python instalado globalmente em seu computador. Se não, você pode obter python [aqui](https://www.python.org/downloads/ "aqui").

- Depois de fazer isso, confirme se você também instalou o virtualenv globalmente. Caso contrário, execute este:

        $ pip install virtualenv
- Logo em seguida, Git clone este repositório para o seu PC

        $ git clone https://github.com/LucasFilipiDosSantos/Django-restapi
## Depêndencias
1.  Cd em seu repositório clonado como tal:

        $ cd django-rest-api
2. Crie e ative seu ambiente virtual:

        $ virtualenv env -p python3
    
        $ source env/Scripts/Activate
3. Instale as dependências necessárias para executar o aplicativo:

        $ pip install -r requirements.txt
4.  Cd no projeto Dajngo como tal:

        $ cd huai       
5. Faça essas migrações funcionarem:

        $ python manage.py migrate

## Executá-lo
1. Inicie o servidor usando este comando simples:

        $ python manage.py runserver
2. Agora você pode acessar o serviço API de arquivo em seu navegador usando:

        http://localhost:8000/

## Endpoints
Em um REST API, endpoints (URLs) definir a estrutura da API e como os usuários finais acessam os dados de nosso aplicativo usando os métodos HTTP - GET, POST, PUT, DELETE. 

Endpoint |HTTP | CRUD | Resultado
-- | -- |-- |--
`auth/login` | POST | CREATE | Cria um novo token para o usuário logado
`auth/user` | GET | READ | Seleciona o usuário logado
`auth/user` | PUT | UPDATE | Atualiza o usuário logado
`auth/logout` | POST | CREATE | Desabilita o token gerado para o usuário
`auth/registration`| POST | CREATE | Cria um novo usuário(vendedor)
`lote/:pk` | PUT | UPDATE | Atualiza um nove lote
`lote/:pk` | DELETE | DELETE | Deleta um lote
`lote/?page=valor` | GET | READ | Seleciona todos os lotes
`lote/:pk` | GET | READ | Pega um único lote
`lote`| POST | CREATE | Cria um novo lote
`lote/:pk` | PUT | UPDATE | Atualiza um nove lote
`lote/:pk` | DELETE | DELETE | Deleta um lote
`item/?page=valor` | GET | READ | Seleciona todos os itens
`item-relat/?page=valor` | GET | READ | Seleciona todos os itens e suas respectivas relações detalhadas
`item/:pk` | GET | READ | Pega um único item
`item`| POST | CREATE | Cria um novo item
`item/:pk` | PUT | UPDATE | Atualiza um nove item
`item/:pk` | DELETE | DELETE | Deleta um item
`cliente/?page=valor` | GET | READ | Seleciona todos os clientes
`cliente/:pk` | GET | READ | Pega um único cliente
`cliente`| POST | CREATE | Cria um novo cliente
`cliente/:pk` | PUT | UPDATE | Atualiza um nove cliente
`cliente/:pk` | DELETE | DELETE | Deleta um cliente
`pedido/?page=valor` | GET | READ | Seleciona todos os pedidos
`pedido-relat/?page=valor` | GET | READ | Seleciona todos os pedidos e suas respectivas relações detalhadas
`pedido/:pk` | GET | READ | Pega um único pedido
`pedido`| POST | CREATE | Cria um novo pedido
`pedido/:pk` | PUT | UPDATE | Atualiza um nove pedido
`pedido/:pk` | DELETE | DELETE | Deleta um pedido
`relatorio/?ordering=campo&page=2` | GET | READ | Seleciona todos os pedidos e suas respectivas relações detalhadas

## Usage
### Auth endpoint
POST http://localhost:8000/auth/login/

REQUEST
```json
{
    "username": "mariasilva",
    "email": "maria.silva@exemplo.com",
    "password": "senha123exemplo"
}
```
RESPONSE
```json
{
    "key": "841bd0f3b8ff790dbce91497f676d8ae2c821ccd"
}
```
GET http://localhost:8000/auth/user/

RESPONSE
```json
{
    "pk": 2,
    "username": "mariasilva",
    "email": "maria.silva@exemplo.com",
    "first_name": "Maria Fernanda",
    "last_name": "Silva"
}
```
PUT http://localhost:8000/auth/user/

REQUEST
```json
{
    "pk": 2,
    "username": "mariasilva",
    "email": "maria.silva@exemplo.com",
    "first_name": "Maria Fernanda",
    "last_name": ""
}
```
RESPONSE
```json
{
    "pk": 2,
    "username": "mariasilva",
    "email": "maria.silva@exemplo.com",
    "first_name": "Maria Fernanda",
    "last_name": ""
}
```
POST http://localhost:8000/auth/logout/

REQUEST
```json
{

}
```
RESPONSE
```json
{
    "detail": "Successfully logged out."
}
```
POST http://localhost:8000/auth/registration

REQUEST
```json
{
    "username": "mariasilva",
    "email": "maria.silva@exemplo.com",
    "password1": "senha123exemplo",
    "password2": "senha123exemplo"
}
```
RESPONSE
```json
{
    "key": "d06b63b4b9deb606b552c5b649fb764ae6142fe2"
}
```

### Model endpoint
POST http://localhost:8000/lote/

REQUEST
```json
{
    "nome": "Lote 6",
    "quantidade": 100
}
```
RESPONSE
```json
{
    "id": 6,
    "nome": "Lote 6",
    "dt_fabric": "2020-09-07",
    "quantidade": 100
}
```
PUT http://localhost:8000/lote/6

REQUEST
```json
{
    "id": 6,
    "nome": "Lote 6",
    "dt_fabric": "2020-09-07",
    "quantidade": 300
}
```
RESPONSE
```json
{
   "id": 6,
    "nome": "Lote 6",
    "dt_fabric": "2020-09-07",
    "quantidade": 300
}
```
DELETE http://localhost:8000/lote/6

RESPONSE
```json
{
    "id": 6,
    "nome": "Lote 6",
    "dt_fabric": "2020-09-07",
    "quantidade": 300
}
```
GET http://localhost:8000/lote/

RESPONSE
```json
{
    "count": 5,
    "next": "http://localhost:8000/lote/?page=2",
    "previous": null,
    "results": [
        {
            "id": 1,
            "nome": "Item 1",
            "dt_fabric": "2020-09-07",
            "quantidade": 100
        },
        {
            "id": 2,
            "nome": "Item 2",
            "dt_fabric": "2020-09-07",
            "quantidade": 100
        }
    ]
}
```
GET http://localhost:8000/lote/?page=2
```json
{
    "count": 5,
    "next": "http://localhost:8000/lote/?page=3",
    "previous": "http://localhost:8000/lote/",
    "results": [
        {
            "id": 3,
            "nome": "Item 3",
            "dt_fabric": "2020-09-07",
            "quantidade": 100
        },
        {
            "id": 4,
            "nome": "Item 4",
            "dt_fabric": "2020-09-07",
            "quantidade": 100
        }
    ]
}
```

#### Obs: Todos endpoint models são similares ao Lote endpoint.

### Relatório endpoint
GET http://localhost:8000/relatorio/

RESPONSE
```json
{
    "count": 4,
    "next": "http://localhost:8000/relatorio/?page=2",
    "previous": null,
    "results": [
        {
            "id": 1,
            "vendedor": {
                "id": 1,
                "username": "joaosouza",
                "first_name": "",
                "last_name": "",
                "email": "joao.souza@exemplo.com",
                "last_login": "2020-09-07T08:02:16.678039Z"
            },
            "cliente": {
                "id": 2,
                "cpf": "123.456.789-00",
                "nome": "Maria Fernanda Silva",
                "dt_nasc": "2001-02-23"
            },
            "itens": [
                {
                    "id": 2,
                    "nome": "Item 2",
                    "descricao": "teste",
                    "cor": "teste",
                    "valor": "100.00",
                    "lote": {
                        "id": 2,
                        "nome": "Item 2",
                        "dt_fabric": "2020-09-07",
                        "quantidade": 100
                    }
                }
            ],
            "valor_total": "3000.00",
            "dt_compra": "2020-09-07"
        },
        {
            "id": 2,
            "vendedor": {
                "id": 2,
                "username": "mariasilva",
                "first_name": "Maria Fernanda",
                "last_name": "Silva",
                "email": "maria.silva@exemplo.com",
                "last_login": "2020-09-07T08:05:33.264891Z"
            },
            "cliente": {
                "id": 1,
                "cpf": "987.654.321-00",
                "nome": "João Pedro Souza",
                "dt_nasc": "2000-06-24"
            },
            "itens": [
                {
                    "id": 1,
                    "nome": "Item 1",
                    "descricao": "teste",
                    "cor": "teste",
                    "valor": "100.00",
                    "lote": {
                        "id": 1,
                        "nome": "Item 1",
                        "dt_fabric": "2020-09-07",
                        "quantidade": 100
                    }
                },
                {
                    "id": 3,
                    "nome": "Item 3",
                    "descricao": "teste",
                    "cor": "teste",
                    "valor": "100.00",
                    "lote": {
                        "id": 3,
                        "nome": "Item 3",
                        "dt_fabric": "2020-09-07",
                        "quantidade": 100
                    }
                }
            ],
            "valor_total": "3000.00",
            "dt_compra": "2020-09-07"
        }
    ]
}
```
GET http://localhost:8000/relatorio/?page=2

RESPONSE
```json
{
    "count": 4,
    "next": null,
    "previous": "http://localhost:8000/relatorio/",
    "results": [
        {
            "id": 3,
            "vendedor": {
                "id": 1,
                "username": "joaosouza",
                "first_name": "",
                "last_name": "",
                "email": "joao.souza@exemplo.com",
                "last_login": "2020-09-07T08:02:16.678039Z"
            },
            "cliente": {
                "id": 2,
                "cpf": "123.456.789-00",
                "nome": "Maria Fernanda Silva",
                "dt_nasc": "2001-02-23"
            },
            "itens": [
                {
                    "id": 1,
                    "nome": "Item 1",
                    "descricao": "teste",
                    "cor": "teste",
                    "valor": "100.00",
                    "lote": {
                        "id": 1,
                        "nome": "Item 1",
                        "dt_fabric": "2020-09-07",
                        "quantidade": 100
                    }
                },
                {
                    "id": 3,
                    "nome": "Item 3",
                    "descricao": "teste",
                    "cor": "teste",
                    "valor": "100.00",
                    "lote": {
                        "id": 3,
                        "nome": "Item 3",
                        "dt_fabric": "2020-09-07",
                        "quantidade": 100
                    }
                }
            ],
            "valor_total": "500.00",
            "dt_compra": "2020-09-07"
        },
        {
            "id": 4,
            "vendedor": {
                "id": 2,
                "username": "mariasilva",
                "first_name": "Maria Fernanda",
                "last_name": "Silva",
                "email": "maria.silva@exemplo.com",
                "last_login": "2020-09-07T08:05:33.264891Z"
            },
            "cliente": {
                "id": 1,
                "cpf": "987.654.321-00",
                "nome": "João Pedro Souza",
                "dt_nasc": "2000-06-24"
            },
            "itens": [
                {
                    "id": 2,
                    "nome": "Item 2",
                    "descricao": "teste",
                    "cor": "teste",
                    "valor": "100.00",
                    "lote": {
                        "id": 2,
                        "nome": "Item 2",
                        "dt_fabric": "2020-09-07",
                        "quantidade": 100
                    }
                }
            ],
            "valor_total": "10.00",
            "dt_compra": "2020-09-07"
        }
    ]
}
```
GET http://localhost:8000/relatorio/?ordering=valor_total&page=2

Order by valor_total - ascending

GET http://localhost:8000/relatorio/?-ordering=valor_total&page=2  

Order by valor_total - descending

GET http://localhost:8000/relatorio/?ordering=dt_compra&page=2   

Order by dt_compra - ascending

GET http://localhost:8000/relatorio/?-ordering=dt_compra&page=2         

Order by dt_compra - descending

RESPONSE
```json
{
    "count": 4,
    "next": null,
    "previous": "http://localhost:8000/relatorio/?ordering=valor_total",
    "results": [
        {
            "id": 1,
            "vendedor": {
                "id": 1,
                "username": "joaosouza",
                "first_name": "",
                "last_name": "",
                "email": "joao.souza@exemplo.com",
                "last_login": "2020-09-07T08:02:16.678039Z"
            },
            "cliente": {
                "id": 2,
                "cpf": "123.456.789-00",
                "nome": "Maria Fernanda Silva",
                "dt_nasc": "2001-02-23"
            },
            "itens": [
                {
                    "id": 2,
                    "nome": "Item 2",
                    "descricao": "teste",
                    "cor": "teste",
                    "valor": "100.00",
                    "lote": {
                        "id": 2,
                        "nome": "Item 2",
                        "dt_fabric": "2020-09-07",
                        "quantidade": 100
                    }
                }
            ],
            "valor_total": "3000.00",
            "dt_compra": "2020-09-07"
        },
        {
            "id": 2,
            "vendedor": {
                "id": 2,
                "username": "mariasilva",
                "first_name": "Maria Fernanda",
                "last_name": "Silva",
                "email": "maria.silva@exemplo.com",
                "last_login": "2020-09-07T08:05:33.264891Z"
            },
            "cliente": {
                "id": 1,
                "cpf": "987.654.321-00",
                "nome": "João Pedro Souza",
                "dt_nasc": "2000-06-24"
            },
            "itens": [
                {
                    "id": 1,
                    "nome": "Item 1",
                    "descricao": "teste",
                    "cor": "teste",
                    "valor": "100.00",
                    "lote": {
                        "id": 1,
                        "nome": "Item 1",
                        "dt_fabric": "2020-09-07",
                        "quantidade": 100
                    }
                },
                {
                    "id": 3,
                    "nome": "Item 3",
                    "descricao": "teste",
                    "cor": "teste",
                    "valor": "100.00",
                    "lote": {
                        "id": 3,
                        "nome": "Item 3",
                        "dt_fabric": "2020-09-07",
                        "quantidade": 100
                    }
                }
            ],
            "valor_total": "3000.00",
            "dt_compra": "2020-09-07"
        }
    ]
}
```
