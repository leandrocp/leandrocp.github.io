---
layout: post
title: Configuração Maven Nexus
---

## Nexus

[Sonatype Nexus](http://www.sonatype.org/nexus/) é um conhecido servidor Maven para instalações em ambientes privativos, onde pode-se armazenar artefatos com acesso restrito e também se beneficiar do cache gerado localmente, o que é muito útil para diminuir o consudo de recursos de rede, especialmente em grandes empresas.

Para utilizar o repositório Nexus no lugar do padrão Maven Central, basta configurar o settings.xml no diretório conf da instalação do seu Maven, conforme exemplo:

## Configuração

## Deploy

Se deseja fazer o deploy de artefatos neste repositório, adicione o bloco servers no settings.xml

  <servers>
    <server>
      <id>releases</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>
    <server>
      <id>snapshots</id>
      <username>deployment</username>
      <password>deployment123</password>
    </server>
  </servers>

O usuário deployment vem criado por padrão com as permissões necessárias para o deploy de artefatos. Recomendo no mínimo trocar a senha padrão, ou criar outro usuários com as mesmas permissões. 

E finalmente adicione o bloco distributionManagement no pom.xml do seu projeto:

    <distributionManagement>
        <repository>
            <id>releases</id>
            <name>Releases</name>
            <url>http://IP.DO.NEXUS:8081/nexus/content/repositories/releases/</url>
        </repository>
        <snapshotRepository>
            <id>snapshots</id>
            <name>Snapshots</name>
            <url>http://IP.DO.NEXUS:8081/nexus/content/repositories/snapshots/</url>
        </snapshotRepository>
    </distributionManagement>

Substitua IP.DO.NEXUS pelo IP ou URL do servidor Nexus.

## Uso

Agora ao compilar seu projeto ou realizar um deploy, todos artefatos são tranferidos pelo Nexus.  