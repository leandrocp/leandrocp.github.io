---
layout: post
title: Como rodar Docker no MacOS
---

[Docker](https://www.docker.com/) é uma ferramenta para rodar aplicações em ambientes isolados, nos chamados Containers. É desta forma que empresas como Google, Twitter e muitas outras disponibilizam suas aplicações para milhões de usuários. E você também pode se beneficiar desta arquitetura.

O único sistema operacional suportado atualmente é o Linux, porém há formas de rodar o Docker no Mac com praticamente a mesma facilidade e performance, como veremos neste artigo.

**TL/DR**

* Instale os gerenciadores [brew](http://brew.sh/), [cask](https://github.com/caskroom/homebrew-cask) e também o git, caso ainda não tenha:
{% highlight bash %}
ruby -e "$(curl -fsSL
https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew install caskroom/cask/brew-cask

brew install git
{% endhighlight %}

* Instale o [VirtualBox](https://www.virtualbox.org/)
{% highlight bash %}
brew cask install virtualbox
{% endhighlight %}

* Instale o [Vagrant](https://www.vagrantup.com/)
{% highlight bash %}
brew cask install vagrant
{% endhighlight %}

* Instale o Docker
{% highlight bash %}
brew install docker
{% endhighlight %}

* Clone o projeto com o sistema pronto
{% highlight bash %}
git clone https://github.com/leandrocp/coreos-vagrant.git

cd coreos-vagrant
{% endhighlight %}

* Inicialize o Vagrant
{% highlight bash %}
vagrant up
{% endhighlight %}

* Aponte o host do docker
{% highlight bash %}
export DOCKER_HOST=127.0.0.1:2375
{% endhighlight %}

* Docker rodando!
{% highlight bash %}
docker info
{% endhighlight %}

A solução é simples: virtualizar um linux que possua docker, apontar o docker local para este ambiente, compartilhar arquivos e finalmente usar o Docker.

O projeto [boot2docker](http://boot2docker.io/) facilita todo esse processo, porém a performance dos arquivos compartilhados é sofrível. Por isso usamos o [CoreOS](https://coreos.com/), um sistema enxuto criado com o objetivo de rodar containers.

Você ainda pode customizar os parâmetros do CoreOS, para isso edite o arquivo [config.rb](https://github.com/leandrocp/coreos-vagrant/blob/master/config.rb) que está todo explicado com comentários.
