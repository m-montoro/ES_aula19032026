<img width="572" height="1972" alt="image" src="https://github.com/user-attachments/assets/40d9780c-a32a-434e-a0b2-21315241f2ae" />

# Documento de Casos de Uso Completos — Sistema FitPass

Este documento detalha os 20 casos de uso do sistema **FitPass**, preenchidos com informações detalhadas sobre fluxos, requisitos e regras de negócio, seguindo o modelo padrão solicitado.

---

## UC01 — Realizar Login
### Ator Principal
Usuário (Aluno, Recepcionista, Instrutor, Gerente)

### Objetivo
Permitir que o usuário acesse o sistema de forma segura, garantindo que apenas pessoas autorizadas utilizem as funcionalidades.

### Pré-condições
O usuário deve possuir um cadastro ativo no sistema com e-mail e senha previamente definidos.

### Pós-condições
A sessão é iniciada com sucesso e o usuário é redirecionado para a tela inicial (dashboard) correspondente ao seu perfil de acesso.

### Fluxo Principal
1. O usuário informa o e-mail e a senha cadastrados.
2. O sistema valida se os campos foram preenchidos corretamente.
3. O sistema verifica as credenciais no banco de dados.
4. O sistema autentica o usuário e identifica seu perfil (Aluno, Recepcionista, Instrutor ou Gerente).
5. O sistema redireciona o usuário para a tela inicial específica do seu perfil.

### Fluxos Alternativos
**A1 — Senha incorreta:**
  O sistema exibe uma mensagem informando que o e-mail ou a senha estão incorretos e solicita uma nova tentativa.

**A2 — Conta bloqueada:**
  Após três tentativas consecutivas de login sem sucesso, o sistema bloqueia a conta temporariamente e instrui o usuário a entrar em contato com o suporte ou recuperar a senha.

### RF Relacionados
RF_LOGIN - Autenticação de usuários.

### RNF Relacionados
RNF_SEGURANÇA - Criptografia de senhas; RNF_DESEMPENHO - Tempo de resposta de autenticação.

### RN Relacionadas
RN_BLOQUEIO_TENTATIVAS - Regra de bloqueio após falhas sucessivas.

<img width="546" height="313" alt="image" src="https://github.com/user-attachments/assets/dac363ff-1909-4183-b9a4-c09cf9709bf1" />


---

## UC02 — Manter Cadastro de Aluno
### Ator Principal
Recepcionista

### Objetivo
Gerenciar as informações cadastrais dos alunos, permitindo a criação, edição, consulta ou inativação de registros.

### Pré-condições
O Recepcionista deve estar autenticado no sistema.

### Pós-condições
Os dados do aluno são salvos ou atualizados permanentemente no banco de dados.

### Fluxo Principal
1. O ator seleciona a opção "Gerenciar Alunos" no menu principal.
2. O sistema exibe a lista de alunos cadastrados e a opção de "Novo Cadastro".
3. O ator insere os dados obrigatórios: Nome Completo, CPF, Data de Nascimento, E-mail, Telefone e o ID da tag RFID.
4. O sistema valida o formato do CPF e do E-mail.
5. O sistema verifica se o CPF já está cadastrado.
6. O sistema salva os dados e exibe mensagem de sucesso.

### Fluxos Alternativos
**A1 — CPF Duplicado:**
  O sistema identifica que o CPF já existe na base de dados e impede o salvamento, exibindo um alerta ao ator.

**A2 — Dados Incompletos:**
  O sistema destaca os campos obrigatórios não preenchidos e solicita a correção.

### RF Relacionados
RF_CADASTRO_ALUNO - Gestão de dados cadastrais.

### RNF Relacionados
RNF_DISPONIBILIDADE - Sistema deve estar disponível para cadastro em horário comercial.

### RN Relacionadas
RN_UNICIDADE_CPF - Um CPF não pode ser cadastrado duas vezes.

<img width="508" height="516" alt="image" src="https://github.com/user-attachments/assets/5efbe0de-cdde-4f1c-9cd4-fee93d9b8530" />


---

## UC03 — Manter Planos de Academia
### Ator Principal
Gerente

