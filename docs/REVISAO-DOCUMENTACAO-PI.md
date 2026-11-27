# Revisão dos requisitos e da descrição do projeto

A descrição do projeto deve acompanhar o comportamento do código e separar funcionalidades implementadas, parciais e futuras. A referência consolidada está em [requisitos e regras de negócio](REQUISITOS.md); a [passagem de bastão](PASSAGEM-DE-BASTAO.md) detalha operação e pendências.

## Correções em relação à especificação anterior

| Tema | Descrição anterior desatualizada | Referência para a equipe |
| --- | --- | --- |
| Escopo | Avaliadores e notas apresentados junto às funções prontas. | Painel, lançamento, médias e publicação de notas são futuros; validar com Edvanderson. |
| Cliente | Autoridade sobre o produto pouco explícita. | Edvanderson, professor de Geografia, é PO/cliente e tem decisão final sobre regras e novas funcionalidades. Manter contato. |
| Participantes | “Manter membro” sem explicar ingresso. | Conta individual pública, confirmação de e-mail, espera e atribuição de país pela organização. |
| Matrícula | Número declarado tratado como dado suficiente do aluno. | Falta consulta oficial autorizada que comprove vínculo e titularidade; e-mail/Google não comprovam matrícula. |
| RF003 | “Manter resposta”. | O recurso existente é chat por delegação com Message e MessageRead; confirmar outro significado antes de criar entidade. |
| RF004/RF007 | Administrador e organizador tratados como cadastros equivalentes. | Administração técnica do Django e papel organizador são distintos, dentro do modelo User. |
| RF006 | Texto genérico com sufixo “sss”. | Especificar operações sobre tarefas, responsáveis, status e permissões. |
| RF008/RF009 | Avaliação/avaliador sem situação nem critérios. | Manter como futuros; papel no enum não implementa o fluxo. |
| RF010/RF011 | Cronograma e itens como entidades separadas. | Schedule já representa cada atividade; não existe contêiner separado. |
| RF013 | Filtragem de postagem por categoria como pronta. | Post não possui categoria; confirmar necessidade antes de alterar modelo/interface. |
| Documentos | Link de apoio e arquivo PDF confundidos. | Link é conteúdo consultado na delegação; Document é upload ainda sem integração completa no formulário. |
| Comunicação | Chat e história descritos como em construção. | Ambos existem; história é conteúdo local e chat é compartilhado por delegação, com leitura individual. |
| Autenticação | Contas criadas apenas pelo administrador ou uso de Firebase. | Cadastro público/allauth, código de e-mail e JWT; Google usa sessão/cookies e CSRF no backend. |
| Tecnologias | MySQL, MySQL Connector, Workbench e Apache Tomcat. | ORM Django, SQLite local/PostgreSQL configurável, Gunicorn/WhiteNoise. Desenvolvimento com PDM sem venv. |
| PWA | Instalação confundida com dados privados disponíveis offline. | Cache do shell público; edição offline de tarefas/chat não implementada. |
| Disponibilidade | “99%” e hardware mínimo sem medição. | Definir carga, métricas e monitoramento com hospedagem e cliente; não declarar cumprimento sem evidência. |
| Modelo de dados | Imagem externa sem fonte reproduzível. | Usar [diagrama gerado dos modelos Django](MODELO-DE-DADOS.md), mantendo fonte DOT e data de geração. |
| Texto acadêmico | Exemplos de padaria, ordem de serviço, loja e biblioteca. | Usar somente contexto, regras e atores do SINUCA. Remover credenciais de exemplos públicos. |

## Conteúdo por edição e estreia em 2027

- **História e fotos:** acrescentar como tarefa o link do Google Drive de cada edição junto à sua história, identificado pelo ano. Obter e validar os links com a organização.
- **Postagens por ano:** registrar como possibilidade futura, para depois de mais de um ano de funcionamento. Confirmar com Edvanderson se a classificação será pelo ano de publicação ou pela edição; o filtro ainda não existe.
- **Publicação:** o primeiro uso do site no evento será em 2027 e exige novo deploy e homologação. Definir a branch de origem da publicação (possivelmente `main`), conferir a configuração dos serviços e registrar as versões do front e do back efetivamente publicadas.

## Decisões pendentes com Edvanderson

- Escala de notas, critérios/pesos, modalidades, quantidade de avaliações, revisão/exclusão, publicação, médias, ranking e desempates.
- Elegibilidade institucional, fonte de matrículas disponível e tratamento de exceções, em conjunto com o setor autorizado do instituto.
- Provisionamento de organizadores/avaliadores e validade dos convites; endereço secreto sozinho não concede autorização.
- Necessidade de filtros de categoria no mural, PDF integrado, edição anual e ordem persistida do Kanban.

Registrar decisão, data e critérios de aceite. Ao mudar uma regra, atualizar requisitos, testes, modelo de dados e a passagem de bastão afetados. Exemplos e propostas técnicas não substituem a aprovação do cliente.

## Pontos ainda necessários na documentação do evento

Identificar responsáveis e canal de contato para deploy, banco, SMTP, Google, mídia, VAPID, backups e agendamento. Documentar a fonte oficial e o contrato da verificação de matrícula quando autorizados pelo instituto. Definir metas de desempenho/disponibilidade e reunir evidências de homologação por versão. Confirmar o diagrama de casos de uso com os perfis visitante, aluno pendente/vinculado, organizador, avaliador e administrador técnico; representar funções futuras separadamente.
