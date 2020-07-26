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
