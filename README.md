# Projeto: Otimização e Manipulação de Dados em Banco de Dados

## Descrição do Projeto
Este projeto tem como objetivo otimizar o desempenho de consultas SQL em um banco de dados relacional, por meio da criação de índices estratégicos com base em perguntas de negócio. Além disso, o projeto inclui a criação de procedures para manipulação de dados (inserção, atualização e remoção), controladas por uma variável de decisão. O projeto foi dividido em duas partes:

- **Parte 1:** Criação de índices e consultas otimizadas para um cenário de empresa (Company).
- **Parte 2:** Criação de procedures com lógica condicional para um cenário de E-Commerce.

---

## Parte 1 – Criação de Índices e Consultas

### Estrutura Utilizada
- Tabela: `departamento`
- Tabela: `empregado`

### Perguntas e Consultas
1. **Qual o departamento com maior número de pessoas?**
2. **Quais são os departamentos por cidade?**
3. **Relação de empregados por departamento**

### Índices Criados e Justificativas

#### 1. Índice: `idx_empregado_departamento`
```sql
CREATE INDEX idx_empregado_departamento ON empregado(departamento_id);
```
- **Motivo:** Usado para acelerar JOINs e GROUP BY que envolvem a coluna `departamento_id`, essencial para contagem e relacionamentos entre tabelas.

#### 2. Índice: `idx_departamento_cidade`
```sql
CREATE INDEX idx_departamento_cidade ON departamento(cidade);
```
- **Motivo:** Otimiza filtros e ordenações baseadas na coluna `cidade`, frequentemente usada em relatórios geográficos.

### Tipo de Índice
- Foi utilizado o índice padrão `BTREE` do MySQL, ideal para buscas ordenadas, filtros e junções.

---

## Parte 2 – Procedures para Manipulação de Dados

### Estrutura Utilizada
- Tabela: `produto` (id, nome, preco)

### Procedure Criada
```sql
CREATE PROCEDURE sp_gerenciar_produto (
    IN p_opcao INT,
    IN p_id INT,
    IN p_nome VARCHAR(100),
    IN p_preco DECIMAL(10,2)
)
```

### Lógica de Controle
- `p_opcao = 1` → Inserção de novo produto
- `p_opcao = 2` → Atualização de produto existente
- `p_opcao = 3` → Remoção de produto
- Qualquer outro valor → Retorna mensagem de "opção inválida"

### Exemplo de Chamada
```sql
CALL sp_gerenciar_produto(1, 101, 'Teclado Gamer', 199.99); -- Inserção
CALL sp_gerenciar_produto(2, 101, 'Teclado RGB', 179.99);    -- Atualização
CALL sp_gerenciar_produto(3, 101, '', 0.00);                 -- Remoção
```

---

## Considerações Finais
- Os índices foram criados com foco na performance das consultas exigidas.
- A procedure facilita a manipulação segura e controlada de dados por meio de uma única interface.
- O projeto serve como base para aplicações corporativas que demandam performance e controle transacional.

---

## Autor
Desenvolvido por [OrlandoSD] – em bancos de dados SQL Server e MySQL.


