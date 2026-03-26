# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: Isaque Daniel Jeronimo
RA: 25001329
Data: 25/03/26

---

# 1. Definição do MVP
Descreva aqui **qual parte do sistema** foi incluída no seu MVP.  
Explique claramente:
Gestão de Estoque, Operação da Farmácia e Atendimento ao Cliente.
Foram imclidos no meu MVP Primeiro a Gestão de estoque pois sem ela o sistema não funciona ou teria que ser usado de uma forma anotada tudo no papél. 
Segundo operação da farmácia e atendimento ao cliente, sendo muito importante também para o funcionamento de alguma parte do sistema realizando o processo de venda com manuseio dos balcanistas.
Relatórios e Indicadores, Esse seria um marco importante para que a farmacia passe a utilizar ainda mais o sistema pois com isso é possivél tomar decisões estratégicas o que é muito valorizado para empresas.
Perfis de Usuários e Permissões, Vejo esse como um adicional do sistema completo garantindo que não ocorra algumas falhas ou acidentes no manuseio do sistema. Porém ele é muito necessário para uma boa garantida de que nada de errado acontecerá como por exemplo uma venda com vlor de desconto muito baixo que não seria altorizada com esse processo.


Fora do MVP:
Contas a pagar e a receber, por ser algo que não é necessário para o uso, o sistema ja faz registro do inventario e a venda, ou seja essa parte de contas a pagar e a rececber não era necessaia como fundamental para o sistea funcionar.
Compras e Fornecedores, não está no MVP pois na gestão de estoque ele é como se fosse um adicional para ela.
Perfis de Usuários e Permissões, Vejo esse como um adicional do sistema completo garantindo que não ocorra algumas falhas ou acidentes no manuseio do sistema.
Integração de Processos, Aqui estamos em uma parte em que o sistema ja esta perfeitamente funcional porém um pouco manual, com essa integração de processos pode-se dividir o sistema para cada usuario com base em suas funções, focando apenas no que interesa para cada setor


- O que está **dentro** do MVP  
- O que está **fora** do MVP  
- Por que você fez essas escolhas  

---

# 2. Regras de Negócio (mínimo: 5)
Liste e descreva **cada RN** de forma clara.

**RN01 Verificação de itens no estoque antes da Venda—**  
**RN02 Confirmação de entrega de mercadorias—**  
**RN03 Registro de Venda—**  
**RN04 Atualização de inventario—**  
**RN05 Verificação de indentidade e permisão para alterar valores—**  

---

# 3. Requisitos Funcionais (mínimo: 8)
Liste os requisitos funcionais do seu MVP.

**RF01 Login de Usuario—**  
**RF02 Recuperação de senha—**  
**RF03 Cadastro de clientes—**  
**RF04 Atualização de inventario—**  
**RF05 Verificação de itens no inventario antes da venda—**  
**RF06 Validação de um reestoque—**  
**RF07 Confirmar indentidade de usuario para mudança de preços—**  
**RF08 Atualização de perfil—**  

---

# 🛡 4. Requisitos Não Funcionais (mínimo: 4)
Liste os RNFs do sistema conforme seu MVP.

**RNF01 Segurança de dados—**  
**RNF02 Bom tempo de resposta—**  
**RNF03 Atualizar inventario sem precisar atualizar o aplicativo—**  
**RNF04 Exibir perfil do usuario atual em alguma parte da tela—**  

---

# 5. Casos de Uso (mínimo: 10)
### Inserir **diagrama de casos de uso geral**, demonstrando claramente:

@startuml
left to right direction
skinparam packageStyle rectangle
skinparam monochrome true
skinparam shadowing false

actor "Atendente" as AT
actor "Farmacêutico" as FA
actor "Gerente" as GE
actor "Financeiro" as FI
actor "Adm/Sistema" as SIS

package "Sistema Farmácia" {
    usecase "UC01: Realizar Venda" as UC01
    usecase "UC02: Cadastrar Cliente" as UC02
    usecase "UC07: Validar Receita" as UC07
        usecase "UC03: Manter Produtos" as UC03
    usecase "UC04: Atualizar Estoque" as UC04
    usecase "UC05: Registrar Compra" as UC05
    usecase "UC06: Relatórios" as UC06
    usecase "UC08: Usuários" as UC08
    usecase "UC09: Contas a Receber" as UC09
    usecase "UC10: Contas a Pagar" as UC10
}
AT --> UC01
AT --> UC02
FA --> UC07
UC07 ..> UC01 : <<extend>>
GE --> UC03
GE --> UC05
GE --> UC06
FI --> UC09
FI --> UC10
SIS --> UC04
SIS --> UC08
UC01 ..> UC04 : <<include>>
UC05 ..> UC04 : <<include>>
@enduml


- os 10 casos
- relação entre eles e atores
- pelo menos 3 includes
- pelo menos 3 extends

---

