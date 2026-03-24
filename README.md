# Sistema de Requerimento Acadêmico com Integração via API

## Visão Geral

Este projeto consiste em um sistema de requerimento acadêmico desenvolvido para ambiente universitário, com integração via API ao Ambiente Virtual de Aprendizagem (AVA).

O sistema tem como objetivo automatizar a validação de alunos e o carregamento de seus dados acadêmicos, garantindo consistência e evitando redundância de informações.

---

## Objetivo

Permitir que alunos realizem requisições acadêmicas em um sistema próprio, validando automaticamente suas informações através de integração com o AVA (Moodle).

---

## Arquitetura e Funcionamento

O sistema segue uma lógica de consulta inteligente para otimizar performance e reduzir chamadas desnecessárias à API externa.

### Fluxo principal:

1. O usuário tenta realizar login no sistema
2. O sistema verifica se o aluno existe no banco de dados local
3. Caso não exista:

   * Realiza uma requisição via API ao AVA (Moodle)
   * Verifica se o aluno está devidamente matriculado
4. Se o aluno estiver válido:

   * Os dados são clonados do AVA
   * Persistidos no banco de dados local
5. A partir disso:

   * O login é realizado normalmente
   * O sistema passa a utilizar apenas os dados locais

Importante:

* A consulta à API externa ocorre apenas uma vez por usuário
* Evita chamadas repetitivas e melhora a performance

---

## Integração com AVA (Moodle)

A integração com o AVA permite:

* Validação de matrícula do aluno
* Importação de dados acadêmicos
* Sincronização inicial de informações

### Dados obtidos via API:

* Dados do aluno
* Curso
* Disciplinas
* Informações acadêmicas relevantes

---

## Funcionalidades

* Autenticação de usuários
* Validação de matrícula via API
* Sincronização de dados com AVA
* Persistência local de dados
* Sistema de requerimentos acadêmicos
* Controle de usuários, cursos e disciplinas

---

## Tecnologias Utilizadas

* PHP (Laravel)
* API REST
* Banco de dados relacional
* Integração com Moodle (AVA)


---

## Estrutura do Projeto

* Controllers:

  * AuthController: autenticação e login
  * UserController: gerenciamento de usuários
  * CourseController: gestão de cursos
  * DisciplineController: gestão de disciplinas
  * MoodleController: integração com API do AVA
  * RequerimentoController: controle de requerimentos
  * PermissionController: controle de permissões

* Diretórios principais:

  * routes/: definição de rotas
  * database/: estrutura e migrations
  * tests/: testes automatizados

---

## Estratégia de Testes

Foram implementados testes de API para validar:

* Autenticação de usuários
* Integração com o AVA
* Consistência dos dados retornados
* Regras de negócio (validação de matrícula)

### Tipos de testes:

* Testes funcionais de API
* Testes de integração
* Testes positivos e negativos

---

## Cenários de Teste

### Validação de aluno

* Deve validar aluno existente no AVA
* Não deve autenticar aluno não matriculado
* Deve buscar dados apenas uma vez
* Deve persistir dados corretamente no banco local

### Login

* Deve permitir login com usuário válido
* Não deve permitir login sem validação prévia
* Deve utilizar dados locais após sincronização

### Integração com API

* Deve consumir API do Moodle com sucesso
* Deve tratar falhas de comunicação
* Deve validar estrutura dos dados retornados

---

## Diferenciais do Projeto

* Estratégia de cache de dados (evita chamadas repetidas à API)
* Integração eficiente com sistema externo (AVA)
* Separação clara de responsabilidades
* Aplicação de testes em nível de API
* Foco em performance e consistência de dados

---

## Possíveis Melhorias

* Implementação de fila para sincronização assíncrona
* Cache com Redis
* Monitoramento de chamadas à API
* CI/CD com pipeline de testes
* Testes de carga

---

## Como Executar o Projeto

```bash
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan serve
```

---

## Como Executar os Testes

```bash
php artisan test
```

---


