# CRIAR BANCO DE DADOS

```
CREATE DATABASE universe_API_developpment;
```

# LISTAR BANCO DE DADOS

```
\l
```

# DELETAR BANCO DE DADOS

```
DROP DATABASE universe_api_developpment;
```

# CONECTAR A UM BANCO DE DADOS

```
\c universe_API_developpment;
```

# CRIAR BANCO TABELA

```
CREATE TABLE planets (
  name VARCHAR (50) NOT NULL,
  star_name VARCHAR (50) NOT NULL,
  code VARCHAR (20) UNIQUE NOT NULL,
  discovery_date DATE,
  satellites INT
);

```

# MOSTRAR DADOS DE UMA TABELA

```
\d planets
```

# ALTERAR TABELA (ADICIONAR COLUNA)

```
ALTER TABLE planets ADD COLUMN description text;
```

# ALTERAR TABELA (DELETAR COLUNA)

```
ALTER TABLE planets DROP COLUMN description;
```

# ALTERAR TABELA (ADICIONAR CONSTRAIN)

```
ALTER TABLE planets ADD CHECK (satellites > 1);
```

# ALTERAR TABELA (ADICIONAR VALOR DEFAULT)

```
ALTER TABLE planets ALTER COLUMN has_life SET DEFAULT true;
```

# ALTERAR TABELA (RENOMEAR COLUNA)

```
ALTER TABLE planets RENAME COLUMN sun_name TO star_name;
```

# INSERIR NA TABELA

```
INSERT INTO planets (name, star_name, code, discovery_date, satellites) VALUES ('x45', 'Rimuru', 'SDF54D8SX', '1961-06-16', 10);

INSERT INTO planets (satellites, star_name, code, discovery_date, name) VALUES (11, 'Rimuru', 'SDF54D8SX2', '1961-06-16', 'x46');
```

```
INSERT INTO planets VALUES ('x45', 'Rimuru', 'SDF54D8SX', '1961-06-16', 10);
```

# CONSULTANDO TODOS OS CAMPOS

```
SELECT * FROM planets;
```

# CHAVE PRIMARIA (ADICIONANDO)

```
ALTER TABLE planets ADD COLUMN ID SERIAL PRIMARY KEY;
```

SERIAL significa alto incrementada.

# CHAVE PRIMARIA (NA CRIAÇÃO DA TABELA)

```
CREATE TABLE planets (
  ID SERIAL PRIMARY KEY,
  name VARCHAR (50) NOT NULL,
  star_name VARCHAR (50) NOT NULL,
  code VARCHAR (20) UNIQUE NOT NULL,
  discovery_date DATE,
  satellites INT
);
```

# ATUALIZANDO UMA LINHA

```
UPDATE planets SET star_name = 'Tempest' WHERE ID = 2;
```

# DELETANDO UMA LINHA

```
DELETE FROM planets WHERE ID = 3;
```

# FOREIGN KEY (AO CRIAR A TABELA)

```
CREATE TABLE
foreignkey=# CREATE TABLE nave(
  id SERIAL PRIMARY KEY NOT NULL,
  nome VARCHAR(50) NOT NULL,
  capacidade int not null,
  astronautaId int,
  CONSTRAINT fkAstronauta FOREIGN KEY(astronautaId) REFERENCES astronauta(id)
);
```

```
  CONSTRAINT <nome_da_constraint> FOREIGN KEY(astronautaId) REFERENCES astronauta(id)
```
