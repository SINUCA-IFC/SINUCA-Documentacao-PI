# Requisitos e regras de negócio

Referência: código dos repositórios e decisões de produto registradas até 27/11/2026. “Implementado” indica presença no código; a homologação com API real, contas de teste e dispositivos deve ser registrada por versão. Edvanderson, professor de Geografia e Product Owner/cliente, confirma regras e prioridades.

## Requisitos funcionais

Os identificadores RF001–RF014 preservam a referência da especificação anterior. Descrições ambíguas foram esclarecidas abaixo; funcionalidades futuras continuam identificadas como tal.

| ID | Requisito e verificação esperada | Situação |
| --- | --- | --- |
| RF001 | Organização gerencia delegações/países e consulta participantes vinculados. | Implementado; retirada de vínculo pendente no backend. |
| RF002 | Aluno cadastra conta individual, confirma e-mail e aguarda atribuição de delegação. Perfil permite editar os campos autorizados. | Implementado; remoção de foto e edição por pendentes precisam de ajuste. |
| RF003 | Alunos vinculados e organização trocam mensagens no chat da delegação; leitura é individual por usuário. | Implementado como Message/MessageRead, sem entidade “Resposta” separada. |
| RF004 | Administração técnica usa Django Admin com permissões administrativas. | Implementado; superusuário e organizador têm responsabilidades distintas. |
| RF005 | Visitantes leem postagens; organização cria, edita e exclui postagens com imagem opcional. | Implementado. |
| RF006 | Alunos autorizados criam, editam e excluem tarefas no seu escopo e alteram status no Kanban. | Implementado; ordem manual não persiste. |
| RF007 | Organização aprova alunos atribuindo delegações e gerencia conteúdos do evento. | Gestão implementada; provisionamento/convites controlados pendentes. |
| RF008 | Avaliadores registram notas por delegação e modalidade; servidor calcula resultados por tema. | Futuro; escala, pesos, correção e publicação dependem de Edvanderson. |
| RF009 | Avaliadores autorizados têm painel de avaliação e acesso ao conteúdo público. | Futuro; existe somente o papel no modelo. |
| RF010 | Organização cria, edita e exclui atividades com datas, local, delegações e links; aluno consulta atividades da sua delegação. | Implementado em Schedule. |
| RF011 | Cada item do cronograma corresponde a uma atividade Schedule. | Não existe contêiner separado; confirmar com Edvanderson se será necessário. |
| RF012 | Servidor restringe operações por papel, vínculo com delegação e propriedade dos recursos. | Implementado; testar tentativas de acesso entre contas e delegações. |
| RF013 | Filtrar postagens por categoria. | Futuro, sujeito à confirmação; Post não possui categoria. |
| RF014 | Tarefas podem ter responsáveis autorizados, com validação no servidor e aviso push aos novos responsáveis inscritos. | Implementado. |
| RF015 | Confirmar e-mail por código de seis dígitos, com expiração/reenvio; login por senha ou Google. | Implementado via allauth/JWT; SMTP e Google exigem homologação real. |
| RF016 | Consultar links de apoio da delegação e documentos associados a atividades. | Implementado para links; upload de PDF ainda não integra o formulário. |
| RF017 | Entregar Web Push para novas postagens, atribuições, chat e tarefas atrasadas. | Implementado; requer VAPID, permissão e agendador de atrasos. |
| RF018 | Consultar a história do evento. | Implementado com conteúdo local, sem editor administrativo. |
| RF019 | Verificar matrícula e titularidade em fonte oficial autorizada do instituto antes de habilitar participação como aluno. | Futuro; cadastro por Google e contas existentes também devem ser abrangidos. |
| RF020 | Recuperar/alterar senha com confirmação, expiração e tratamento de erros. | Fluxo integrado ao site pendente. |
| RF021 | Disponibilizar o link do Google Drive com as fotos de cada edição junto à história daquela edição, identificado pelo ano e acessível ao público previsto. | Tarefa pendente; obter e conferir os links com a organização. |
| RF022 | Permitir filtrar as postagens do mural por ano, com paginação consistente e acesso aos anos anteriores. | Possibilidade futura para quando houver mais de um ano de funcionamento; definir com Edvanderson se o ano se refere à publicação ou à edição. Não implementado. |
| RF023 | Disponibilizar uma tela “Como utilizar”, com tutoriais das páginas por perfil e orientações de instalação do app no celular conforme navegador e sistema operacional. | Requisito futuro; conteúdo e acesso à ajuda ainda precisam ser implementados e validados. |

