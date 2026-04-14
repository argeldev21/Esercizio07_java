Codice SQL DDL per la creazione delle tabelle e delle chiavi:

-- TABELLA STUDENTI
CREATE TABLE studenti (
    id_studente INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    data_iscrizione DATE NOT NULL
);

-- TABELLA CORSI
CREATE TABLE corsi (
    id_corso INT PRIMARY KEY AUTO_INCREMENT,
    titolo VARCHAR(150) NOT NULL,
    descrizione TEXT,
    docente VARCHAR(100) NOT NULL
);

-- TABELLA ISCRIZIONI (relazione studenti ↔ corsi)
CREATE TABLE iscrizioni (
    id_iscrizione INT PRIMARY KEY AUTO_INCREMENT,
    studente_id INT NOT NULL,
    corso_id INT NOT NULL,
    data_iscrizione DATE NOT NULL,
    FOREIGN KEY (studente_id) REFERENCES studenti(id_studente),
    FOREIGN KEY (corso_id) REFERENCES corsi(id_corso),
    UNIQUE (studente_id, corso_id) -- evita doppie iscrizioni allo stesso corso
);

-- TABELLA VALUTAZIONI
CREATE TABLE valutazioni (
    id_valutazione INT PRIMARY KEY AUTO_INCREMENT,
    studente_id INT NOT NULL,
    corso_id INT NOT NULL,
    voto_finale DECIMAL(4,2) CHECK (voto_finale >= 0 AND voto_finale <= 30),
    FOREIGN KEY (studente_id) REFERENCES studenti(id_studente),
    FOREIGN KEY (corso_id) REFERENCES corsi(id_corso),
    UNIQUE (studente_id, corso_id) -- una sola valutazione per studente/corso
);
