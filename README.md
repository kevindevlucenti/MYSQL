-- Criação do banco de dados
CREATE DATABASE IF NOT EXISTS Faculdade_EAD;
USE Faculdade_EAD;

-- Tabela de Cursos
CREATE TABLE Cursos (
    id_curso INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

-- Tabela de Alunos
CREATE TABLE Alunos (
    id_aluno INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    data_nascimento DATE,
    id_curso INT,
    FOREIGN KEY (id_curso) REFERENCES Cursos(id_curso)
);

-- Tabela de Professores
CREATE TABLE Professores (
    id_professor INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    titulacao VARCHAR(50)
);

-- Tabela de Disciplinas
CREATE TABLE Disciplinas (
    id_disciplina INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    id_curso INT,
    FOREIGN KEY (id_curso) REFERENCES Cursos(id_curso)
);

-- Relação entre Disciplinas e Professores (muitos-para-muitos)
CREATE TABLE Disciplina_Professor (
    id_disciplina INT,
    id_professor INT,
    PRIMARY KEY (id_disciplina, id_professor),
    FOREIGN KEY (id_disciplina) REFERENCES Disciplinas(id_disciplina),
    FOREIGN KEY (id_professor) REFERENCES Professores(id_professor)
);

-- Tabela de Matrículas (Alunos em Disciplinas)
CREATE TABLE Matriculas (
    id_matricula INT AUTO_INCREMENT PRIMARY KEY,
    id_aluno INT,
    id_disciplina INT,
    data_matricula DATE,
    FOREIGN KEY (id_aluno) REFERENCES Alunos(id_aluno),
    FOREIGN KEY (id_disciplina) REFERENCES Disciplinas(id_disciplina)
);

-- Inserção de dados em Cursos
INSERT INTO Cursos (nome) VALUES 
('Engenharia de Software'),
('Administração'),
('Direito');

-- Inserção de dados em Alunos
INSERT INTO Alunos (nome, data_nascimento, id_curso) VALUES
('João Silva', '2000-05-10', 1),
('Maria Oliveira', '1999-08-20', 2),
('Carlos Souza', '2001-03-15', 1);

-- Inserção de dados em Professores
INSERT INTO Professores (nome, titulacao) VALUES
('Dr. Ana Paula', 'Doutorado'),
('Prof. Marcos Lima', 'Mestrado'),
('Dr. Fernanda Costa', 'Doutorado');

-- Inserção de dados em Disciplinas
INSERT INTO Disciplinas (nome, id_curso) VALUES
('Algoritmos', 1),
('Gestão Empresarial', 2),
('Direito Constitucional', 3),
('Banco de Dados', 1);

-- Relação Disciplina_Professor
INSERT INTO Disciplina_Professor (id_disciplina, id_professor) VALUES
(1, 1), -- Algoritmos - Ana Paula
(2, 2), -- Gestão - Marcos Lima
(3, 3), -- Direito - Fernanda Costa
(4, 1); -- Banco de Dados - Ana Paula

-- Matrículas
INSERT INTO Matriculas (id_aluno, id_disciplina, data_matricula) VALUES
(1, 1, '2024-02-01'),
(1, 4, '2024-02-01'),
(2, 2, '2024-02-01'),
(3, 1, '2024-02-02');

