# DTO (Data Transfer Object)

<details>
<summary>Conceito geral</summary>

Um **DTO (Data Transfer Object)** é um objeto simples usado para **transportar dados** entre as camadas da aplicação.  
Diferente da Entity, o DTO **não representa uma tabela** e **não possui lógica de negócio**.

É comum usar DTOs para:
- Receber dados da requisição (POST, PUT);
- Retornar dados para o cliente (GET);
- Proteger a aplicação contra exposição direta das entidades.

</details>

--------------------------------------------------------------------

<details>
<summary>Exemplo de DTO com validações</summary>

    package br.com.backend.Backend_satc.arquitetura1.dto;

    import jakarta.validation.constraints.Email;
    import jakarta.validation.constraints.NotBlank;
    import jakarta.validation.constraints.Size;

    public class ClienteDTO {

        @NotBlank(message = "O nome é obrigatório")
        @Size(min = 3, max = 100, message = "O nome deve ter entre 3 e 100 caracteres")
        private String nome;

        @NotBlank(message = "O CPF é obrigatório")
        @Size(min = 11, max = 11, message = "O CPF deve ter 11 dígitos")
        private String cpf;

        @NotBlank(message = "O e-mail é obrigatório")
        @Email(message = "E-mail inválido")
        private String email;

        @NotBlank(message = "O endereço é obrigatório")
        private String endereco;

        public ClienteDTO() {}
    }

Explicação:
- As validações são feitas com anotações do **Jakarta Bean Validation**.
- Essas regras são aplicadas automaticamente quando o DTO é usado em um controller com `@Valid`.

</details>

--------------------------------------------------------------------

<details>
<summary>Validação de dados (Bean Validation)</summary>

O Spring valida automaticamente os campos de um DTO quando ele é recebido por um endpoint com `@Valid`.

Exemplo:

    @PostMapping("/clientes")
    public ResponseEntity<Cliente> criarCliente(@Valid @RequestBody ClienteDTO dto) {
        Cliente cliente = clienteMapper.toEntity(dto);
        Cliente salvo = clienteService.salvar(cliente);
        return ResponseEntity.ok(salvo);
    }

O `@Valid` garante que o Spring valide o DTO **antes de chamar o método**.  
Se algum campo violar as regras (ex: CPF vazio, e-mail inválido),  
a requisição é automaticamente rejeitada com o código **400 Bad Request**.

</details>

--------------------------------------------------------------------

<details>
<summary>Tipos de validação mais usados</summary>

| Anotação | Função |
|-----------|--------|
| `@NotNull` | O campo não pode ser nulo. |
| `@NotEmpty` | O campo não pode ser nulo nem vazio. |
| `@NotBlank` | O campo não pode ser vazio nem conter apenas espaços. |
| `@Size(min, max)` | Restringe o tamanho do texto. |
| `@Email` | Verifica se o formato do e-mail é válido. |
| `@Min`, `@Max`, `@Positive` | Valida valores numéricos. |
| `@Past`, `@Future` | Valida datas. |

</details>