# 6. Documentação dos Casos de Uso
Para **cada caso de uso**, utilize o template abaixo:
---

## **UCXX — Nome do Caso de Uso**
**Ator(es):**  
**Descrição:**  
**Pré-condições:**  
**Pós-condições:**  

### Fluxo Principal
1.  
2.  
3.  
4.  

### Fluxos Alternativos / Exceções
- FA01 —  
- FA02 —  

### Relacionamentos
- **Include:** (listar quando aplicável)  
- **Extend:** (listar quando aplicável)  

### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

---

## UC01 — Realizar Venda de Produtos
  Atores: Atendente, Farmacêutico.
  Descrição: Permite registrar a venda de medicamentos ou itens de conveniência
  Pré-condições: Usuário autenticado no sistema; Produtos devem estar cadastrados.
  Pós-condições: Estoque atualizado; Comprovante emitido; Registro financeiro criado.

###Fluxo Principal
O Atendente inicia uma nova venda.
O Atendente pesquisa o produto nome, codigo ou fabricante
O sistema verifica a disponibilidade no estoque da unidade RN01
O Atendente informa a quantidade e adiciona ao carrinho.
O sistema calcula o valor total
O Atendente finaliza a venda e escolhe a forma de pagamento

###Fluxos Alternativos / Exceções
FA01 — Produto com estoque insuficiente: O sistema alerta e impede a venda do item.
FA02 — Venda de medicamento controlado: O sistema pede validação do Farmacêutico.

###Relacionamentos
Include: UC02 e UC04 
Extend: UC09

##UC02 — Cadastrar Cliente
  Ator: Atendente, Gerente.
  Descrição: Registro de novos clientes no sistema para histórico de compras e vendas a prazo
  Pré-condições:
  Pós-condições: Cliente salvo na base de dados

###Fluxo Principal
O Atendente acessa a tela de cadastro de clientes
O Atendente insere nome, CPF e dados de contato.
O sistema valida se o CPF já existe.
O sistema confirma o salvamento do registro

###Fluxos Alternativos / Exceções
FA01 — CPF Inválido: O sistema solicita a correção dos dados
FA02 — Cliente já cadastrado: O sistema exibe os dados atuais para edição

###Relacionamentos
Include: 
Extend:

(Código do plantUML da UC01, 2 e 7 para não ficar muito pequeno)

@startuml
left to right direction
skinparam monochrome true
actor "Atendente" as AT
actor "Farmacêutico" as FA
package "Módulo de Vendas" {
    usecase "UC01: Realizar Venda" as UC01
    usecase "UC02: Cadastrar Cliente" as UC02
    usecase "UC07: Validar Receita" as UC07
    usecase "UC09: Registrar Conta a Receber" as UC09
}
AT --> UC01
AT --> UC02
FA --> UC07
UC07 .> UC01 : <<extend>>
UC09 .> UC01 : <<extend>>

@enduml




##UC03 — Manter Cadastro de Produtos
Ator: Gerente
Descrição: Incluir, alterar ou excluir informações de produtos 
Pré-condições: Usuário com perfil de Gerente
Pós-condições: Dados do produto atualizados no catálogo

###Fluxo Principal
O Gerente acessa o módulo de produtos
O Gerente seleciona Novo ou pesquisa um produto existente
O Gerente altera os campos necessários como preço de venda
O sistema solicita confirmação de identidade para alteração de valores RN05
O sistema salva as alteraçoes

###Fluxos Alternativos / Exceções
FA01 — Tentativa de exclusão de produto com estoque: O sistema impede a exclusão e sugere inativação

###Relacionamentos
Include:
Extend: 

##UC04 — Atualizar Estoque
  Atores: Sistema, Gerente.
  Descrição: Ajusta as quantidades físicas de produtos na unidade após vendas, perdas ou transferências

  Pré-condições: Ocorrência de um evento de movimentação.

  Pós-condições: Saldo de estoque refletindo a realidade física.


###Fluxo Principal
O sistema recebe a notificação de uma venda ou entrada.
O sistema identifica o ID do produto e a unidade.
O sistema subtrai ou soma a quantidade da RN04.
O sistema verifica se o nível está abaixo do mínimo e alerta.

###Fluxos Alternativos / Exceções
FA01 — Ajuste Manual: O Gerente informa o motivo da alteração e corrige o saldo.

###Relacionamentos
Include:
Extend: 

##UC05 — Registrar Compra de Fornecedor
Atores: Gerente, Setor Administrativo.
Descrição: Registrar a entrada de mercadorias compradas de fornecedores.
Pré-condições: Fornecedor cadastrado.
Pós-condições: Estoque incrementado, conta a pagar gerada.

###Fluxo Principal
O Gerente insere os dados da nota fiscal de compra.
O Gerente lista os produtos e quantidades recebidas.
O sistema confirma a entrada da mercadoria da RN02.
O sistema atualiza o preço de custo.

