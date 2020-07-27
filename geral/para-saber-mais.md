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