### Objetivo
Configurar as opções de planos oferecidos pela academia, incluindo modalidades, preços e periodicidades.

### Pré-condições
O Gerente deve estar autenticado com perfil administrativo.

### Pós-condições
O plano é registrado ou atualizado, ficando disponível para novas matrículas.

### Fluxo Principal
1. O gerente acessa a área de "Configurações de Planos".
2. Define o nome do plano (ex: VIP, Standard), valor da mensalidade e periodicidade (Mensal, Trimestral, Anual).
3. Seleciona as modalidades incluídas (Musculação, Crossfit, Natação, etc.).
4. O sistema valida se o valor informado é superior ao custo mínimo operacional.
5. O sistema registra o plano no catálogo.

### Fluxos Alternativos
**A1 — Plano com valor zero:**
  O sistema detecta o valor zero e solicita uma confirmação especial, tratando o registro como um "Plano Cortesia".

### RF Relacionados
RF_GESTAO_PLANOS - Configuração de ofertas comerciais.

### RNF Relacionados
RNF_USABILIDADE - Interface intuitiva para edição de valores.

### RN Relacionadas
RN_VALOR_MINIMO_PLANO - Valor não pode ser inferior ao piso estabelecido pela gerência.

<img width="546" height="465" alt="image" src="https://github.com/user-attachments/assets/3eda1527-0e88-498a-a660-1c1ffb41655e" />


---

## UC04 — Efetuar Matrícula
### Ator Principal
Recepcionista

### Objetivo
Vincular um aluno cadastrado a um plano específico, oficializando seu ingresso na academia.

### Pré-condições
O aluno deve estar previamente cadastrado e deve existir pelo menos um plano ativo no sistema.

### Pós-condições
A matrícula é ativada, o contrato é gerado e a primeira parcela financeira é criada.

### Fluxo Principal
1. O recepcionista busca o aluno pelo nome ou CPF.
2. Seleciona o plano desejado pelo aluno.
3. Define a data de início e a data de vencimento das mensalidades.
4. O sistema gera o contrato digital para visualização.
5. O ator confirma a operação de matrícula.
6. O sistema altera o status do aluno para "Ativo".

### Fluxos Alternativos
**A1 — Aluno com pendência:**
  O sistema verifica que o aluno possui débitos de períodos anteriores e exibe um alerta, bloqueando a nova matrícula até a regularização.

### RF Relacionados
RF_MATRICULA - Registro de vínculos contratuais.

### RNF Relacionados
RNF_CONFIABILIDADE - Garantia de integridade entre matrícula e financeiro.

### RN Relacionadas
RN_MATRICULA_ATIVA - Um aluno só pode ter uma matrícula ativa por vez.

<img width="540" height="541" alt="image" src="https://github.com/user-attachments/assets/cc5e68a3-d7dc-4d1c-b7f7-6c2e02b42e95" />


---

## UC05 — Registrar Pagamento
### Ator Principal
Recepcionista

### Objetivo
Registrar a entrada financeira referente às mensalidades ou taxas pagas pelos alunos.

### Pré-condições
O aluno deve possuir pelo menos uma parcela com status "Pendente" ou "Atrasada".

### Pós-condições
A parcela é marcada como "Paga", o saldo do aluno é atualizado e o recibo é disponibilizado.

### Fluxo Principal
1. O recepcionista localiza o aluno no sistema.
2. O sistema exibe a lista de parcelas em aberto.
3. O ator seleciona a parcela que será quitada.
4. Informa o método de pagamento: Dinheiro, Cartão de Crédito, Cartão de Débito ou Pix.
5. O sistema processa a baixa e gera um comprovante eletrônico.

### Fluxos Alternativos
**A1 — Pagamento Parcial:**
  O ator informa um valor menor que o total; o sistema registra o pagamento e mantém o saldo restante como pendente.

### RF Relacionados
RF_PAGAMENTOS - Controle de entradas financeiras.

### RNF Relacionados
RNF_SEGURANÇA_FINANCEIRA - Log de todas as transações financeiras.

### RN Relacionadas
RN_BAIXA_PAGAMENTO - Regra de cálculo de juros para pagamentos em atraso.

