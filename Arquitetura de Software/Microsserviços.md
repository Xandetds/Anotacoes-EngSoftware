# Microsserviços

Microsserviço é um serviço separado, especializado em fazer somente uma função.

A ideia é pegar uma aplicação grande e dividir em partes menores (contextos), onde cada uma vira um microsserviço independente.

Esses microsserviços se comunicam entre si, geralmente através de APIs, e funcionam como se fossem mini aplicações isoladas.

Um exemplo simples:

se uma parte da aplicação consome muito mais recurso que o resto, a gente acaba pagando caro só por causa dela.

Separando essa parte em um microsserviço, é possível controlar melhor os custos e escalar só o que precisa.

---

<details>
<summary><strong>Complexidade aumentada</strong></summary>

### Complexidade aumentada

- **Exemplo prático de comunicação e autenticação**
    
    Imagina que existem dois serviços: um de **autenticação** (gera e valida tokens) e outro de **perfil** (dados do usuário).
    
    Ambos são públicos e têm IPs diferentes.
    
    Para acessar o perfil, é preciso passar pela autenticação todas as vezes — o problema é que precisamos garantir que essa requisição realmente veio de uma sessão válida.
    
    **Como resolver isso:**
    
    1. O token JWT é verificado pra ver se é válido e não expirou.
    2. É criado um hash SHA-256 da string `"logou"`.
    3. Esse hash é adicionado no perfil.
    4. Quando o serviço de perfil recebe uma requisição, ele compara o hash com o token pra confirmar se veio de uma autenticação real.
    
    Também tenho que estudar o funcionamento do AWS Secrets e do Git Secret, pra entender como guardar chaves e tokens de forma segura.
    
</details>

---

<details>
<summary><strong>DDD — Desenvolvimento Orientado a Domínio</strong></summary>

### DDD — Desenvolvimento Orientado a Domínio

- **Aplicação do DDD nos microsserviços**
    
    No DDD, cada microsserviço tem acesso **somente ao seu próprio banco e às suas tabelas**.
    
    Por exemplo:
    
    - O serviço de autenticação (`auth`) acessa apenas tabelas de autenticação.
    - O serviço de perfil (`profile`) acessa só as tabelas de perfil.
    
    No NestJS, pode ser customizado um decorator `@Auth`, que automatiza a verificação antes de executar uma ação, como um `get()`:
    
    ```jsx
    @Auth()
    get()
    ```
    
    Também dá pra passar parâmetros, por exemplo:
    
    ```jsx
    @Auth('admin')
    ```
    
    Isso deixa o código mais limpo e elegante, sem precisar ficar colocando `if (admin)` em todo lugar.
    
    Outro benefício é que **facilita a manutenção de versões** — dá pra rodar a versão antiga e a nova de uma API ao mesmo tempo, testar a nova e só depois substituir a antiga.
    
</details>

---

<details>
<summary><strong>Como surgiram os microsserviços</strong></summary>

### Como surgiram os microsserviços

- **Motivação e contexto histórico**
    
    Antigamente, nas aplicações monolíticas, era comum várias alterações serem feitas juntas num único commit.
    
    Se algo desse errado, tinha que fazer rollback do sistema inteiro.
    
    Com os microsserviços, isso muda.
    
    Cada parte tem seu ciclo próprio — se der problema, é só voltar a versão de um serviço específico, sem mexer no resto.
    
    Essa ideia também ajuda na **agilidade das entregas** e na **redução de custos** em cloud, porque os microsserviços são menores e mais focados.
    
    Cada contexto é isolado — os serviços **não compartilham estado** e nem precisam saber o que o outro está fazendo.
    
    Normalmente cada um roda em uma porta diferente (`3000`, `3001`, `3002`, etc).
    
</details>

---

<details>
<summary><strong>Redis e cache</strong></summary>

### Redis e cache

- **U**so de cache e quando evitar
    
    O Redis é muito usado pra guardar informações acessadas com frequência, como listas de produtos ou dados de autenticação.
    
    O cache melhora a performance e evita consultas repetitivas no banco.
    
    Mas é importante cuidar pra não exagerar — usar cache demais pode causar inconsistência ou até sobrecarregar a rede.
    
    Outro cuidado é evitar compartilhar dados entre microsserviços.
    
    Por exemplo, dois serviços editando a mesma tabela ao mesmo tempo podem causar conflito.
    
