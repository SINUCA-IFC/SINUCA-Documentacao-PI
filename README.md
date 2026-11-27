# SINUCA — documentação do projeto

O Simulado Interdisciplinar das Nações Unidas do Campus Araquari reúne delegações de alunos em debates, mesas de cooperação e atividades culturais. A aplicação centraliza comunicados, materiais, tarefas, cronogramas e a comunicação entre participantes e organização.

## Responsáveis

**Product Owner / cliente: Edvanderson, professor de Geografia do instituto.** A próxima equipe pode identificá-lo pelo primeiro nome. Manter contato para esclarecer dúvidas, validar entregas e definir prioridades. A decisão final sobre notas, modalidades, regras do evento e novas funcionalidades é dele.

Professores orientadores do desenvolvimento: [Marco André Mendes](https://github.com/marcoandre), [Eduardo da Silva](https://github.com/eduardo-da-silva) e Professor Edvanderson Ramalho dos Santos.

Equipe de 2026:

- [Carlos Henrique Pereira Santos](https://github.com/carloshenriqueok)
- [Maria Carolina da Silveira](https://github.com/maricarols)
- [Maria Clara Pavanello Giareta](https://github.com/MCPavanello)
- [Pedro Gabriel Gonçalves](https://github.com/PedGabriel)

## Documentos para continuidade

- [Passagem de bastão](docs/PASSAGEM-DE-BASTAO.md): execução com PDM, funcionamento, operação, pendências e próximos passos.
- [Requisitos e regras de negócio](docs/REQUISITOS.md): situação de cada funcionalidade e critérios de verificação.
- [Modelo de dados](docs/MODELO-DE-DADOS.md): diagrama gerado automaticamente a partir do backend e instruções de atualização.
- [Revisão dos requisitos e da descrição do projeto](docs/REVISAO-DOCUMENTACAO-PI.md): diferenças em relação à especificação anterior e decisões pendentes.

## Situação do sistema

Visitantes acessam mural e história. Alunos se cadastram individualmente, confirmam e-mail e aguardam atribuição de delegação. Alunos vinculados usam tarefas/Kanban, cronogramas, documentos, perfil e chat. Organizadores gerenciam delegações, aprovação, postagens, cronogramas e links. Há PWA e Web Push com VAPID.

**Avaliações, médias e painel do avaliador são requisitos futuros.** O papel de avaliador no cadastro de usuários não significa que essas funções existam. Também faltam verificação de matrícula em fonte oficial do instituto, convites controlados e a integração de retirada de participante. As pendências detalhadas estão na passagem de bastão.

Frontend: Vue 3, Vite, Pinia e Axios. Backend: Django, Django REST Framework, allauth e JWT. O ORM usa SQLite no desenvolvimento e PostgreSQL configurável para produção; a aplicação é servida por Gunicorn e WhiteNoise. O curso utiliza PDM com ambientes virtuais desativados.

## Preparação para 2027 e próximas edições

O primeiro uso do site no evento está previsto para **2027**. Preparar um novo deploy de front/back em uma branch definida para publicação, possivelmente `main`, e homologar antes da estreia; confirmar a branch realmente acompanhada pela hospedagem.

No conteúdo histórico, incluir o link do Google Drive das fotos junto à história de cada edição. Quando houver mais de um ano de funcionamento, avaliar com Edvanderson um filtro anual de postagens. Essas tarefas e possibilidades estão detalhadas nos requisitos e na passagem de bastão.

## Repositórios e ambientes

| Parte | Código | Ambiente publicado |
| --- | --- | --- |
| Frontend | [SINUCA-FRONT](https://github.com/SINUCA-IFC/SINUCA-FRONT) | [Aplicação](https://sinuca-ifc-mocha.vercel.app) |
| Backend | [SINUCA-BACK](https://github.com/SINUCA-IFC/SINUCA-BACK) | [API](https://sinuca-backend.class.fabricadesoftware.ifc.edu.br/api/) |

Os READMEs de cada repositório contêm os comandos de instalação. Funcionalidade presente no código precisa ser homologada com a API real e os perfis envolvidos antes do uso no evento.