<img width="497" height="516" alt="image" src="https://github.com/user-attachments/assets/d9edaae2-02b4-4437-b446-407f1e5950b5" />

---

## UC06 — Validar Acesso na Catraca
### Ator Principal
Sistema de Catraca (API)

### Objetivo
Controlar automaticamente a entrada física dos alunos na unidade mediante leitura de tag RFID.

### Pré-condições
A tag RFID do aluno deve estar vinculada ao seu cadastro e aproximada do leitor da catraca.

### Pós-condições
O acesso é liberado fisicamente ou negado, com o registro do evento salvo no log de acessos.

### Fluxo Principal
1. A catraca lê o ID da tag e envia para o servidor do FitPass via API.
2. O sistema localiza o aluno vinculado àquela tag.
3. O sistema verifica se o status da matrícula é "Ativo".
4. O sistema verifica se não há mensalidades com atraso superior ao limite permitido.
5. O sistema envia o comando "Liberado" para a catraca.
6. A catraca abre o braço para passagem.

### Fluxos Alternativos
**A1 — Inadimplência:**
  O sistema identifica atraso no pagamento e retorna "Negado", exibindo na tela da catraca a mensagem "Procure a Recepção".

**A2 — Tag não reconhecida:**
  O sistema não encontra o ID da tag e nega o acesso por segurança.

### RF Relacionados
RF_CONTROLE_ACESSO - Integração com hardware de catraca.

### RNF Relacionados
RNF_TEMPO_RESPOSTA - A validação deve ocorrer em menos de 1 segundo.

### RN Relacionadas
RN_BLOQUEIO_INADIMPLENTE - Bloqueio automático após X dias de atraso.

<img width="546" height="370" alt="image" src="https://github.com/user-attachments/assets/f7d18dca-487b-47f5-9d5c-e73c3410d560" />


---

## UC07 — Agendar Aula Coletiva
### Ator Principal
Aluno

### Objetivo
Permitir que o aluno reserve uma vaga em aulas com limite de participantes (ex: Yoga, Spinning).

### Pré-condições
O aluno deve estar autenticado no aplicativo/portal e possuir matrícula ativa.

### Pós-condições
A vaga é reservada e o nome do aluno é incluído na lista de presença da aula.

### Fluxo Principal
1. O aluno acessa a "Grade de Horários" no sistema.
2. Filtra por modalidade ou data.
3. Seleciona a aula desejada e clica em "Agendar Vaga".
4. O sistema verifica a disponibilidade de vagas.
5. O sistema confirma a reserva e envia uma notificação de confirmação.

### Fluxos Alternativos
**A1 — Aula lotada:**
  O sistema informa que não há vagas e pergunta se o aluno deseja entrar na "Lista de Espera".

### RF Relacionados
RF_AGENDAMENTO - Reserva de horários e vagas.

### RNF Relacionados
RNF_CONCORRENCIA - Suporte a múltiplos agendamentos simultâneos sem duplicar vagas.

### RN Relacionadas
RN_LIMITE_VAGAS - Respeitar a capacidade máxima da sala definida no cadastro da aula.

<img width="483" height="461" alt="image" src="https://github.com/user-attachments/assets/a477ecb0-751b-4eff-a8d9-8520d03cfbdf" />


---

## UC08 — Registrar Presença em Aula
### Ator Principal
Instrutor

### Objetivo
Confirmar quais alunos agendados compareceram efetivamente à aula para fins de estatística e controle.

### Pré-condições
A aula deve estar em andamento ou ter ocorrido recentemente.

### Pós-condições
As presenças são salvas, permitindo a geração de relatórios de frequência.

### Fluxo Principal
1. O instrutor acessa o menu "Minhas Aulas".
2. Seleciona a aula atual.
3. O sistema exibe a lista de alunos que realizaram o agendamento.
4. O instrutor marca o check-box de presença para cada aluno presente.
5. O instrutor clica em "Finalizar Lista".

### Fluxos Alternativos
**A1 — Aluno não agendado:**
  O instrutor pode buscar o aluno pelo nome e adicioná-lo manualmente à lista de presença, caso haja vaga.

