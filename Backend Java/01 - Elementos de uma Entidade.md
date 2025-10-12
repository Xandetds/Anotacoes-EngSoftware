# Elementos de uma Entidade (JAVA / JPA)

<details>
<summary>Construtores</summary>

Servem para criar objetos.

O construtor é chamado sempre que se usa `new NomeDaClasse()`.

Construtor vazio (padrão):

    public Pessoa() {}

- É obrigatório em entidades JPA.
- O JPA usa reflexão para criar objetos automaticamente quando busca do banco.
- Sem ele, ocorre erro: "No default constructor for entity"

Construtor com parâmetros:

    public Pessoa(String cpf, String nome) {
        this.cpf = cpf;
        this.nome = nome;
    }

Facilita quando tu quer criar o objeto manualmente.

Exemplo de uso:

    Pessoa p = new Pessoa("12345678900", "Maria");

</details>

--------------------------------------------------------------------

<details>
<summary>equals()</summary>

Usado para comparar objetos.

Por padrão, o Java só compara se estão na mesma posição de memória.
Com equals(), tu define quando dois objetos são iguais pela lógica da aplicação.

Exemplo:

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Pessoa)) return false;
        Pessoa pessoa = (Pessoa) o;
        return Objects.equals(cpf, pessoa.cpf);
    }

Explicação:
- this == o → verifica se é o mesmo objeto.
- instanceof → verifica se é do mesmo tipo.
- Objects.equals(...) → compara o valor do campo.

Duas pessoas com o mesmo CPF são consideradas iguais.

</details>

--------------------------------------------------------------------

<details>
<summary>hashCode()</summary>

Gera um número único (hash) com base nos atributos do objeto.
É usado por coleções como HashSet, HashMap, HashTable.

Exemplo:

    @Override
    public int hashCode() {
        return Objects.hash(cpf);
    }

Regra:
Se dois objetos são iguais segundo o equals(), eles devem ter o mesmo hashCode().

Assim o Java encontra o objeto certo dentro das coleções.

Exemplo prático:

Imagina que tu tem uma lista de pessoas cadastradas no sistema e quer garantir que não existam CPFs duplicados.
Tu poderia usar uma estrutura chamada HashSet, que não permite elementos repetidos.
O HashSet usa o hashCode() e o equals() internamente pra decidir se um objeto já existe no conjunto.

    Set<Pessoa> pessoas = new HashSet<>();

    Pessoa p1 = new Pessoa("12345678900", "Maria");
    Pessoa p2 = new Pessoa("12345678900", "Maria Oliveira");

    pessoas.add(p1);
    pessoas.add(p2);

    System.out.println(pessoas.size()); // Resultado: 1

Por que deu 1 e não 2?
Porque o HashSet chamou o hashCode() e o equals() das duas pessoas,
viu que o CPF é igual e entendeu que é a mesma pessoa, então não adicionou duplicado.

</details>

--------------------------------------------------------------------

<details>
<summary>Getters e Setters</summary>

São os acessos controlados aos atributos privados.
Servem pra ler e alterar valores de fora da classe.

Exemplo:

    public String getNome() { return nome; }
    public void setNome(String nome) { this.nome = nome; }

Explicação:
- getNome() → retorna o valor.
- setNome() → altera o valor.
- Usamos getters e setters porque os atributos são private.

</details>

--------------------------------------------------------------------

<details>
<summary>toString()</summary>

Converte o objeto em texto legível (String).
Usado para depuração, logs e exibição no console.

Exemplo:

    @Override
    public String toString() {
        return "Pessoa{" +
                "cpf='" + cpf + '\'' +
                ", nome='" + nome + '\'' +
                '}';
    }

Como fica:

        Sem toString():
            br.com.backend.entity.Pessoa@6e8dacdf

        Com toString():
            Pessoa{cpf='12345678900', nome='Maria'}

</details>

--------------------------------------------------------------------

<details>
<summary>Resumo</summary>

| Elemento              | Função                                          |
|-----------------------|--------------------------------------------------|
| Construtor vazio      | Permite ao JPA criar objetos automaticamente     |
| Construtor com params | Facilita criação manual                          |
| equals()              | Define quando dois objetos são iguais            |
| hashCode()            | Gera número único para coleções                  |
| getters/setters       | Acesso seguro aos atributos                      |
| toString()            | Exibição legível do objeto                       |

</details>