###Fluxos Alternativos / Exceções
FA01 — Produto Novo: O sistema encaminha para o UC03 para realizar cadastro prévio.

###Relacionamentos
Include: UC04 e UC10.
Extend: 

(codigo da uc3,4,5)

@startuml
left to right direction
skinparam monochrome true
actor "Gerente" as GE
actor "Sistema" as SIS
package "Módulo de Estoque" {
    usecase "UC03: Manter Produtos" as UC03
    usecase "UC04: Atualizar Estoque" as UC04
    usecase "UC05: Registrar Compra" as UC05
}
GE --> UC03
GE --> UC05
SIS --> UC04
UC05 ..> UC04 : <<include>>
@enduml

##UC06 — Gerar Relatórios de Desempenho
Atores: Gerente, Administrador.
Descrição: Emissão de documentos com indicadores de vendas, produtos mais vendidos.
Pré-condições: Existência de dados no período solicitado.
Pós-condições: Relatório exibido em tela ou exportado.

###Fluxo Principal
O Usuário seleciona o tipo de relatório.
O Usuário define os filtros de data e categoria.
O sistema processa os dados armazenados.
O sistema exibe os resultados e indicadores.

###Fluxos Alternativos / Exceções
FA01 — Nenhum dado encontrado: O sistema informa que não há registros.
###Relacionamentos
Include: 
Extend: 

(Codio que inclui a 6 e a 8 que estão ligadas)
@startuml
left to right direction
skinparam monochrome true
actor "Administrador" as ADM
actor "Gerente" as GE
package "Módulo Administrativo" {
    usecase "UC06: Gerar Relatórios" as UC06
    usecase "UC08: Gerenciar Usuários" as UC08
}
ADM --> UC08
ADM --> UC06
GE --> UC06
@enduml


##UC07 — Validar Receita Médica
  Ator: Farmacêutico.
  Descrição: Verificação técnica de receitas para medicamentos controlados.
  Pré-condições: Venda de item controlado iniciada.
  Pós-condições: Venda autorizada ou bloqueada.

###Fluxo Principal
  O Farmacêutico analisa a receita física ou digital.
  O Farmacêutico insere os do paciente no sistema.
  O Farmacêutico confirma a validade da receita.
  O sistema libera o item na UC01.

###Fluxos Alternativos / Exceções
  FA01 — Receita Vencida: O Farmacêutico nega a validação e o sistema bloqueia o item na venda.

###Relacionamentos
  Include:
  Extend: extensão do UC01

##UC08 — Gerenciar Usuários e Permissões
Ator(es): Administrador.
Descrição: Controle de quem pode acessar o sistema e quais funções estão liberadas para cada perfil.
Pré-condições: Usuário logado como Administrador.
Pós-condições: Perfis de acesso atualizados.

###Fluxo Principal
O Administrador acessa o painel de usuários.
O Administrador seleciona um funcionário.
O Administrador atribui um perfil Atendente, Financeiro, etc.
O sistema aplica as restrições de acesso conforme o perfil.

###Fluxos Alternativos / Exceções
FA01 — Bloqueio de Usuário: o Administrador desativa o acesso de um funcionário desligado.

###Relacionamentos
Include: 
Extend:

##UC09 — Registrar Conta a Receber
Ator: Sistema, Setor Financeiro.
Descrição: Lançamento automático ou manual de valores que a farmácia recebe de clientes.

Pré-condições: Venda a prazo finalizada.
Pós-condições: Lançamento financeiro criado com status em aberta.

###Fluxo Principal
sistema identifica uma venda com forma de pagamento prazo.
gera uma parcela com valor, data de vencimento e identificação do cliente.
O Financeiro monitora o status da conta.

###Fluxos Alternativos / Exceções
FA01 — recebimento da Conta: O Financeiro altera o status para recebida ao confirmar o pagamento.

###Relacionamentos
Include: 
Extend: extensão do UC01

##UC10 — Registrar Conta a Pagar
Ator: Sistema, Setor Financeiro.
Descrição: Registro de contas financeiras da farmácia.

Pré-condições: Compra realizada ou despesa fixa identificada.
Pós-condições: Lançamento financeiro criado no fluxo de caixa.

##Fluxo Principal
o sistema recebe os dados de uma compra da UC05.
registra o valor e a data de vencimento.
o Setor Financeiro valida.

###Fluxos Alternativos / Exceções
FA01 — lançamento de despesa manual: cadastra uma conta que não necessita de validação para compra de produtos.
###Relacionamentos
Include: 
Extend: extensão do UC05
(código da 9 e 10)
@startuml
left to right direction
skinparam monochrome true
actor "setor Financeiro" as FIN
actor "Sistema" as SIS
package "modulo Financeiro" {
  usecase "UC09: Registrar Conta a Receber" as UC09
  usecase "UC10: Registrar Conta a Pagar" as UC10
}
FIN --> UC09
FIN --> UC10
SIS --> UC09
SIS --> UC10
@enduml