### RF Relacionados
RF_PRESENCA - Controle de frequência.

### RN Relacionadas
RN_VALIDACAO_PRESENCA - Presença só pode ser lançada no dia da aula.

<img width="400" height="545" alt="image" src="https://github.com/user-attachments/assets/16b86a31-0276-4c34-914a-57cf68e216e2" />


---

## UC09 — Realizar Avaliação Física
### Ator Principal
Instrutor

### Objetivo
Registrar os dados biométricos e de saúde do aluno para acompanhar sua evolução física.

### Pré-condições
O aluno deve estar presente e o instrutor deve estar autenticado.

### Pós-condições
A avaliação é salva e um gráfico de evolução é gerado automaticamente.

### Fluxo Principal
1. O instrutor inicia uma "Nova Avaliação" para o aluno selecionado.
2. Insere peso, altura, medidas de dobras cutâneas e perímetros corporais.
3. Preenche a anamnese (histórico de saúde).
4. O sistema calcula automaticamente o IMC e o % de Gordura.
5. O sistema salva a avaliação e disponibiliza o PDF para o aluno.

### RF Relacionados
RF_AVAL_FISICA - Módulo de avaliação antropométrica.

### RNF Relacionados
RNF_PRECISAO - Cálculos baseados em protocolos científicos (ex: Pollock).

### RN Relacionadas
RN_PERIODICIDADE_AVAL - Sugerir nova avaliação a cada 60 ou 90 dias.

<img width="377" height="397" alt="image" src="https://github.com/user-attachments/assets/c0f28de4-33bf-48b9-8d39-41fb7e7bcc55" />


---

## UC10 — Consultar Ficha de Treino
### Ator Principal
Aluno

### Objetivo
Visualizar a prescrição de exercícios feita pelo instrutor diretamente no celular ou terminal.

### Pré-condições
O aluno deve estar autenticado e o instrutor deve ter liberado uma ficha de treino.

### Pós-condições
O aluno visualiza a série de exercícios, cargas e repetições do dia.

### Fluxo Principal
1. O aluno clica na opção "Meu Treino".
2. O sistema identifica o dia da semana e exibe a ficha correspondente (Treino A, B ou C).
3. O sistema mostra vídeos ou imagens demonstrativas de cada exercício.
4. O aluno pode marcar o exercício como "Concluído".

### RF Relacionados
RF_TREINOS - Visualização de prescrições.

### RN Relacionadas
RN_VALIDADE_FICHA - Fichas expiram após 3 meses, exigindo nova prescrição.

<img width="382" height="397" alt="image" src="https://github.com/user-attachments/assets/0baa38d1-bf1f-4169-a5bb-0bc972b109e7" />


---

## UC11 — Gerar Relatório de Inadimplência
### Ator Principal
Gerente

### Objetivo
Extrair dados sobre alunos com pagamentos atrasados para ações de cobrança e gestão financeira.

### Pré-condições
Existência de dados financeiros no período solicitado.

### Pós-condições
Um arquivo (PDF ou CSV) é gerado com a lista detalhada de devedores.

### Fluxo Principal
1. O gerente acessa "Relatórios Financeiros".
2. Seleciona o filtro "Inadimplentes".
3. Define o período de vencimento e o valor mínimo de débito.
4. O sistema processa a busca no banco de dados.
5. O sistema exibe o resumo na tela e oferece o botão "Exportar".

### RF Relacionados
RF_RELATORIO_FINANCEIRO - Extração de dados gerenciais.

### RN Relacionadas
RN_REGRA_ATRASO - Considerar inadimplente apenas após 5 dias do vencimento.

<img width="430" height="397" alt="image" src="https://github.com/user-attachments/assets/7bccc54f-495e-4098-9a79-b50b6e4628fa" />


---

## UC12 — Configurar Grade de Horários
### Ator Principal
Gerente

### Objetivo
Organizar o cronograma semanal de aulas coletivas da academia.

### Pré-condições
Modalidades e instrutores devem estar previamente cadastrados.

### Pós-condições
A grade horária é publicada para visualização e agendamento pelos alunos.

