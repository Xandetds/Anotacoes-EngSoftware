# Arquiteturas

<details>
<summary>Arquitetura em Camadas (Layered Architecture)</summary>

### Estrutura típica

    com.seuprojeto
    ├── entities
    │   ├── Aluno.java
    │   ├── Professor.java
    │   └── Pessoa.java
    ├── repositories
    │   ├── AlunoRepository.java
    │   ├── ProfessorRepository.java
    │   └── PessoaRepository.java
    ├── services
    │   ├── AlunoService.java
    │   ├── ProfessorService.java
    │   └── PessoaService.java
    └── resources
        ├── AlunoResource.java
        ├── ProfessorResource.java
        └── PessoaResource.java

### Conceito

- Divide o projeto por **tipo de função**, sendo elas Entity, Repository, Service e Controller.
- É o modelo mais usado em **APIs Spring Boot**.
- Ajuda na **organização horizontal**, pois todas as camadas são separadas globalmente.

### Vantagens

- Fácil de entender e aprender.
- Facilita o **reuso** de serviços e repositórios.
- Ideal para **projetos pequenos** ou atividades acadêmicas.

### Desvantagens

- Em projetos grandes, as pastas ficam muito cheias de arquivos.
- As partes de um mesmo módulo (ex: “Aluno”) ficam **espalhadas em várias pastas**, dificultando a navegação.

</details>

--------------------------------------------------------------------

<details>
<summary>Arquitetura por Domínio / por Feature (Domain-Driven / Feature-Based)</summary>

### Estrutura típica

    com.seuprojeto
    ├── aluno
    │   ├── Aluno.java
    │   ├── AlunoRepository.java
    │   ├── AlunoService.java
    │   └── AlunoResource.java
    ├── professor
    │   ├── Professor.java
    │   ├── ProfessorRepository.java
    │   ├── ProfessorService.java
    │   └── ProfessorResource.java
    └── pessoa
        ├── Pessoa.java
        ├── PessoaRepository.java
        ├── PessoaService.java
        └── PessoaResource.java

### Conceito

- Organiza o código por **funcionalidade (feature)** e não por camada.
- Cada módulo contém tudo o que precisa dentro da própria pasta.
- É o estilo usado em **sistemas maiores** ou com **microsserviços**.

### Vantagens

- Facilita a **manutenção**, pois cada módulo está isolado.
- Evita a navegação por várias pastas diferentes.
- Escalável para **grandes equipes** ou **projetos corporativos**.

### Desvantagens

- Exige **disciplina de organização** para manter o padrão entre os módulos.
- Pode gerar **duplicação de código** se várias features precisarem das mesmas classes utilitárias.

</details>
