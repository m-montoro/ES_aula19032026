![alt text](DUC_samuelbedin_murilomontoro.png)

## UC01 — Cadastrar Novo Aluno

### Ator Principal
Recepcionista

### Objetivo
Registrar os dados de um novo aluno no sistema, vinculando-o a um plano.

### Pré-condições
- A recepcionista deve estar autenticada no sistema.
- Devem existir planos cadastrados e ativos no sistema.

### Pós-condições
- Aluno cadastrado com sucesso e com status inicial definido.

### Fluxo Principal
1. A recepcionista seleciona a opção "Cadastrar Aluno".
2. O sistema exibe o formulário de cadastro.
3. A recepcionista preenche dados pessoais, contato e endereço.
4. A recepcionista seleciona o plano contratado.
5. O sistema salva os dados e gera o perfil do aluno.
6. O sistema emite a cobrança inicial e aguarda pagamento.

### Fluxos Alternativos
- **A1 — CPF já cadastrado:**
  O sistema exibe uma mensagem de erro informando que o aluno já existe e sugere redirecionar para a tela de edição ou renovação.

### RF Relacionados
- RF01 — Cadastro de Alunos
- RF02 — Gerenciamento de Planos

### RNF Relacionados
- RNF02 — Segurança
- RNF04 — Usabilidade

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC02 — Atualizar Cadastro de Aluno

### Ator Principal
Recepcionista / Aluno

### Objetivo
Permitir a alteração de dados cadastrais de um aluno existente.

### Pré-condições
- O usuário deve estar autenticado.
- O aluno deve estar previamente cadastrado no sistema.

### Pós-condições
- Dados do aluno atualizados no banco de dados.

### Fluxo Principal
1. O usuário acessa o perfil do aluno.
2. O usuário seleciona a opção "Editar Dados".
3. O sistema exibe os dados atuais preenchidos.
4. O usuário altera os dados desejados (ex: endereço, telefone).
5. O usuário clica em "Salvar".
6. O sistema valida e atualiza as informações.

### Fluxos Alternativos
- **A1 — Dados inválidos:**
  O sistema destaca os campos incorretos (ex: e-mail sem '@') e impede o salvamento até a correção.

### RF Relacionados
- RF01 — Cadastro de Alunos

### RNF Relacionados
- RNF02 — Segurança
- RNF04 — Usabilidade

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC03 — Criar Plano de Assinatura

### Ator Principal
Gerente

### Objetivo
Cadastrar um novo tipo de plano (mensal, anual, funcional, etc.) para oferta aos alunos.

### Pré-condições
- O gerente deve estar autenticado no sistema.

### Pós-condições
- Novo plano criado e disponível para novas matrículas.

### Fluxo Principal
1. O gerente acessa o módulo de "Planos" e clica em "Novo Plano".
2. O sistema exibe o formulário de criação.
3. O gerente informa nome, modalidade, valor e periodicidade.
4. O gerente salva o plano.
5. O sistema registra o plano como ativo.

### Fluxos Alternativos
- **A1 — Nome do plano em uso:**
  O sistema avisa que já existe um plano com o mesmo nome e pede uma alteração.

### RF Relacionados
- RF02 — Gerenciamento de Planos

### RNF Relacionados
- RNF04 — Usabilidade

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC04 — Editar e Desativar Plano de Assinatura

### Ator Principal
Gerente

### Objetivo
Alterar informações de um plano existente ou torná-lo inativo para novas vendas.

### Pré-condições
- O gerente deve estar autenticado e deve existir pelo menos um plano cadastrado.

### Pós-condições
- Plano atualizado ou desativado. Planos de alunos atuais não sofrem quebra de contrato.

### Fluxo Principal
1. O gerente acessa a lista de planos.
2. O gerente seleciona um plano e clica em "Editar" ou "Desativar".
3. Se editar, altera os dados e salva; se desativar, confirma a inativação.
4. O sistema atualiza o status do plano no banco de dados.

### Fluxos Alternativos
- **A1 — Cancelar edição:**
  O gerente clica em "Cancelar" e nenhuma alteração é feita.