### Fluxo Principal
1. O gerente acessa o "Calendário de Aulas".
2. Seleciona um horário vago, uma modalidade e um instrutor.
3. Define a sala e a capacidade máxima de alunos.
4. O sistema verifica se o instrutor já possui outra aula no mesmo horário.
5. O sistema salva a configuração na grade semanal.

### RF Relacionados
RF_GRADE_HORARIA - Planejamento de atividades.

### RN Relacionadas
RN_CONFLITO_HORARIO - O sistema impede o cadastro de duas aulas para o mesmo instrutor no mesmo horário.

<img width="437" height="405" alt="image" src="https://github.com/user-attachments/assets/ca7d56d1-25db-4cdc-a530-b11743e5a0a4" />


---

## UC13 — Cancelar Agendamento de Aula
### Ator Principal
Aluno

### Objetivo
Desistir de uma vaga reservada, permitindo que outros alunos utilizem o espaço.

### Pré-condições
O aluno deve ter um agendamento ativo para uma aula futura.

### Pós-condições
A vaga é liberada e o sistema notifica automaticamente o próximo da lista de espera.

### Fluxo Principal
1. O aluno acessa "Meus Agendamentos".
2. Seleciona a aula que deseja cancelar.
3. Clica no botão "Cancelar Reserva".
4. O sistema confirma o cancelamento e remove o nome da lista.

### Fluxos Alternativos
**A1 — Cancelamento fora do prazo:**
  Se o cancelamento ocorrer muito próximo ao início da aula, o sistema aplica uma advertência conforme as regras da academia.

### RN Relacionadas
RN_TEMPO_MINIMO_CANCELAMENTO - Cancelamento deve ser feito até 2 horas antes do início.

<img width="428" height="489" alt="image" src="https://github.com/user-attachments/assets/82fe0b94-540b-4f4d-bef3-0796640b3513" />


---

## UC14 — Emitir Recibo de Pagamento
### Ator Principal
Recepcionista

### Objetivo
Fornecer ao aluno um comprovante formal de quitação de valores.

### Pré-condições
O pagamento deve ter sido registrado com sucesso (UC05).

### Pós-condições
O documento é impresso ou enviado por e-mail/WhatsApp para o aluno.

### Fluxo Principal
1. Após finalizar o recebimento, o sistema pergunta se deseja emitir recibo.
2. O ator confirma e o sistema gera um documento com: Dados da Academia, Nome do Aluno, Valor, Data e Descrição do Serviço.
3. O sistema registra que o recibo foi emitido.

### RF Relacionados
RF_PAGAMENTOS - Emissão de comprovantes.

<img width="358" height="434" alt="image" src="https://github.com/user-attachments/assets/5c60f5fc-fdbd-42b9-945f-99463f51d0d7" />


---

## UC15 — Visualizar Dashboard Gerencial
### Ator Principal
Gerente

### Objetivo
Monitorar a saúde do negócio através de indicadores visuais em tempo real.

### Pré-condições
O Gerente deve estar autenticado.

### Pós-condições
O gerente visualiza gráficos de faturamento, taxa de evasão e lotação das aulas.

### Fluxo Principal
1. O gerente acessa a tela principal "Dashboard".
2. O sistema carrega os KPIs (Key Performance Indicators) do mês atual.
3. O gerente pode filtrar a visão por unidade ou período.

### RF Relacionados
RF_DASHBOARD - Visualização de métricas de negócio.

<img width="350" height="341" alt="image" src="https://github.com/user-attachments/assets/ff6e028b-46d4-4f78-aa1a-7622375a87f4" />


---

## UC16 — Vincular Tag RFID
### Ator Principal
Recepcionista

### Objetivo
Associar um cartão ou pulseira física ao cadastro do aluno para permitir o acesso pela catraca.

### Pré-condições
O aluno deve estar cadastrado e a tag física deve estar disponível.

### Pós-condições
O ID da tag é gravado no perfil do aluno, habilitando-o para uso no UC06.

