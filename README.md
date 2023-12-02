# InovaWeek
Uma base de modelo funcional projetado no Prisma, para sustentar uma API que faz pulls e requests de várias informações em um banco de dados relacional. Criado pela turma CC4Mb da Universidade Vila Velha, cursando o curso de Ciência da Computação. Os integrantes do grupo são:
- Arthur Buback
- Caroline Andrade Silva
- Marne Silva Matos de Amorim
- Pedro Henrique Lucas Belo

O professor responsável por ministrar a matéria e proporcionar a atividade de criação do projeto:
- Otávio Lube

  
# Passos para iniciar o projeto Node e Typescript

 ## Iniciando o node
 npm init -y
 ## Instalar o typescript
 npm install typescript --save-dev
 ## Inicializar e Configurar o Typescript
 npx tsc --init
## Configurar o config.ts
 Modelo recomendado para as configurações:
 
 {
   "compilerOptions": {
    "target": "es2016",
    "module": "commonjs",
    "rootDir": "./src",
    "outDir": "./dist",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true
  }
}

# Passos para iniciar o projeto Prisma e o Prisma Client

  ## Instalar o typescript node
  npm install typescript ts-node @types/node --save-dev
  ## Instalar o Prisma CLI
  npm install prisma --save-dev
  ## Inicializar o Prisma
  npx prisma init --datasource-provider sqlite

## Gere um Prisma Client baseado no modelo incrementado no prisma.scheme
npx prisma generate
## Implemente a importação do Prisma Client no arquivo que você deseja utilizá-lo e teste
Crie um arquivo typescript no seu projeto, seja ele dentro de uma outra pasta chamada src, com o nome de teste.ts ou qualquer outro nome. Após ter feito isso,
adicione este código ao início do arquivo:

import { PrismaClient } from '@prisma/client/edge'
const prisma = new PrismaClient()

Caso o seu editor de texto apresente algum erro na linha de código da importação do Prisma Client, significa que você pulou alguma parte das etapas, e o Prisma não foi instalado corretamente. Revise as etapas a procura de alguma que tenha passado despercebido, e caso não encontre, tente também pesquisar o seu erro na internet ou recomeçar um novo projeto.

# Como utilizar queries e conectar o banco de dados

## Use o Prisma Migrate para criar o banco de dados
npx prisma migrate dev --name init

# Instalar o Express e o EJS:
Baixar o express com os comandos:

npm i express

npm i --save-dev @types/express

## Baixar o Ejs para visualizar na porta 3000

npm install ejs

# Explicações sobre o modelo lógico

## Modelo Aluno
Cada aluno é identificado com a sua matrícula, em todos os campos que forem relacionados. Um aluno também sempre participará de um grupo, e na sua listagem de atributos, possui
o id do grupo em que ele participa assim como um objeto grupo para visualização dos atributos do grupo. Um aluno também possui um nome em tipo String, e pode fazer várias ou nenhuma avaliação de projetos do Inova. E por fim, um aluno pode ser líder de um grupo, representando assim uma varíavel booleana para representar se ele é líder ou não.

## Modelo Grupo
Cada grupo é identificado pelo seu id, em todos os campos que forem relacionados. Cada grupo tem uma lista de alunos integrantes, que pode guardar vários ou nenhum aluno. Finalmente, cada grupo tem o seu projeto associado, sendo representado por um objeto do tipo Projeto e o id do projeto que ele tem como projeto do grupo. É importante notar que a relação grupo-projeto é de 1:1, ou seja, um grupo só pode ter um projeto associado, ao mesmo tempo que um projeto só pode ter um grupo associado.

## Modelo Projeto
Cada projeto é identificado pelo seu id, em todos os campos que forem relacionados, e seu id é o número do stand que eles foram selecionados para apresentar. Cada projeto possui seu nome, a data na qual ele vai ser apresentado, e um grupo associado, do qual o projeto faz parte. A relação projeto-grupo é de 1:1.

## Modelo Avaliacao
Cada avaliação é identificada por seu id, em todos os campos que forem relacionadas. Como cada professor ou aluno pode fazer uma avaliação de um dado projeto do InovaWeek, o modelo de avaliação precisa ter campos que expressem notas de acordo com os critérios do InovaWeek. De acordo com os critérios oficiais para a avaliação de um projeto do Inova, divulgado pela própria universidade, os critérios são:
- Maturidade
- Inovação
- Apresentação
- Atratividade

Logo, os campos maturidade, inovacao, apresentacao e atratividade representam justamente os critérios de avaliação do Inova, e todos os campos são do tipo float, o que permite ver a nota parcial da avaliação de acordo com o critério escolhido. A junção de todas as notas escolhidas para esses critérios caracteriza a nota final da avaliação para com o projeto, e esta também está representada na avaliação pelo campo notaFinal, manifestado em tipo float, assim como os critérios de avaliação. Para dar continuidade, cada avaliação precisa ter um professor ou um aluno como autor, e como só é permitido um dos dois para cada avaliação, os campos que representam os objetos Professor e Aluno são opcionais, significando que uma avaliação pode existir sem um dos dois atrelados à ela. Para a identificação dos professores e alunos que são autores de uma avaliação, é utilizado os campos alunoId e professorId para especificar o id de cada autor. Por fim, é importante notar que a relação de avaliação-professor e avaliação-aluno é de 1:N, ou seja, uma avaliação só pode ter um autor (seja ele professor ou aluno), mas um professor ou aluno pode realizar várias avaliações tomando como base projetos distintos do InovaWeek.

## Modelo Professor
Cada professor é identificado pelo seu id, em todos os campos que forem relacionados. Um professor possui o seu nome, e uma lista de avaliações, na qual ele pode optar por preencher com várias avaliações ou nenhuma avaliação. A relação de professor-avaliação é caracterizada sendo 1:N, ou seja, um professor pode ter várias avaliações, mas uma avaliação só pode ter um professor atrelado à ela.

# Minimundo

A Inovaweek constitui uma iniciativa promovida pela Universidade de Vila Velha com o objetivo de introduzir propostas inovadoras no mercado. Ao longo dessa semana, o Inova recebe uma variedade de projetos concebidos por estudantes da instituição. Cada projeto, composto por, no máximo, quatro alunos, será avaliado por professores e outros colegas. As apresentações desses projetos têm datas e horários predeterminados, uma vez que os estandes serão utilizados por diferentes grupos em dias distintos.

Os grupos participantes da Inovaweek serão identificados por um nome, um aluno designado como líder e um título para o seu projeto. Simultaneamente, os alunos serão reconhecidos por meio de sua matrícula, nome e grupo. Por fim, os professores terão um nome e um identificador pessoal associado.

