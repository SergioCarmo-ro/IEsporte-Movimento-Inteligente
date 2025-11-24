# ENGENHARIA DE SOFTWARE  
## MANUTENÇÃO E INTEGRAÇÃO DE SOFTWARE  
### TRABALHO PRÁTICO 5 – ENGENHARIA REVERSA

---

**Prof. Dr.:** Andey Rodrigues  
**Aluno:** Sérgio Ademir Rocha do Carmo  

---


# IEsporte – Movimento Inteligente

[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org/)  
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5)  
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)](https://www.javascript.com/)
[![Django](https://img.shields.io/badge/Django-092E20?style=flat&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat&logo=sqlite&logoColor=white)](https://www.sqlite.org/index.html)





---


## 🧾 Introdução

O **IEsporte - Movimento Inteligente** é uma plataforma web interativa voltada para fisioterapia e análise clínica de movimento. Desenvolvido com tecnologias modernas, o sistema proporciona a profissionais e pacientes o acesso a um painel dinâmico de exercícios corretivos, recursos avançados de cadastro, relatórios clínicos e futuras integrações com inteligência artificial e acessibilidade.

---

## 🧾 Objetivo

O objetivo principal do sistema IEsporte é:
- Facilitar o diagnóstico e acompanhamento do progresso de pacientes por profissionais de saúde.
- Prover aos usuários um ambiente digital para explorar, filtrar e executar exercícios voltados à correção postural e coordenação funcional.
- Garantir uma experiência inclusiva, segura e expansível para todos os públicos, com apoio à acessibilidade (Libras), segurança e privacidade de dados.

---

## 🧾 Escopo

O escopo do IEsporte compreende:
- Cadastro e autenticação de usuários, garantindo acesso seguro.
- Cadastro de atletas, atividades e sessões de treino, estruturando o histórico e o progresso individual.
- Visualização interativa dos exercícios, com filtros, detalhes e recomendações personalizadas.
- Geração e consulta de relatórios clínicos, apoiando decisões profissionais.
- Exclusão definitiva de conta e gerenciamento completo dos dados do usuário.
- Suporte à acessibilidade via integração sugerida com VLibras/HandTalk (Libras).
- Estrutura preparada para evolução, permitindo integração futura de módulos de IA e funcionalidades inclusivas, como chat adaptado.

O sistema organiza seu funcionamento em multiparalelismo de frontend SPA (HTML5/CSS3/JS) e backend Django (Python), com persistência por ORM e banco SQLite3, sendo fiel ao código e à arquitetura implementada no repositório original.

---

## 🌐 Visão Geral

IEsporte – Movimento Inteligente é um sistema web/móvel (ou híbrido) para **gerenciamento de atividades esportivas**, com login de usuários, visualização de atividades e painel administrativo para administradores. Ele utiliza arquitetura em camadas (cliente-servidor), e seu backend é construído em **Python**, com armazenamento em **SQLite**, enquanto o frontend usa **HTML5** e **JavaScript**.

---

## 🧾 Requisitos Funcionais

As funcionalidades do sistema são descritas como **histórias de usuário**, com critérios de aceitação e regras de negócio.


| ID    | História de Usuário | Critérios de Aceitação | Regras de Negócio | Evidências |
|-------|---------------------|-------------------------|--------------------|------------|
| **RF01** | Enquanto **novo usuário**, quero **criar uma conta informando e-mail e senha** para poder acessar o painel interativo e explorar exercícios corretivos. | - E-mail deve ser único e obrigatório.<br>- Solicitar leitura e aceite dos Termos de Uso.<br>- Autenticação automática após cadastro com direcionamento à tela principal. | - Não permitir cadastro com e-mail repetido.<br>- Cadastro só efetivado com aceite dos Termos.<br>- Senha deve ser armazenada com hash seguro. | Campos obrigatórios em `index.html`:<br>`<input type="email">`<br>`<input type="password">`<br>`<input type="checkbox" id="termos-uso">`<br>Validação obrigatória pelo JS.<br>Cadastro só avança com todos campos e termos marcados. |
| **RF02** | Enquanto **usuário cadastrado**, quero **realizar login** para acessar recursos disponíveis apenas para autenticados. | - Apenas usuários cadastrados podem acessar.<br>- Dados corretos permitem acesso.<br>- Se falhar, mostrar mensagem.<br>- Logout seguro. | - E-mail validado para existência.<br>- Senha validada via hash seguro.<br>- Logout invalida sessão/cookies. | Formulário de login em `index.html`.<br>Autenticação e alternância de exibição controladas pelo método JS:<br>`toggleView(isLoggedIn)`<br>Mensagens de erro exibidas por `UIManager.showMessage`. |
| **RF03** | Enquanto **usuário autenticado**, quero **visualizar e filtrar exercícios** interativamente para explorar recomendações de correção postural. | - Filtrar exercícios por categoria.<br>- Clique revela detalhes completos (objetivo, execução, recomendações).<br>- Imagens e descrições acessíveis. | - Permitido filtro “Todos” ou por categoria.<br>- Clique abre modal detalhado.<br>- Dados exibidos vindos do banco/JS. | `ExerciseManager` no JS exibe filtros e cards.<br>`renderFilters()` para filtro dinâmico.<br>`renderGrid()` para exibição.<br>Cards exibem informações e disparam modal para mais detalhes. |
| **RF04** | Enquanto **usuário autenticado**, quero **excluir minha conta permanentemente** para não manter meus dados na plataforma caso deseje sair. | - Aviso de ação irreversível.<br>- Modal de confirmação/aborto.<br>- Usuário é deslogado e redirecionado após exclusão. | - Só quem está autenticado pode excluir.<br>- Todos os dados do usuário eliminados.<br>- Exclusão irreversível. | Botão `delete-account-btn` no frontend.<br>JS exibe modal com confirmação:<br>`showDelete()`<br>Exclusão executada somente por usuário logado. |
| **RF05** | Enquanto **profissional ou usuário**, quero **cadastrar atletas (nome, idade, e-mail)** para registrar participantes e associar atividades. | - Nome, idade e e-mail obrigatórios.<br>- E-mail único por atleta. | - Proibir e-mail duplicado (`models.EmailField(unique=True)`).<br>- Idade positiva obrigatória. | Modelagem em `models.py`:<br>`Atleta(nome, idade, email)`.<br>Campo email único, idade positiva. |
| **RF06** | Enquanto **usuário**, quero **cadastrar atividades (nome, descrição, nível)** para organizar exercícios e adaptar ao perfil dos atletas. | - Nome, descrição (opcional) e nível obrigatórios.<br>- Nome deve ser único.<br>- Nível respeita opções predefinidas. | - Nível validado: iniciante, intermediário, avançado.<br>- Nome único obrigatório. | Modelagem em `models.py`:<br>`Atividade(nome, descricao, nivel)`.<br>Choices definidos em NIVEIS.<br>Nome único. |
| **RF07** | Enquanto **atleta autenticado**, quero **registrar sessões (atividade, data, duração)** para monitorar meu progresso e histórico. | - Sessão associa atleta, atividade, data e duração.<br>- Sem duplicidade de sessões (mesmo atleta, atividade, data).<br>- Duração positiva. | - Restrição: `unique_together = ('atleta', 'atividade', 'data')`.<br>- Duração positiva. | Classe `Sessao` em `models.py`:<br>FK para atleta e atividade.<br>Campos data automática e duração positiva.<br>Restrição `unique_together`. |
| **RF08** | Enquanto **atleta ou profissional**, quero **visualizar relatórios de progresso** para acompanhar evolução e tomar decisões clínicas/treinamento. | - Relatório apresenta detalhes e data.<br>- Só usuários autenticados acessam seus próprios relatórios. | - Relatórios vinculados ao usuário lógico.<br>- Detalhes armazenam observações e recomendações. | Classe `RelatorioProgresso` em `models.py`:<br>FK para `auth.User`.<br>Campos `data` e `detalhes`. |
| **RF09** | Enquanto **usuário surdo/deficiente auditivo**, quero **acessar conteúdo traduzido automaticamente para Libras**. | - Recurso (botão/configuração) ativa tradutor de Libras.<br>- Todo conteúdo textual relevante pode ser traduzido. | - Tradutor disponível por padrão ou fácil ativação.<br>- Solução com VLibras ou HandTalk.<br>- Não interfere na UI normal. | Plugin VLibras integrado via:<br>`<script src="https://vlibras.gov.br/app/vlibras-plugin.js"></script>` |
| **RF10** | Enquanto **usuário surdo/deficiente auditivo**, quero **usar chat acessível** para comunicação com profissionais/usuários. | - Chat compatível com tradução para Libras.<br>- Aceita mensagens escritas, opcionais em Libras.<br>- Mensagens de áudio transcritas automaticamente. | - Chat não depende de áudio.<br>- Botão ativa tradução.<br>- Mensagens permanecem acessíveis. | Exemplo de integração:<br>`<button onclick="VLibras.playMessage(document.getElementById('chat-message').value)">Ativar Tradutor</button>` #32 |

"""



## 🧾 Requisitos Não Funcionais — Sistema IEsporte

| ID      | Requisito Não Funcional                 | Descrição                                                                                               | Evidência/Código/Fonte                                        |
|---------|-----------------------------------------|---------------------------------------------------------------------------------------------------------|---------------------------------------------------------------|
| **RNF01** | Usabilidade                           | Interface intuitiva, responsiva e fácil navegação para todos os públicos.                               | Tailwind CSS, SPA, filtros interativos em `index.html`/`script.js`. |
| **RNF02** | Segurança                             | Proteção de dados, CSRF, hash de senhas e rotas/autenticação restrita.                                  | `csrf_token` em formulários Django; senha via hash; rotas protegidas nas views. |
| **RNF03** | Compatibilidade                       | Compatibilidade com os principais navegadores web e dispositivos móveis.                                | HTML5, CSS3 responsivo, testes multiplataforma.               |
| **RNF04** | Desempenho                            | Painel carrega rápido e sem travamentos, garantindo experiência fluida.                                 | Lógica SPA, scripts otimizados, manipulação DOM dinâmica.     |
| **RNF05** | Persistência de Dados                 | Dados (usuários, atletas, atividades, sessões) armazenados com confiabilidade.                          | ORM Django e banco `db.sqlite3`.                              |
| **RNF06** | Extensibilidade                       | Integração facilitada de novos módulos, IA ou plugins de acessibilidade.                                | Padrão Facade, modularização dos arquivos/código.             |
| **RNF07** | Acessibilidade                        | Acessível a usuários deficientes, incluindo tradução automática para Libras.                            | Integração sugerida VLibras/HandTalk; estrutura para inclusão no frontend. |
| **RNF08** | Localização e Internacionalização     | Preparado para múltiplos idiomas, ajustando datas e formatos conforme usuário.                         | Suporte Django a i18n/l10n e templates dinâmicos.             |
| **RNF09** | Privacidade                           | Dados pessoais tratados com confidencialidade, com opção de exclusão definitiva.                        | Funcionalidade para exclusão/autenticação, remoção do banco.  |


## 📐 Modelagem Estrutural e Comportamental

### Diagrama de Classes (UML)

<img width="1039" height="807" alt="image" src="https://github.com/user-attachments/assets/8dfb15b1-2637-4886-83b2-dd2c34a50900" />

---

### Diagrama de Sequência (UML) – Login

<img width="1016" height="838" alt="image" src="https://github.com/user-attachments/assets/3f14e0f3-25c9-46ea-af0a-5f13921d7915" />

---


## 🏗 Padrão de Arquitetura do Sistema IEsporte

## 1. MVC/MTV Django

O sistema segue o padrão **MVC** (Model–View–Controller), adaptado ao Django como **MTV** (Model–Template–View):

- **Model:**  
  Define as estruturas de dados e regras do domínio (`models.py`).  
  Exemplos: `User`, `Atleta`, `Atividade`, `Sessao`, `RelatorioProgresso`.

- **Template:**  
  Arquivos HTML que recebem dados e renderizam a interface para o usuário (`index.html` em `templates/`).

- **View (Controller):**  
  Implementa a lógica de processamento de requisições, manipula os modelos e define o que será mostrado nos templates (`views.py`).  
  Opera rotas, autenticação, filtros, respostas aos AJAX/REST, tratando o fluxo da aplicação.

---

## 2. Facade Pattern (Padrão Fachada)

- O sistema implementa o padrão **Facade** como componente centralizador do backend (`facade.py`).
- O **Facade** expõe métodos de alto nível para login, cadastro, listagem, registro, geração de relatório, abstraindo a complexidade das operações internas e tornando o sistema mais simples de usar e manter.
- Todo o fluxo complexo do backend passa, direta ou indiretamente, pelo Facade, garantindo desacoplamento e organização.

---

## 3. Camadas Separadas

- **Frontend:** SPA independente, focada na interface e consumo de APIs.
- **Backend:** Lógica central organizada no Django, com o Facade intermediando funcionalidades.
- **Banco de Dados:** Persistência relacional (SQLite) acessada exclusivamente pelo ORM do Django.

Essa arquitetura favorece separação de responsabilidades: o cliente (navegador ou app) apenas consome a API, o backend lida com a lógica de negócio e persistência, e o banco guarda os dados localmente ou em servidor.


  <img width="593" height="688" alt="Arquitetura Sistema IEsporte   MVC" src="https://github.com/user-attachments/assets/f966286c-0d38-4a47-92db-2f3291f222b9" />

  

  <img width="809" height="509" alt="Arquitetura do Sistema Iesporte" src="https://github.com/user-attachments/assets/23df85c4-2578-4f02-9c39-54f6299f2712" />

---

## 🧰  Stack Tecnológica do Sistema IEsporte

## Frontend

- **HTML5**
  - Estrutura principal da interface, organização dos elementos da SPA.
- **CSS3 (Tailwind CSS via CDN)**
  - Framework utilitário para layouts responsivos.
- **JavaScript (ES6+)**
  - Lógica dinâmica: filtros, manipulação de DOM, integração AJAX/REST.
- **Chart.js**
  - Gráficos interativos para painel de visualização dos dados.
- **Arquivos principais**
  - `index.html`: template SPA
  - `style.css`: estilos customizados
  - `script.js`: lógica dinâmica e requisições REST
- **[Futuro/Opcional]**
  - VLibras ou HandTalk: integração sugerida para acessibilidade via Libras.

---

## Backend

- **Python 3.13+**
  - Linguagem principal
- **Django 5.2.7**
  - Framework MVC/MTV: gerenciamento de rotas, autenticação, regras de negócio e segurança
- **Principais componentes**
  - `manage.py`: comando principal do projeto
  - `settings.py`, `urls.py`, `wsgi.py`: configuração global
  - `esporte_app/models.py`: entidades do domínio
  - `esporte_app/views.py`: controle de rotas e requisições
  - `esporte_app/facade.py`: padrão Facade, operações complexas centralizadas
  - `esporte_app/urls.py`: roteamento do app
  - `templates/`: HTML dinâmico
  - `static/js/`, `static/css/`: arquivos JS e CSS estáticos
- **Dependências (`requirements.txt`)**
  - Django==5.2.7
  - asgiref==3.10.0
  - sqlparse==0.5.3
  - tzdata==2025.2
- **Segurança**
  - Proteção CSRF, hash de senhas, rotas protegidas

---

## Banco de Dados

- **SQLite3**
  - SGBD relacional embutido, gerenciado pelo Django via ORM
  - Arquivo principal: `db.sqlite3`
  - Persistência de todas as entidades do domínio (usuários, atletas, atividades, sessões, relatórios)

---

## Padrões & Extras

- **Facade Pattern**
  - Centralizador das operações complexas no backend (`facade.py`)
- **MVC/MTV Django**
  - Separação clara entre dados (models), lógica/processamento (views) e interface (templates)
 

<img width="1276" height="575" alt="Stack Tecnologica 2" src="https://github.com/user-attachments/assets/ea083677-1007-4fe3-8fcd-fd435399b095" />



---
# 📝 Conclusão

A engenharia reversa do **IEsporte – Movimento Inteligente** permitiu mapear estrutura, funcionamento e tecnologia do sistema, com levantamento dos requisitos, modelos e padrões adotados. 

A análise confirma a arquitetura em camadas (frontend SPA, backend Django, banco SQLite3) e o uso de práticas modernas, como Facade e SPA, além da preparação para integrações futuras (IA, acessibilidade).

As evidências comprovam que cada função atende às necessidades dos usuários com segurança, usabilidade e inclusão. O documento oficializa as bases para manutenção, evolução e integração do sistema, apoiando o crescimento e a referência do **IEsporte** em gestão esportiva e clínica.


 
## ✅ Autor  **Sérgio Ademir Rocha do Carmo**
  © 2025 – *IEsporte: Movimento Inteligente* 





