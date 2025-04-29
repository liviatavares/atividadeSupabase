# Atividade Supabase - 29/04/2025

Seguem os comandos utilizados no SQL Editor no Supabase para criar as 3 tabelas de banco de dados (Alunos, Matrícula, e Cursos):

CREATE TABLE alunos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  turma TEXT NOT NULL,
  curso TEXT NOT NULL,
  data_nascimento DATE
);

CREATE TABLE cursos (
  id SERIAL PRIMARY KEY,
  nome TEXT NOT NULL,
  duracao_anos INT
);

CREATE TABLE matriculas (
  id SERIAL PRIMARY KEY,
  aluno_id INT REFERENCES alunos(id) ON DELETE CASCADE,
  curso_id INT REFERENCES cursos(id) ON DELETE CASCADE,
  data_matricula DATE DEFAULT CURRENT_DATE
);

INSERT INTO alunos (nome, turma, curso, data_nascimento)
VALUES ('Ana Lima', '1A', 'Engenharia Civil', '2002-05-10'),
       ('Bruno Souza', '1B', 'Administração', '2003-08-15');

INSERT INTO cursos (nome, duracao_anos)
VALUES ('Engenharia Civil', 5),
       ('Administração', 4);

INSERT INTO matriculas (aluno_id, curso_id)
VALUES (1, 1),
       (2, 2);

SELECT a.nome AS aluno, c.nome AS curso, m.data_matricula
FROM matriculas m
JOIN alunos a ON m.aluno_id = a.id
JOIN cursos c ON m.curso_id = c.id;

UPDATE alunos
SET curso = 'Engenharia de Produção'
WHERE nome = 'Ana Lima';

UPDATE cursos
SET nome = 'Administração de Empresas'
WHERE nome = 'Administração';

DELETE FROM alunos
WHERE nome = 'Ana Lima';

UPDATE cursos
SET nome = 'Administração Tech'
WHERE nome = 'Administração de Empresas';

UPDATE cursos
SET nome = 'Engenharia de Software'
WHERE nome = 'Engenharia Civil';

INSERT INTO cursos (nome, duracao_anos)
VALUES ('Engenharia da Computação', 4),
       ('Ciências da Computação', 4),
       ('Sistemas de Informação', 4);

UPDATE cursos
SET duracao_anos = 4
WHERE duracao_anos = 5;

INSERT INTO alunos (nome, turma, curso, data_nascimento)
VALUES ('Maria Vitória', '1B', 'Engenharia de Software', '2002-05-10'),
       ('Gabriel Leon', '1B', 'Administração Tech', '2004-09-14');

INSERT INTO alunos (nome, turma, curso, data_nascimento)
VALUES ('Matheus Scapolan', '1B', 'Engenharia da Computação', '2002-05-10'),
       ('Livia Tavares', '1B', 'Ciências da Computação', '2004-03-22');

SELECT a.nome AS aluno, c.nome AS curso, m.data_matricula
FROM matriculas m
JOIN alunos a ON m.aluno_id = a.id
JOIN cursos c ON m.curso_id = c.id;

INSERT INTO alunos (nome, turma, curso, data_nascimento)
VALUES ('Rodrigo Ferraz', '1A', 'Engenharia de Computação', '2002-04-10'),
       ('Bruna Mayer', '1B', 'Administração Tech', '2003-07-22'),
       ('Christian Lawrence', '1A', 'Sistemas de Informação', '2004-08-21'),
       ('Isaac Souza', '1B', 'Ciências da Computação', '2005-08-20'),
       ('Cristiano Benites', '1A', 'Engenharia de Software', '2006-08-19'),
       ('Julia Stateri', '1B', 'Engenharia de Computação', '2007-08-18'),
       ('Kizzy Terra', '1A', 'Administração Tech', '2001-08-17'),
       ('João Pedro', '1B', 'Sistemas de Informação', '2004-08-16');

INSERT INTO matriculas (aluno_id, curso_id)
VALUES 
  (
    (SELECT id FROM alunos WHERE nome = 'Maria Vitória'),
    (SELECT id FROM cursos WHERE nome = 'Engenharia de Software')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Gabriel Leon'),
    (SELECT id FROM cursos WHERE nome = 'Administração Tech')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Matheus Scapolan'),
    (SELECT id FROM cursos WHERE nome = 'Engenharia da Computação')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Livia Tavares'),
    (SELECT id FROM cursos WHERE nome = 'Ciências da Computação')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Rodrigo Ferraz'),
    (SELECT id FROM cursos WHERE nome = 'Engenharia da Computação')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Bruna Mayer'),
    (SELECT id FROM cursos WHERE nome = 'Administração Tech')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Christian Lawrence'),
    (SELECT id FROM cursos WHERE nome = 'Sistemas de Informação')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Isaac Souza'),
    (SELECT id FROM cursos WHERE nome = 'Ciências da Computação')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Cristiano Benites'),
    (SELECT id FROM cursos WHERE nome = 'Engenharia de Software')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Julia Stateri'),
    (SELECT id FROM cursos WHERE nome = 'Engenharia da Computação')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'Kizzy Terra'),
    (SELECT id FROM cursos WHERE nome = 'Administração Tech')
  ),
  (
    (SELECT id FROM alunos WHERE nome = 'João Pedro'),
    (SELECT id FROM cursos WHERE nome = 'Sistemas de Informação')
  );
