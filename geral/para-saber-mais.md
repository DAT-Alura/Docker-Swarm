# Para saber mais

## Cloud e Docker Machine

Durante o curso, utilizaremos a ```Docker Machine``` apenas para criarmos nosso ambiente com diversas máquinas isoladas e iniciarmos nosso cluster.

Porém, a Docker Machine também é muito utilizada com provedores de serviço em nuvem, como a AWS! Podemos definir nossas credenciais, e, utilizando o driver ```amazonec2```, temos a possibilidade de criar diversas máquinas nos servidores da Amazon!

Caso tenha interesse, mais informações podem ser obtidas na [documentação](https://docs.docker.com/machine/examples/aws/) oficial.

## Outras restrições

No último vídeo vimos como podemos adicionar restrições a um serviço utilizando o comando:

```docker service update --constraint-add```
Utilizamos o comando acima para restringir serviços a funcionarem apenas em nós managers ou workers.

Porém, também podemos impor outros tipos de restrições, como id, hostname e o próprio role. Vamos ver alguns exemplos!

Caso quiséssemos restringir o serviço de id ci10k3u7q6ti para funcionar apenas em um nó com id t76gee19fjs8, poderíamos utilizar o comando:

```docker service update --constraint-add node.id==t76gee19fjs8 ci10k3u7q6ti```

Se o objetivo fosse fazer o serviço rodar apenas em nossa vm4 por exemplo, uma possibilidade seria utilizar:

```docker service update --constraint-add node.hostname==vm4 ci10k3u7q6ti```

Por fim, podemos também remover restrições criadas utilizando o comando de atualização passando a flag --constraint-rm. Para remover as duas restrições anteriores:

``` Docker
docker service update --constraint-rm node.id==t76gee19fjs8 ci10k3u7q6ti
docker service update --constraint-rm node.hostname==vm4 ci10k3u7q6ti
```

Após esse momento, quaisquer novas réplicas criadas para esse serviço poderão ser alocadas sem restrição alguma!

## Service Scale

Vamos supor que temos um serviço com id ci10k3u7q6ti. Como podemos escalar esse serviço para ter 5 réplicas?

Aprendemos uma das possibilidades de alterar o número de réplicas de um serviço utilizando o comando docker service update --replicas 5 ci10k3u7q6ti, mas esse não é o único meio!

Para isso também temos o comando docker service scale. Utilizando o id, podemos atualizar com o comando:

```docker service scale ci10k3u7q6ti=5```

Nesse caso, definimos 5 réplicas para o serviço. Os dois comandos produzem o mesmo resultado, o segundo é apenas uma forma resumida do primeiro comando.

## Containers e Overlay

Por mais que o driver overlay seja responsável por comunicar múltiplos hosts em uma mesma rede, também podemos conectar containers em escopo local criados com o comando docker container run em redes criadas com esse driver.

Para isso, basta no momento da criação da rede utilizarmos a flag --attachable:

```docker network create -d overlay --attachable my_overlay```

Com o comando acima, conseguiremos conectar tanto serviços como containers "standalone" em nossa rede my_overlay.

## Volumes no Swarm

Por padrão, tanto o Docker no modo standalone quanto o Docker Swarm, partilham apenas de um driver local para uso de volumes. Isso quer dizer que o Docker Swarm não possui, até então, solução nativa para distribuir volumes entre os nós.

Então, no exemplo do vídeo anterior, ao definirmos o volume para cada serviço, criamos um volume local dentro de cada nó que for executar a tarefa. Logo, os volumes não são compartilhados entre os diferentes nós do cluster.

Existem soluções que não são nativas do Docker Swarm para utilizar volumes distribuídos entre nós, que podem ser consultadas na [Docker Store](https://hub.docker.com/search?category=volume&q=&type=plugin).