</details>

---

<details>
<summary><strong>Tamanho e granularidade dos microsserviços</strong></summary>

### Tamanho e granularidade dos microsserviços

Microsserviço pode ter diferentes tamanhos, dependendo do quanto ele precisa pra funcionar bem.

Isso é o que chamamos de **granularidade**.

- **Baixa granularidade:** poucos serviços, mas maiores.
- **Alta granularidade:** vários serviços pequenos.
- **Motivos pra granular microsserviços**
    1. **Coesão:**
        
        Seguir o DDD e dividir o sistema em contextos bem definidos.
        
        Exemplo: replicar a entidade de usuário em serviços diferentes, como “order captured” e “order fulfillment”.
        
    2. **Volatilidade:**
        
        Separar as partes que mudam mais.
        
        Assim, quando for atualizar, só precisa subir o serviço que realmente mudou.
        
    3. **Demanda por escala:**
        
        Nem tudo precisa escalar igual.
        
        Exemplo: o serviço de produtos é muito mais acessado que o de perfil.
        
    4. **Resiliência:**
        
        Se um serviço cair, o resto continua funcionando.
        
    5. **Segurança:**
        
        Cada serviço acessa só os dados necessários, o que reduz riscos.
        
</details>

---

<details>
<summary><strong>Quando juntar microsserviços</strong></summary>

### Quando juntar microsserviços

- Cenários onde separar demais atrapalha
    
    Às vezes, separar tudo demais pode causar inconsistência.
    
    Por exemplo: o serviço de carrinho consulta o de produtos e atualiza os itens.
    
    Se o produto muda logo depois, o carrinho fica desatualizado.
    
    Nessas situações, o melhor é juntar os dois serviços em uma única transação, pra garantir que os dados fiquem sincronizados.
    
</details>

---

<details>
<summary><strong>Reutilização de código e bibliotecas compartilhadas</strong></summary>

### Reutilização de código e bibliotecas compartilhadas

- Como lidar com código comum entre serviços
    
    Um dos motivos pra usar microsserviços é reutilizar partes do código, mas nem sempre compensa centralizar tudo.
    
    O comum é duplicar o que for necessário, pra manter os serviços realmente independentes.
    
    Em alguns casos, é útil ter um microsserviço só pra bibliotecas internas, onde ficam módulos como autenticação, logs, etc.
    
</details>

---

<details>
<summary><strong>Replicação de dados</strong></summary>

### Replicação de dados

- **Quando evitar e alternativas**
    
    Replicar dados entre serviços pode parecer prático, mas aumenta o custo de manutenção e pode gerar falhas de segurança.
    
- Alternativas
    - Armazenar apenas as chaves primárias e buscar os dados quando for necessário.
    - Usar cache inteligente (como Redis) pra dados temporários e consultas rápidas.
    
</details>

---

<details>
<summary><strong>Quando migrar pra microsserviços</strong></summary>

### Quando migrar pra microsserviços

- Momento ideal pra migrar
    
    Não vale a pena começar um sistema já usando microsserviços — no início o foco é velocidade e simplicidade.
    
    O ideal é começar monolítico e migrar quando fizer sentido.
    
    Quando migrar:
    
    - Quando o time crescer.
    - Quando quiser testar novas tecnologias.
    - Quando for necessário melhorar a robustez.
    - Quando precisar reduzir o tempo de entrega de novas versões.
    
</details>

---

<details>
<summary><strong>Micro Frontends</strong></summary>

### Micro Frontends

O frontend costuma ter **muitos arquivos e pouco código por arquivo**, diferente do backend que é o contrário.

O conceito de **micro frontends** segue o mesmo princípio dos microsserviços, só que aplicado na interface.

- **Quando dividir o frontend**
    
    Vale a pena dividir o frontend quando:
    
    - Precisamos deixar uma página mais leve e rápida.
    - Estamos aplicando DDD também na parte visual.
    - Temos times grandes e queremos evitar que um atrapalhe o outro.
    
    Cada micro frontend tem suas próprias dependências — por exemplo, todos podem precisar do Tailwind.
    
    Isso aumenta um pouco a duplicação, mas traz **independência de deploy** e mais controle de versões.
    
</details>

---
