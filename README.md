# Trabalho efetivo discente - Banco de dados

> Status: Concluído

## QUESTÃO

Um consultório médico deseja um sistema de informação para controlar o atendimento aos pacientes feitos pelos médicos.

No consultório médico existem funcionários encarregados da limpeza, funcionários responsáveis pelo atendimento aos pacientes e médicos, que por sua vez possui especialização em uma ou mais áreas. Existem várias especialidades médicas (clínica geral, cardiologia, urologia, dermatologia, etc). Cada médico possui ao menos uma especialidade e uma especialidade possui ao menos um médico especializado.

Para os funcionários é importante armazenar o nome, rg, endereço residencial e telefone. Os funcionários que fazem atendimentos aos pacientes devem possuir curso superior em enfermagem, sendo necessário armazenar o ano de conclusão da graduação, a faculdade cursada e qual foi o título do projeto final elaborado.

Para os médicos é importante saber o número no CRM e todos os possíveis telefones de contato, caso haja alguma emergência. Os médicos do consultório podem ou não ser credenciados a algum convênio. Caso isso ocorra, esses médicos concedem descontos em suas consultas de acordo com o contrato elaborado e até terminar o prazo de vigência do convênio. Os descontos concedidos não são uniformes para todos os médicos de um convênio. Um médico pode ser credenciado a um ou mais convênios.

Os convênios possuem sigla, nome, telefone e hospital que realiza os exames.

Para os pacientes é importante armazenar o rg, nome, endereços e seus telefones de contato. Um paciente pode realizar várias consultas com vários médicos. No entanto, um médico atende um paciente de cada vez. As consultas devem ser agendadas com antecedência, sendo indicado nesse momento se o paciente é conveniado ou não.

Durante uma consulta o médico pode solicitar ao paciente alguns exames, que devem ser realizados no hospital assistido pelo convênio do paciente. Caso o paciente não seja conveniado, ele realiza os exames em um hospital de sua escolha. Para os exames é necessário armazenar o local onde foi realizado, a data solicitada e qual é a sua categoria.

Os funcionários podem agendar também consultas, e neste caso, os pacientes são atendidos normalmente.

 

 

1)    Elabore o modelo de entidade e relacionamentos para o consultório médico.

2)    Gere os scripts SQL de criação das tabelas.


## SOLUÇÃO

