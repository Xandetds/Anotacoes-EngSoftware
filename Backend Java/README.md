# Anotações — Backend com Spring Boot

Este diretório reúne anotações, resumos e exemplos práticos relacionados ao **desenvolvimento backend em Java com Spring Boot**.  
Aqui estão os principais conceitos aprendidos e implementados durante o projeto [backend satc](https://github.com/Xandetds/backend_satc), abordando desde o mapeamento de entidades até a criação de APIs REST completas.

## Conteúdos abordados

- **Entity e JPA** — mapeamento objeto-relacional, herança e relacionamentos entre tabelas.
- **DTOs e validação** — transporte de dados entre camadas e verificação de integridade.
- **Camadas da aplicação** — Resource, Service e Repository.
- **MapStruct** — conversão automática entre DTO e Entity.
- **Boas práticas de arquitetura** — isolamento de responsabilidades e estrutura em camadas.

---

## Estrutura dos arquivos

| Arquivo | Descrição |
|----------|------------|
| `Elementos de uma Entidade (JAVA / JPA).md` | Explicações sobre os elementos e funções frequentemente usadas em uma entidade. |
| `Anotações do Spring e JPA.md` | Explica sobre as anotações normalmente usadas, sejam elas derivadas do Spring ou do JPA. |
| `Arquiteturas .md` | Mostra sobre as duas arquiteturas Spring aprendidas nas aulas da matéria de backend da UNISATC. |
| `Entidades aprofundadas.md` | Explicações sobre entidades, focando mais em herança e relacionamentos. |
| `DTO (Data Transfer Object).md` | Conceito, uso e validação de DTOs. |
| `mapstruct.md` | Guia completo do MapStruct e exemplos práticos. |
| `implementacao_pratica.md` | Detalhamento do projeto `backend_satc` e seu fluxo entre camadas. |

---

## Projeto de referência

As anotações foram feitas com base no projeto real:  
🔗 [**backend_satc** — GitHub Repository](https://github.com/Xandetds/backend_satc)

O projeto aplica na prática todos os conceitos descritos aqui, incluindo herança entre entidades, validações com Bean Validation e conversão automática via MapStruct.

