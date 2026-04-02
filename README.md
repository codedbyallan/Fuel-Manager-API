# Fuel Manager API

API REST desenvolvida em **ASP.NET Core Web API** para gerenciamento de **veículos** e **consumos de combustível**, com persistência em banco relacional via **Entity Framework Core**, autenticação baseada em **JWT** e documentação interativa com **Swagger**.

Este projeto foi construído com foco em prática acadêmica e evolução técnica em **back-end com .NET**, cobrindo conceitos importantes como modelagem de entidades, relacionamentos, CRUD, autenticação, migrations, HATEOAS e organização de uma API moderna.

---

## Sobre o projeto

O **Fuel Manager API** centraliza operações de cadastro e controle de veículos, abastecimentos e usuários, oferecendo endpoints protegidos, estrutura relacional consistente e respostas enriquecidas com **HATEOAS**.

O sistema permite:

- gerenciamento de veículos
- gerenciamento de consumos
- gerenciamento de usuários
- associação entre usuários e veículos
- autenticação com JWT
- autorização por perfil (Admin / User)

A proposta do projeto é servir como base prática para estudo e portfólio, demonstrando domínio em:

- construção de APIs REST com ASP.NET Core
- modelagem de domínio com Entity Framework Core
- autenticação com JWT
- documentação com Swagger
- uso de migrations para versionamento do banco
- implementação de HATEOAS em respostas da API
- relacionamento entre entidades

---

## Principais destaques

- API construída com **.NET 8**
- Arquitetura baseada em **Controllers**
- Persistência com **Entity Framework Core**
- Banco configurado com **SQL Server / LocalDB**
- Autenticação com **JWT Bearer**
- Endpoints protegidos com **[Authorize]**
- Regra de autorização por perfil em rota administrativa
- Documentação automática com **Swagger**
- Relacionamento entre **veículos**, **consumos** e **usuários**
- Respostas enriquecidas com **links HATEOAS**

---

## Stack Utilizada

- **C#**
- **.NET 8**
- **ASP.NET Core Web API**
- **Entity Framework Core**
- **SQL Server / LocalDB**
- **JWT Bearer Authentication**
- **Swagger / OpenAPI**
- **BCrypt.Net-Next**

---

## Funcionalidades implementadas

### Usuários
- cadastrar usuário
- listar usuários
- buscar usuário por ID
- atualizar usuário
- excluir usuário
- autenticar usuário (geração de token JWT)
- criptografia de senha com **BCrypt**
- definição de perfil (**Admin** ou **User**)

### Veículos
- cadastrar veículo
- listar veículos
- buscar veículo por ID
- atualizar veículo
- excluir veículo (apenas Admin)
- associar usuário a um veículo
- remover vínculo entre usuário e veículo
- retornar consumos e usuários relacionados no detalhe

### Consumos
- cadastrar consumo
- listar consumos
- buscar consumo por ID
- atualizar consumo
- excluir consumo

---

## Segurança

A API possui autenticação configurada com **JWT Bearer**.

### Fluxo de autenticação
1. Usuário realiza login
2. API valida usuário e senha
3. Senha é verificada com **BCrypt**
4. API gera um **Token JWT**
5. O token deve ser enviado nas próximas requisições:
   ```
   Authorization: Bearer SEU_TOKEN
   ```

### Regras de autorização
- Rotas protegidas com **[Authorize]**
- Exclusão de veículos restrita ao perfil **Admin**
- Usuários possuem perfis:
  - `Admin`
  - `User`

---

## Modelagem principal

### Veículo
- `Id`
- `Marca`
- `Modelo`
- `Placa`
- `AnoFabricacao`
- `AnoModelo`

### Consumo
- `Id`
- `Descricao`
- `Data`
- `Valor`
- `Tipo`
- `VeiculoId`

### Usuário
- `Id`
- `Nome`
- `Password`
- `Perfil`

### Associação
- `VeiculoUsuarios`

---

## Relacionamentos

O sistema possui os seguintes relacionamentos:

- um veículo pode ter vários consumos
- um veículo pode estar associado a vários usuários
- um usuário pode estar associado a vários veículos

Relacionamento muitos-para-muitos implementado através da tabela **VeiculoUsuarios**.

---

## Endpoints principais

### Usuários

| Método | Rota | Descrição |
|---|---|---|
| `POST` | `/api/usuarios/Auth` | Autenticar usuário |
| `GET` | `/api/Usuarios` | Lista todos os usuários |
| `POST` | `/api/Usuarios` | Cadastrar usuário |
| `GET` | `/api/Usuarios/{id}` | Buscar usuário por ID |
| `PUT` | `/api/Usuarios/{id}` | Atualizar usuário |
| `DELETE` | `/api/Usuarios/{id}` | Excluir usuário |

---

### Veículos

| Método | Rota | Descrição |
|---|---|---|
| `GET` | `/api/Veiculos` | Lista todos os veículos |
| `POST` | `/api/Veiculos` | Cadastra um novo veículo |
| `GET` | `/api/Veiculos/{id}` | Retorna um veículo por ID |
| `PUT` | `/api/Veiculos/{id}` | Atualiza um veículo |
| `DELETE` | `/api/Veiculos/{id}` | Remove um veículo |
| `POST` | `/api/Veiculos/{id}/usuarios` | Associa um usuário ao veículo |
| `DELETE` | `/api/Veiculos/{id}/usuarios/{usuarioId}` | Remove vínculo entre usuário e veículo |

---

### Consumos

| Método | Rota | Descrição |
|---|---|---|
| `GET` | `/api/Consumos` | Lista todos os consumos |
| `POST` | `/api/Consumos` | Cadastra um novo consumo |
| `GET` | `/api/Consumos/{id}` | Retorna um consumo por ID |  
| `PUT` | `/api/Consumos/{id}` | Atualiza um consumo |
| `DELETE` | `/api/Consumos/{id}` | Remove um consumo |

---

## Como executar o projeto localmente

### Pré-requisitos

Antes de iniciar, tenha instalado:

- **.NET SDK 8**
- **SQL Server** ou **LocalDB**
- **Visual Studio 2022**, VS Code ou outro editor compatível
- [Opcional] **Postman** ou **Insomnia**

### 1. Clonar o repositório

```bash
git clone https://github.com/codedbyallan/mf-apis-web-services-fuel-manager.git
```

### 2. Acessar a pasta do projeto

```bash
cd mf-apis-web-services-fuel-manager/mf-apis-web-services-fuel-manager
```

### 3. Restaurar dependências

```bash
dotnet restore
```

### 4. Aplicar as migrations

```bash
dotnet ef database update
```

### 5. Executar a aplicação

```bash
dotnet run
```

---

Este projeto demonstra experiência prática com:

- desenvolvimento de API REST com **ASP.NET Core**
- autenticação e autorização com **JWT**
- criptografia de senha com **BCrypt**
- Entity Framework Core
- modelagem relacional
- relacionamento muitos-para-muitos
- arquitetura baseada em controllers
- documentação com Swagger
- controle de acesso por perfil
- boas práticas de desenvolvimento back-end

Este é um projeto completo de API com autenticação, autorização e relacionamento entre entidades, representando uma aplicação real de back-end.

---

## Autor

**Allan Barbosa**  
GitHub: https://github.com/codedbyallan

Repositório:  
https://github.com/codedbyallan/mf-apis-web-services-fuel-manager

---

## Licença

Projeto disponibilizado para fins de estudo, prática e composição de portfólio.

