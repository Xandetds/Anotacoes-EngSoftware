# Anotações do Spring e JPA

<details>
<summary>JPA (Java Persistence API)</summary>

Usadas para mapear as classes Java às tabelas do banco de dados.

- `@Entity` → Diz que a classe representa uma tabela no banco.
- `@Id` → Marca o atributo que é a chave primária (identificador único).
- `@GeneratedValue(strategy = GenerationType.IDENTITY)` → Gera o ID automaticamente (auto-increment).
- `@Column`(nullable = false, length = 50) → Configura detalhes da coluna (se pode ser nula, tamanho etc).
- `@Table(name = "tb_pessoa")` → Define manualmente o nome da tabela (opcional).
- `@OneToMany(mappedBy = "pessoa")` → Um para muitos — ex: uma pessoa → vários endereços.
- `@ManyToOne` → Muitos para um — ex: vários endereços → uma pessoa.
- `@OneToOne` → Um para um — ex: pessoa ↔ CPF.
- `@ManyToMany` → Muitos para muitos — ex: alunos ↔ disciplinas.
- `@JoinColumn(name = "pessoa_id")` → Cria a coluna de ligação entre as tabelas.
- `@JoinTable(...)` → Cria uma tabela intermediária pra relacionamentos N:N.

Exemplo prático de uso em uma entidade:

    @Entity
    @Table(name = "tb_pessoa")
    public class Pessoa {

        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;

        @Column(nullable = false, length = 100)
        private String nome;

        @OneToMany(mappedBy = "pessoa")
        private List<Endereco> enderecos;

        // getters e setters
    }

</details>

--------------------------------------------------------------------

<details>
<summary>Spring Boot</summary>

- `@Component` → Marca uma classe gerenciada pelo Spring (pode ser injetada em outros lugares).
- `@Service` → Camada de **regras de negócio** (lógica da aplicação).
- `@Repository` → Camada de **acesso ao banco** (DAO).  
  O Spring trata automaticamente exceções de banco.

- `@RestController` → Junta @Controller + @ResponseBody.  
  Diz que a classe expõe **endpoints REST** (retorna JSON).

- `@RequestMapping("/pessoas")` → Define o caminho base do endpoint.
- `@GetMapping` / `@PostMapping` / `@PutMapping` / `@DeleteMapping` → Especificam o método HTTP usado.
- `@PathVariable` → Pega uma variável da URL (/pessoas/{id} → id).
- `@RequestBody` → Converte o corpo JSON da requisição em um objeto Java.
- `@Autowired` → Faz a **injeção de dependência automática**, ligando camadas.  
  Exemplo:

        @Autowired
        private PessoaService service;

- `@SpringBootApplicatio` → Marca a classe principal (com o método main).
- `@Configuration` → Define configurações do Spring.
- `@Bean` → Cria manualmente um componente gerenciado pelo Spring.

Exemplo de Controller:

    @RestController
    @RequestMapping("/pessoas")
    public class PessoaResource {

        @Autowired
        private PessoaService service;

        @GetMapping
        public List<Pessoa> listarPessoas() {
            return service.listarTodas();
        }

        @PostMapping
        public Pessoa salvar(@RequestBody Pessoa pessoa) {
            return service.salvar(pessoa);
        }
    }

</details>

--------------------------------------------------------------------

<details>
<summary>Resumo</summary>

| Categoria | Anotações principais | Função |
|------------|----------------------|---------|
| JPA | `@Entity`, `@Id`, `@Column` | Mapeiam a tabela e colunas |
| Relacionamentos | `@OneToMany`, `@ManyToOne`, `@JoinTable` | Ligam tabelas |
| Spring Boot | `@Service`, `@Repository`, `@RestController` | Definem camadas da aplicação |
| HTTP | `@GetMapping`, `@PostMapping`, `@RequestBody` | Mapeiam endpoints REST |
| Injeção de dependência | `@Autowired`, `@Bean` | Fazem o Spring conectar os componentes |

</details>
