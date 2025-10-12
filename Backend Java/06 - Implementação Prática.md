# Implementação Prática

Visão geral

O projeto [Backend Satc](https://github.com/Xandetds/backend_satc) do meu github
 é uma aplicação **Spring Boot** integrada ao **PostgreSQL**, construída com arquitetura em **camadas** (Entity, DTO, Mapper, Repository, Service e Resource).

O sistema simula uma **gestão de chamados técnicos**, onde **clientes** registram problemas e **técnicos** são designados para atendê-los.

O foco da implementação é aplicar:
- Mapeamento objeto-relacional (JPA / Hibernate)
- Herança entre entidades
- Validação de dados com Bean Validation
- Conversão DTO ↔ Entity com MapStruct
- Regras de negócio na camada Service
- Exposição de endpoints REST

</details>

--------------------------------------------------------------------

<details>
<summary>Estrutura geral</summary>

    src/
     ├── entity/        → entidades (mapeamento do banco)
     ├── dto/           → objetos de transporte com validação
     ├── mapper/        → conversores entre DTO ↔ Entity (MapStruct)
     ├── repository/    → interfaces JPA (acesso ao banco)
     ├── service/       → regras de negócio
     └── resource/      → controladores REST

</details>

--------------------------------------------------------------------

<details>
<summary>Entities (Camada de Dados)</summary>

As **entidades** representam as tabelas no banco.

A modelagem usa **herança com JOINED**, o que cria uma tabela para `Pessoa`, `Cliente` e `Técnico`, mantendo o mesmo `id` compartilhado.

- `Pessoa` → classe base com `id`, `nome`, `cpf`.
- `Cliente` → herda de Pessoa e adiciona `email`, `endereço`.
- `Técnico` → herda de Pessoa e adiciona `especialidade`, `chamadosAtendidos`.
- `Chamado` → possui `título`, `descrição`, `datas`, `status`, `cliente` e `técnico`.

**Relações:**
- `@ManyToOne` entre `Chamado` e `Cliente` (um cliente pode ter vários chamados).
- `@ManyToOne` entre `Chamado` e `Técnico` (um técnico pode atender vários chamados).

O `@Enumerated(EnumType.STRING)` foi usado para mapear o **enum Status** (`ABERTO`, `EM_ANDAMENTO`, `FECHADO`) como texto no banco.

</details>

--------------------------------------------------------------------

<details>
<summary>DTOs (Camada de Transporte)</summary>

Os **DTOs** servem para transferir dados entre o cliente (API) e o backend, com **validações automáticas** via `Bean Validation`.

Exemplo:
- `@NotBlank` e `@Size` em `ClienteDTO` garantem o formato correto.
- `@Email` valida endereços de e-mail.
- `@Valid` é usado nos controllers para ativar a validação.

Essa abordagem evita expor as entidades do banco e garante que só dados válidos cheguem à lógica de negócio.

</details>

--------------------------------------------------------------------

<details>
<summary>MapStruct (Conversão DTO ↔ Entity)</summary>

Em vez de converter manualmente DTOs e Entities, o projeto usa **MapStruct**.

O framework gera o código de conversão durante a compilação.

    @Mapper(componentModel = "spring")
    public interface ClienteMapper {
        Cliente toEntity(ClienteDTO dto);
        ClienteDTO toDTO(Cliente entity);
    }

Isso elimina a necessidade de `new Cliente()` e de setters manuais em cada conversão, deixando o código mais limpo, rápido e seguro.

</details>

--------------------------------------------------------------------

<details>
<summary>Repository (Camada de Persistência)</summary>

Cada entidade principal possui seu repositório:

- `ChamadoRepository`
- `ClienteRepository`
- `TecnicoRepository`

Todos estendem `JpaRepository`, o que dá acesso imediato a operações CRUD (`save`, `findAll`, `findById`, `deleteById`, etc.), sem precisar escrever SQL manualmente.

Essa camada é responsável apenas por **consultar e salvar dados** — não contém lógica de negócio.

</details>

--------------------------------------------------------------------

<details>
<summary>Service (Camada de Negócio)</summary>

A **lógica de negócio** fica centralizada na camada Service.

No caso do `ChamadoService`, as principais regras implementadas são:

- Ao criar um chamado:
    - Define automaticamente `status = ABERTO`
    - Define `dataAbertura = LocalDateTime.now()`
- Ao fechar um chamado:
    - Atualiza `status = FECHADO`
    - Registra `dataFechamento = LocalDateTime.now()`

Essa camada também é responsável por buscar dados, aplicar validações lógicas e retornar mensagens de erro apropriadas (ex: “Chamado não encontrado”).

</details>

--------------------------------------------------------------------

<details>
<summary>Resource (Camada de Controle / API REST)</summary>

A camada **Resource** (ou Controller) expõe os endpoints HTTP.

Exemplo: `ChamadoResource`.

Endpoints criados:
- `POST /chamados` → cria um novo chamado
- `GET /chamados` → lista todos os chamados
- `PUT /chamados/{id}/fechar` → fecha um chamado existente

O controller recebe objetos DTO anotados com `@Valid`, passa para o service e retorna a resposta.

O Spring Boot, junto com o `springdoc-openapi`, gera automaticamente a **interface Swagger** para teste:
> http://localhost:8080/swagger-ui.html

</details>

--------------------------------------------------------------------

<details>
<summary>Fluxo geral de funcionamento</summary>

1. **Cliente → API:**  
   Envia JSON com os dados do chamado (DTO validado).

2. **Controller → Service:**  
   O controller chama o `ChamadoService`, que aplica as regras de negócio.

3. **Service → Repository:**  
   O service usa o `ChamadoRepository` para persistir ou buscar dados.

4. **Repository → Banco:**  
   O Hibernate traduz automaticamente os métodos do repository em SQL.

5. **Banco → Service → Controller → Cliente:**  
   O resultado (entidade ou DTO) é retornado ao cliente como JSON.

</details>

--------------------------------------------------------------------

<details>
<summary>Banco de dados e integração</summary>

Banco usado: **PostgreSQL**, conectado via `application.properties`:

    spring.datasource.url=jdbc:postgresql://localhost:5432/backend_satc
    spring.datasource.username=postgres
    spring.datasource.password=123456
    spring.jpa.hibernate.ddl-auto=update

- `ddl-auto=update` faz o Hibernate criar e atualizar as tabelas automaticamente.
- Após executar o projeto (`Run` no IntelliJ), o Hibernate gera:
    - `pessoa`
    - `cliente`
    - `tecnico`
    - `chamado`

Cada execução sincroniza automaticamente o modelo com o banco.

</details>

--------------------------------------------------------------------

<details>
<summary>Conclusão</summary>

O projeto **backend-satc** me deu novos conhecimentos sobre muitas partes do desenvolvimento backend moderno:

- Modelagem relacional com herança JPA  
- Validação de entrada com Bean Validation  
- Separação em camadas (controller, service, repository)  
- Conversão automática de objetos com MapStruct  
- Documentação automática via Swagger UI  

O código segue boas práticas de baixo acoplamento e alta coesão,  
servindo como base sólida para sistemas corporativos REST em Spring Boot.

</details>
