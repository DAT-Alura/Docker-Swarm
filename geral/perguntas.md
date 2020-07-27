# Perguntas

## Aula 1

1 - O Docker Swarm apresenta uma série de vantagens em relação ao Docker usado de maneira tradicional. Marque as alternativas que contém essas vantagens:

- O Docker Swarm não precisa de uma rede para funcionar pois já vem com um driver customizado.
- __O Docker Swarm divide os containers entre múltiplas máquinas de um mesmo cluster de maneira automática.__

> Alternativa correta! Através do dispatcher o Docker Swarm define a melhor máquina para executar algum container

- __O Docker Swarm consegue resetar containers automaticamente em caso de falhas.__

> Alternativa correta! O Docker Swarm tem capacidade de reiniciar containers a fim de manter a aplicação funcionando.

- O Docker Swarm é uma nova versão do Docker, por isso é mais rápido, bem projetado e deve ser usado em produção.

2 - Vimos na última aula que a Docker Machine, por mais que não esteja relacionada diretamente ao Docker Swarm, pode nos ajudar bastante. Qual das alternativas abaixo contém uma funcionalidade da Docker Machine?

- __Ao utilizar a Docker Machine, podemos criar máquinas virtuais prontas para executar Docker.__

> Alternativa correta! A Docker Machine cria máquinas virtuais bem leves já provisionadas com o Docker.

- Com a Docker Machine, criamos containers de maneira mais rápida e fácil.
- A Docker Machine provê aos nossos containers maior segurança por utilizar o ssh.
- A Docker Machine instala o Docker Swarm em nossa máquina física de maneira mais fácil.

3 - Queremos criar nosso primeiro cluster para dividir os containers em diversas máquinas e não sobrecarregar uma única máquina. Qual dos comandos abaixo devemos utilizar para criar o cluster e darmos o primeiro passo para atingir nosso objetivo?

- docker swarm start now
- __docker swarm init__

> Alternativa correta! Além disso, a boa prática também seria utilizar a flag --advertise-addr.

- docker init swarm
- docker swarm start

## Aula 2

1 - Agora queremos adicionar nós ao swarm. Qual das alternativas abaixo é realmente uma responsabilidade dos nós workers dentro do swarm?

- Servir como segurança para caso o nó manager pare de funcionar, ele assuma o lugar dele.
- Alocar a memória para todos os nós do swarm.
- __São responsáveis pela execução dos containers dentro do swarm.__

> Alternativa correta! Como o nome diz, eles são os trabalhadores, responsáveis por rodar containers.

2 - Para executarmos comandos de leitura, como por exemplo ```docker node ls```, e/ou alteração no estado do swarm, temos uma condição. Qual das alternativas abaixo contém essa condição?

- Esses comandos podem ser executados tanto em nós managers quanto nós workers.
- __Podem ser executados apenas em nós managers.__

> Alternativa correta! Tais comandos ficam restritos apenas aos nós managers dentro do swarm.

- Podem apenas ser executados em nós workers.

3 - Vimos na última aula uma diferença bem importante entre os comandos docker service create e docker container run. Qual é essa diferença?

- O ```comando docker container run``` foi defasado. Hoje o recomendado pela empresa Docker é que se utilize apenas o comando docker service create.
- O ```comando docker container run``` só pode ser usado fora do swarm, enquanto o docker service create pode ser usado tanto dentro quanto fora.
- __O ```comando docker service create``` no final cria um container em escopo do swarm e o docker container run em escopo local.__

> Alternativa correta! Como vimos, essa é uma grande diferença entre os dois comandos.

- O ```comando docker service create``` no final cria um container em escopo local e o docker container run em escopo do swarm.

4 - Qual artifício do Docker Swarm permite que nós possamos acessar quaisquer serviços a partir do IP de qualquer nó dentro do swarm, apenas informando a porta?

- Router Nodes.
- __Routing Mesh.__

> Alternativa correta! Graças ao Routing Mesh conseguimos acessar diferentes serviços a partir de qualquer IP pertencente ao swarm.

- Service Tuner.
- Dispatcher.

## Aula 3

1 - Caso nosso único manager pare de funcionar, podemos ter problemas. O que acontecerá com o nosso swarm em caso de perda do manager?

- O swarm será destruído automaticamente.
- __As tarefas em execução em outros nós serão mantidas sem problemas.__

> Alternativa correta! A ausência do manager não afetará as tarefas de outros nós.

- __Não conseguiremos mais executar comandos de leitura e/ou criar novos serviços.__

> Alternativa correta! Com a ausência do manager, não teremos mais nós capazes de executar comandos administrativos.