## Regras de negócio

- RN01: o cadastro público cria aluno sem delegação; o cliente não escolhe privilégios. Contas administrativas e de avaliação exigem provisionamento controlado.
- RN02: confirmação de e-mail, verificação institucional de matrícula e atribuição de delegação são etapas diferentes. A verificação institucional ainda precisa ser implementada.
- RN03: cada aluno pertence a uma delegação por vez. A organização atribui o país ao aprovar a participação; retirada de vínculo não deve excluir a conta.
- RN04: mensagens são compartilhadas pela delegação, mas a posição de leitura pertence a cada pessoa. Pendentes e avaliadores não têm acesso ao chat.
- RN05: tarefas validam responsáveis e escopo no servidor. A exclusão de usuário pode apagar tarefas de sua autoria; definir desativação e preservação antes de exclusões operacionais.
- RN06: atividades e links podem ser compartilhados por várias delegações. Editar/excluir um recurso compartilhado afeta todas; documentos da atividade devem estar disponíveis para os países envolvidos.
- RN07: upload de PDF é diferente de cadastrar link. Arquivos possuem dono, limites de tamanho e cota; URL pública de mídia não equivale a documento privado.
- RN08: Web Push depende da autorização do navegador. Ausência de push não remove mensagens não lidas. O campo legado Task.notification não controla a entrega.
- RN09: notas, modalidades, critérios, prioridades e novas funcionalidades dependem da decisão final de Edvanderson. Registrar as decisões e critérios de aceite antes de implementar.

## Requisitos não funcionais

| ID | Requisito | Como verificar |
| --- | --- | --- |
| RNF01 | Interface responsiva e utilizável por teclado. | Exercitar os fluxos nos tamanhos mobile/desktop e verificar foco, rótulos e feedback. |
| RNF02 | Autorização efetiva no servidor. | Testar acesso sem sessão, por papel, conta e delegação diferentes. |
| RNF03 | HTTPS em produção; segredos somente no servidor; CORS/CSRF e cookies adequados ao OAuth. | Revisar configuração e validar cadastro, Google e logout no ambiente publicado. |
| RNF04 | API REST Django/DRF e interface Vue; ORM com SQLite local/PostgreSQL configurável; Gunicorn/WhiteNoise. | Conferir configuração, migrações e build em instalação limpa. MySQL/Tomcat não descrevem a implementação atual. |
| RNF05 | Dados privados da API não entram no cache da PWA. | Inspecionar Service Worker/cache; modo offline oferece o shell público, sem edição offline. |
| RNF06 | Dados escolares e credenciais de integração ficam restritos ao necessário para a finalidade. | Revisar permissões, respostas, logs e acesso autorizado à fonte de matrícula. |
| RNF07 | Backup e restauração antes de migrações relevantes e operação com dados reais. | Registrar teste de restauração e responsáveis. |
| RNF08 | Manutenção com PDM sem ambientes virtuais, migrações versionadas e testes isolados. | Executar os comandos da passagem de bastão em instalação limpa. |
| RNF09 | Metas de desempenho e disponibilidade definidas com o cliente e a hospedagem. | Acordar carga, tempos e período de medição; realizar teste e monitoramento antes de declarar uma meta atendida. |
| RNF10 | Publicar e homologar uma versão de front/back para o primeiro uso do evento em 2027, a partir de uma branch de publicação definida, possivelmente main. | Confirmar a branch acompanhada pela hospedagem, registrar commits, aplicar migrações e validar os fluxos reais e a atualização da PWA antes da estreia. |

## Homologação

Para cada versão, registrar commits do front/back, banco, navegador/dispositivo, cenário, resultado e responsável. Cobrir cadastro/código/reenvio, Google, expiração/logout, aprovação, isolamento entre contas, tarefas, cronogramas/links compartilhados, chat e push. APIs simuladas não substituem a integração real. Critérios específicos de matrícula e notas estão na [passagem de bastão](PASSAGEM-DE-BASTAO.md).

A estreia prevista para 2027 exige novo deploy e homologação da versão escolhida. Para os álbuns, conferir o link no contexto de cada edição e seu acesso pelo público previsto. Se o filtro anual for aprovado no futuro, testar anos com e sem postagens, troca de ano, limites de datas e paginação.