### Fluxo Principal
1. O recepcionista abre o cadastro do aluno.
2. Clica em "Vincular Nova Tag".
3. O aluno aproxima a tag do leitor de mesa.
4. O sistema captura o ID único e associa ao CPF do aluno.
5. O sistema confirma o vínculo.

### RF Relacionados
RF_CONTROLE_ACESSO - Gestão de dispositivos de identificação.

<img width="351" height="452" alt="image" src="https://github.com/user-attachments/assets/4f8557e6-d5d4-40d6-8e3d-4af6bcc9f7ba" />


---

## UC17 — Manter Instrutor
### Ator Principal
Gerente

### Objetivo
Gerenciar o corpo técnico da academia, incluindo dados pessoais e especialidades.

### Pré-condições
Gerente autenticado.

### Pós-condições
Dados do instrutor salvos para uso na grade horária e fichas de treino.

### Fluxo Principal
1. O gerente acessa "Gestão de Colaboradores".
2. Insere dados como: Nome, Registro Profissional (CREF), Especialidades e Horário de Trabalho.
3. O sistema valida os campos e salva o registro.

### RF Relacionados
RF_CADASTRO_INSTRUTOR - Gestão de recursos humanos técnicos.

<img width="380" height="341" alt="image" src="https://github.com/user-attachments/assets/648ca9a8-2569-4c94-90c4-9baa299a4267" />


---

## UC18 — Registrar Saída na Catraca
### Ator Principal
Sistema de Catraca (API)

### Objetivo
Registrar o momento em que o aluno deixa a academia para controle de tempo de permanência.

### Pré-condições
O aluno deve ter registrado entrada anteriormente no mesmo dia.

### Pós-condições
O horário de saída é salvo, encerrando a sessão física de treino.

### Fluxo Principal
1. O aluno aproxima a tag do leitor de saída da catraca.
2. A catraca envia o ID para o sistema.
3. O sistema registra o log de saída vinculado à última entrada.
4. O sistema libera o braço da catraca para saída.

### RF Relacionados
RF_CONTROLE_ACESSO - Registro de logs de permanência.

<img width="372" height="341" alt="image" src="https://github.com/user-attachments/assets/2d3c6e5f-5502-4fa4-8c80-306b9042e034" />


---

## UC19 — Solicitar Trancamento de Matrícula
### Ator Principal
Aluno / Recepcionista

### Objetivo
Pausar temporariamente o contrato do aluno por motivos de viagem, saúde ou outros, sem cancelar o plano.

### Pré-condições
Matrícula deve estar ativa e sem débitos vencidos.

### Pós-condições
O status da matrícula muda para "Trancado" e as cobranças futuras são suspensas pelo período definido.

### Fluxo Principal
1. O aluno solicita o trancamento na recepção ou via app.
2. O ator informa o motivo e a data de retorno prevista.
3. O sistema verifica se o plano permite trancamento.
4. O sistema calcula a taxa de trancamento (se houver).
5. O sistema confirma a pausa do contrato.

### RN Relacionadas
RN_TAXA_TRANCAMENTO - Valor cobrado para manter a vaga; RN_DIAS_MAX_PAUSA - Limite de dias por ano para trancamento.

<img width="546" height="346" alt="image" src="https://github.com/user-attachments/assets/e9fef216-0a82-4315-94c7-97c0903efe61" />


---

## UC20 — Consultar Histórico de Avaliações
### Ator Principal
Aluno

### Objetivo
Permitir que o aluno acompanhe seu progresso físico ao longo do tempo através de dados históricos.

### Pré-condições
O aluno deve possuir pelo menos duas avaliações físicas realizadas (UC09).

### Pós-condições
O sistema exibe comparativos numéricos e gráficos de evolução.

### Fluxo Principal
1. O aluno acessa a aba "Minha Evolução".
2. Seleciona as datas das avaliações que deseja comparar.
3. O sistema gera um gráfico de linha mostrando a variação de peso, massa magra e gordura.
4. O aluno pode baixar o relatório comparativo em PDF.

### RF Relacionados
RF_AVAL_FISICA - Histórico e acompanhamento.

<img width="546" height="327" alt="image" src="https://github.com/user-attachments/assets/d39ea369-70f4-4994-ac69-aecb334af049" />

