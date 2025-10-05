# Escalabilidade

A **escalabilidade** é a capacidade de um sistema lidar com um aumento de carga (usuários, requisições ou dados) sem perder desempenho.

Ela permite que a aplicação cresça de forma sustentável, atendendo mais usuários sem precisar ser reescrita do zero.

### Principais formas de escalar um sistema

- Escalabilidade Vertical (Scale Up)
    
    Consiste em **melhorar o hardware existente**, como adicionar mais CPU, memória RAM ou armazenamento ao servidor.
    
    É mais simples, mas tem um limite físico e costuma ser mais cara.
    
    **Exemplo:** aumentar a memória do servidor de 4 GB para 32 GB.
    

- Escalabilidade Horizontal (Scale Out)
    
    Envolve **adicionar novos servidores ou instâncias** para dividir a carga entre eles.
    
    É a base dos sistemas distribuídos modernos e permite crescimento praticamente ilimitado.
    
    **Exemplo:** em vez de um servidor processar tudo, usar cinco servidores balanceados.
    

---

### Gargalos de desempenho

Um **gargalo** é o ponto do sistema que limita o desempenho geral.

Pode ocorrer no banco de dados, na CPU, na rede ou em um serviço externo.

**Exemplo prático:**

Uma API que processa pedidos, mas demora muito porque cada requisição faz cálculos complexos e acessa o banco várias vezes.

Mesmo com vários usuários simultâneos, o desempenho fica travado por esse ponto.

---

### Experimento Prático – API de E-commerce com Gargalo e Cache Redis

### **Contexto do experimento**

Nesta atividade, foi desenvolvida uma **API REST em** Typescript com Nest simulando um sistema de e-commerce.

Repositório do código utilizado: [Arquitetura de software](https://github.com/Xandetds/Arquitetura-de-software)
 

O objetivo foi compreender como **otimizar o desempenho e a escalabilidade** identificando gargalos e implementando **cache com Redis**.

As etapas principais foram:

1. Testar a API com gargalo (sem cache);
2. Implementar cache com Redis;
3. Repetir os testes de carga e comparar os resultados.

---

### **Cenário inicial – com gargalo**

Foi adicionado um **atraso artificial** (`setTimeout`) no endpoint de busca de produtos, simulando uma operação demorada de banco de dados.

**Endpoint:**

```jsx
app.get("/products", async (req, res) => {
  setTimeout(() => {
    res.json(products);  }, 3000); // atraso de 3 segundos});
```

Esse atraso foi proposital para simular uma API sobrecarregada ou sem otimizações.

**Teste de carga com Artillery:**

```yaml
config:
  target: "http://localhost:3000"   
  phases:
    - duration: 60 
      arrivalRate: 20
scenarios:
  - flow:
    - get:
        url: "/products"
```

 **Resultados (sem cache):**

- Tempo médio: ~5,1 ms
- Percentil 95 (p95): ~34 ms
- Percentil 99 (p99): ~53 ms
- Requisições totais: 1200
- Erros: 0

 As requisições foram processadas diretamente pelo servidor, sem cache.

O tempo médio foi alto, e a API apresentou gargalos sob carga.

---

### **Implementação do Cache com Redis**

Para otimizar, foi adicionado **Redis** (banco em memória) usando o container Docker:

```bash
docker run -d --name redis-cache -p 6379:6379 redis
```

**Exemplo de código com cache:**

```jsx
app.get("/products", async (req, res) => {
  const cacheData = await redisClient.get("products");  if (cacheData) {
    return res.json(JSON.parse(cacheData)); // retorna do cache  }
  const data = products; // simula leitura do "banco"  await redisClient.set("products", JSON.stringify(data), "EX", 30); // cache por 30s  res.json(data);});
```

Dessa forma, a primeira requisição busca os dados normalmente, e as próximas vêm direto da memória, sem processar tudo de novo.

---

### **Cenário otimizado – com cache Redis**

**Resultados (com cache):**
- Tempo médio: ~1 ms

- Percentil 95 (p95): ~2 ms

- Percentil 99 (p99): ~5 ms

- Requisições totais: 1200

- Erros: 0

As requisições subsequentes foram respondidas quase instantaneamente, mostrando o impacto real do cache em sistemas escaláveis.

---

### **Comparativo dos resultados**

| Métrica | Sem Cache | Com Cache |
| --- | --- | --- |
| Tempo médio (mean) | ~5,1 ms | ~1 ms |
| p95 | ~34 ms | ~2 ms |
| p99 | ~53 ms | ~5 ms |
| Erros | 0 | 0 |

**Conclusão do teste:**

A aplicação se tornou mais escalável e responsiva.

Com o Redis, as requisições subsequentes são atendidas diretamente da memória, reduzindo a carga no servidor e eliminando o gargalo.

---

### Conclusões e aprendizados

- **Escalabilidade** é essencial para manter o desempenho à medida que a aplicação cresce.
- **Gargalos** precisam ser identificados e tratados, pois eles definem o limite de performance.
- O **cache Redis** é uma solução simples e poderosa para aliviar o servidor e melhorar o tempo de resposta.
- **Docker** facilita a configuração do ambiente e o isolamento dos serviços.
- Ferramentas como **Artillery** ajudam a medir o impacto real das otimizações.
