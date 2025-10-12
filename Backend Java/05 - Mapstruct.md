# MapStruct

<details>
<summary>O que é</summary>

O **MapStruct** é uma biblioteca Java que **gera automaticamente o código de conversão entre objetos**.  
É muito usada para converter entre **DTOs e Entities**, evitando repetição de código com getters e setters.

O processamento ocorre **em tempo de compilação**, o que traz vantagens como:
- Alto desempenho (sem reflexão);
- Menos erros em tempo de execução;
- Verificação estática dos mapeamentos no build.

</details>

--------------------------------------------------------------------

<details>
<summary>Exemplo básico</summary>

    package br.com.backend.Backend_satc.arquitetura1.mapper;

    import br.com.backend.Backend_satc.arquitetura1.dto.ClienteDTO;
    import br.com.backend.Backend_satc.arquitetura1.entity.Cliente;
    import org.mapstruct.Mapper;

    @Mapper(componentModel = "spring")
    public interface ClienteMapper {
        Cliente toEntity(ClienteDTO dto);
        ClienteDTO toDTO(Cliente entity);
    }

O **MapStruct** gera automaticamente uma implementação dessa interface  
durante a compilação, sem que seja necessário escrever o código manualmente.

</details>

--------------------------------------------------------------------

<details>
<summary>Mapeamentos personalizados</summary>

    @Mapper(componentModel = "spring")
    public interface UsuarioMapper {

        @Mapping(source = "nomeCompleto", target = "nome")
        @Mapping(target = "dataCadastro", ignore = true)
        @Mapping(target = "status", constant = "ATIVO")
        Usuario toEntity(UsuarioDTO dto);
    }

**Explicação:**
- `source` → nome do campo de origem.  
- `target` → nome do campo de destino.  
- `ignore = true` → ignora o campo.  
- `constant` → define um valor fixo.

</details>

--------------------------------------------------------------------

<details>
<summary>Principais anotações do MapStruct</summary>

| Anotação | Função |
|-----------|--------|
| `@Mapper(componentModel = "spring")` | Define o mapper e permite injeção via @Autowired. |
| `@Mapping(source, target)` | Mapeia campos com nomes diferentes. |
| `@Mapping(target, ignore = true)` | Ignora campos específicos. |
| `@Mapping(target, constant = "valor")` | Define um valor constante. |
| `@InheritInverseConfiguration` | Gera o mapeamento inverso automaticamente. |
| `@MappingTarget` | Atualiza um objeto existente (usado para update). |

</details>