- Todos as tarefas em execução, em quaisquer nós, irão parar de funcionar.

2 - É muito importante fazermos backup de todo o nosso swarm para evitarmos desastres. Por padrão, em qual diretório fica armazenado o conteúdo do nosso swarm?

- /etc/docker/swarm/state
- /run/docker/swarm
- __/var/lib/docker/swarm__

> Alternativa correta! Nesse diretório temos todas as configurações de estado do nosso swarm.

- /etc/docker

3 - Ao utilizarmos o comando docker node ls, como podemos identificar quais nós são managers dentro do nosso swarm?

- Basta olhar a coluna ```Manager Status``` e ver quais nós tem o valor ```Manager```.
- Basta olhar a coluna ```Manager Status``` e ver quais nós tem o valor ```Reachable```.
- __Basta olhar a coluna ```Manager Status``` e ver quais nós tem o valor ```Reachable``` ou ```Leader```.__

> Alternativa correta! Nós com esses status são managers dentro do nosso swarm.

- Basta olhar a coluna ```Manager Status``` e ver quais nós tem o valor ```YES```.

4 - Vimos que em caso de falhas do ```Leader``` do swarm, temos uma eleição entre os nós managers para definir o novo líder. Se tivéssemos um swarm com 7 nós managers, qual seria o nosso quórum necessário e número máximo de falhas para realização da eleição?

Obs: Caso não lembre das regras, reveja o último vídeo a partir dos 4:00.

- 2 para o quórum e 5 falhas no máximo.
- 3 para o quórum e 4 falhas no máximo.
- 5 para o quórum e 2 falhas no máximo.
- __4 para o quórum e 3 falhas no máximo.__

> Alternativa correta! Como nosso quórum é (N / 2) + 1 e o número máximo de falhas é (N - 1) / 2, temos o valor esperado.

## Aula 4

1 - No último vídeo, removemos um nó manager do swarm a partir de outro manager. Quais os procedimentos que devemos executar para realizar essa remoção?
- __Devemos primeiramente rebaixar o cargo do nó com o comando docker node demote e depois removê-lo com o comando docker node rm.__
> Alternativa correta! É necessário transformar o nó manager em worker e depois remover.
- Basta remover utilizando o comando docker node remove.
- Devemos primeiramente desligar o nó pertencente ao swarm e depois removê-lo com o comando docker node rm.
- Basta remover utilizando o comando docker node rm.

2 - Quando o nosso objetivo é restringir o comportamento de nós de um swarm, podemos utilizar o comando:
``` Docker
docker node update --availability drain
```
Qual das alternativas abaixo contém o comportamento esperado do nó sobre o qual foi aplicado esse comando?
- O nó será desligado mas continuará dentro do swarm.
- O nó ficará incomunicável com todos os outros nós do swarm.
- __O nó ficará indisponível para executar tarefas.__
> Alternativa correta! Com a disponibilidade em drain, não conseguiremos executar mais tarefas/containers nesse nó.

3 - Podemos também aplicar restrições em serviços utilizando o comando:
```docker service update --constraint-add [outras infos]```
Se quisermos restringir o comportamento para um serviço ser rodado apenas em nós workers, o que mais precisamos informar para o comando acima?
- node == worker
- __node.role == worker__
> Alternativa correta! Informando o role e fazendo a comparação com ==, não teremos problemas.
- node = worker
- node.equals == worker

## Aula 5

1 - No último vídeo, aprendemos diversos aspectos sobre serviços replicados. Quais das alternativas abaixo são verdadeiras sobre esse tipo de serviço?
- __Serviços replicados podem rodar em apenas um nó.__
> Alternativa correta! Basta definirmos para o serviço ter apenas uma réplica.
- O número de réplicas de um serviço não pode ser atualizada depois do serviço ser criado.
- Serviços replicados rodam necessariamente em todos os nós do swarm.
- __Serviços por padrão são criados no modo replicado.__
> Alternativa correta! Quando não informamos o modo desejado, criamos serviços replicados por padrão.

2 - No último vídeo, aprendemos diversos aspectos sobre serviços globais. Quais das alternativas abaixo são verdadeiras sobre esse tipo de serviço?
- __Bons exemplos de serviços globais são serviços de monitoramento e segurança.__
> Alternativa correta! Serviços que são críticos à aplicação como um todo podem e devem ser executados como globais para que todos os nós possam ser devidamente monitorados e estejam seguros.
- Serviços globais rodam em todos os nós do swarm, menos em managers.
- Para um serviço ser global, precisamos necessariamente criá-lo replicado e depois alterar com o docker service update.