### RF Relacionados
- RF02 — Gerenciamento de Planos

### RNF Relacionados
- RNF04 — Usabilidade

### RN Relacionadas
- RN06 — Acesso restrito por perfil

---

## UC05 — Registrar Pagamento na Recepção

### Ator Principal
Recepcionista

### Objetivo
Registrar o recebimento presencial da mensalidade de um aluno.

### Pré-condições
- Recepcionista autenticada.
- Aluno com cobrança pendente.

### Pós-condições
- Pagamento registrado e status de regularidade do aluno atualizado para "Em dia".

### Fluxo Principal
1. A recepcionista busca o aluno e seleciona a cobrança pendente.
2. A recepcionista informa a forma de pagamento (Dinheiro, Cartão ou PIX) e o valor pago.
3. O sistema valida se o valor corresponde ao total.
4. A recepcionista confirma o recebimento.
5. O sistema registra o pagamento e atualiza a situação do aluno imediatamente.

### Fluxos Alternativos
- **A1 — Tentativa de pagamento parcial:**
  O sistema bloqueia a ação, exigindo o valor integral conforme regra de negócio.

### RF Relacionados
- RF03 — Controle de Pagamentos
- RF04 — Regularidade do Aluno

### RNF Relacionados
- RNF03 — Performance

### RN Relacionadas
- RN04 — Pagamento parcial (não permitido)
- RN06 — Acesso restrito por perfil
- RN07 — Atualização automática da regularidade

---

## UC06 — Gerar Boleto/Link de Pagamento Online

### Ator Principal
Aluno

### Objetivo
Permitir que o aluno acesse o sistema para pagar sua mensalidade de forma remota.

### Pré-condições
- Aluno autenticado.
- Cobrança gerada e em aberto.

### Pós-condições
- Boleto ou link de pagamento gerado e exibido para o aluno.

### Fluxo Principal
1. O aluno acessa a área "Financeiro".
2. O aluno seleciona a fatura em aberto e escolhe "Pagar Online".
3. O sistema gera o boleto ou código PIX.
4. O aluno copia o código ou baixa o boleto para pagamento externo.

### Fluxos Alternativos
- **A1 — Fatura já paga:**
  O sistema não exibe a opção de geração, mostrando apenas o recibo.

### RF Relacionados
- RF03 — Controle de Pagamentos

### RNF Relacionados
- RNF01 — Disponibilidade
- RNF02 — Segurança

### RN Relacionadas
- RN07 — Atualização automática da regularidade

---

## UC07 — Validar Acesso na Catraca

### Ator Principal
Sistema de Catraca (API Externa)

### Objetivo
Verificar se o aluno tem permissão para entrar na academia ao aproximar sua tag RFID.

### Pré-condições
- Aluno cadastrado com tag RFID vinculada.

### Pós-condições
- Acesso liberado fisicamente e registrado no histórico, ou acesso negado.

### Fluxo Principal
1. O aluno aproxima o RFID na catraca.
2. O Sistema de Catraca envia o ID via API JSON para o sistema FitPass.
3. O sistema FitPass verifica o status do aluno (regularidade).
4. Sendo regular, o sistema retorna "Acesso Permitido" em até 3 segundos.
5. O Sistema de Catraca libera a roleta.
6. O sistema FitPass registra o horário de entrada.

### Fluxos Alternativos
- **A1 — Acesso Negado (Inadimplência > 5 dias):**
  O sistema verifica que a mensalidade venceu há mais de 5 dias. Retorna "Acesso Negado" para a catraca, que mantém a roleta bloqueada.

### RF Relacionados
- RF04 — Regularidade do Aluno
- RF05 — Controle de Acesso

### RNF Relacionados
- RNF03 — Performance
- RNF06 — Integração

### RN Relacionadas
- RN01 — Bloqueio por inadimplência

---

## UC08 — Consultar Regularidade do Aluno (Automático)

### Ator Principal
Sistema (Job automático)

### Objetivo
Atualizar diariamente o status de regularidade dos alunos com base nos vencimentos.

### Pré-condições
- Existência de cobranças cad
