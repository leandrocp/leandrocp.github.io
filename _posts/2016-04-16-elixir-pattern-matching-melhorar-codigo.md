---
layout: post
title: Elixir - Usando Pattern Matching para melhorar seu código
tags: [elixir, functional-programming]
---

Pattern Matching é o tipo de recurso que se leva um tempo para aprender e perceber o seu real valor. Felizmente temos [vários](http://elixir-lang.org/getting-started/pattern-matching.html) [materiais](https://elixirschool.com/pt/lessons/basics/pattern-matching/) e [artigos](http://philipsampaio.com.br/blog/2015/01/08/10-exemplos-de-pattern-matching-em-elixir) que nos ajudam nesta tarefa. Se você não tem ideia do que é Pattern Matching, recomendo ler os links antes de continuar.

Neste artigo vou mostrar um uso de Pattern Matching que me fez perceber como este recurso é poderoso e elegante. Vamos começar com um exemplo de código que pode ser familiar:

Quem nunca escreveu um código assim ?

{% highlight ruby %}
cliente = Cliente.new(id: 1000, cartao_fidelidade: true)
desconto_pedido = desconto(produto: pizza, cliente: cliente)

# Aplica 5% de desconto no valor do produto caso o cliente possua o cartão fidelidade.
# Caso não possua, envia email de marketing para oferecer o cartão fidelidade.
def desconto(produto:, cliente:)
    if cliente.cartao_fidelidade
        desconto = calcular_valor_desconto(produto, 5)
    else
        desconto = 0
        if cliente.email
            enviar_marketing_fidelidade(cliente.email)
        end
    end
    desconto # retorna o valor calculado do desconto
end
{% endhighlight %}

À primeira vista é um código inofensivo, mas este projeto irá crescer e o excesso de condicionais pode se tornar um problema na manutenção e evolução da base de código. Você já sabe que Pattern Matching, como o próprio nome diz, serve para casar padrões. Então como podemos reescrever nosso `desconto` para que fique mais legível e compreensível ?

{% highlight elixir %}
cliente = %{id: 1000, cartao_fidelidade: true, email: 'cliente@pizzaria.com'}
pedido = desconto(pizza, cliente)

def desconto(produto, %{cartao_fidelidade: false, email: nil}) do
    0
end

def desconto(produto, %{cartao_fidelidade: false, email: email_cliente}) do
    enviar_marketing_fidelidade(email_cliente)
    0
end

def desconto(produto, %{cartao_fidelidade: true}) do
    calcular_valor_desconto(produto, 5)
end
{% endhighlight %}

A grande diferença entre as duas versões é que usando Pattern Matching seu código se torna explícito adotando lógicas isoladas para cada condição, este é um efeito colateral típico de linguagens funcionais. Mas como o Elixir sabe qual função chamar ?

O [map](http://elixir-lang.org/getting-started/keywords-and-maps.html#maps) `cliente` possui as chaves `cartao_fidelidade` e `email`, que serão usadas para casar com os parâmetros de cada função.

