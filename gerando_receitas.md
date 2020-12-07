# **Gerando receitas baseadas no NiFi**

De início é necessário deletar o que não está sendo utilizado, para isso utilize:

```
helm uninstall my-release -n nomedonamespace 
```

Em seguida devemos instalar o NiFi dentro do nosso namespace, para isso utilize o seguinte comando:
```
helm install my-release cetic/nifi -n nomedonamespace --values=nifi-config-test.yml
```
Onde "nifi-config-test.yml" será o arquivo .  yml que será instalado.

Prossiga gerando os templantes("receitas") do arquivo "nifi-config-test.yml", para isso execute o comando:

```
helm template my-release cetic/nifi -n nomedonamespace  --values=nifi-config-test.yml --output-dir ./yamls
```

Após executar o script acima, será gerada uma pasta chamada "yaml". Dentro desta pasta você encontrará outra pasta chamada "nifi", e dentro da pasta "nifi", outra pasta chamada "template". Entre na pasta "template", para isso execute esses comandos:
```
cd yamls
cd nifi
cd templates
```
Dentro da pasta "templates" teremos 3 arquivos .yaml, deveremos utilizar o apply em cada um destes arquivos. Para isso execute o seguinte comando **dentro da pasta "template"**:
```
kubectl apply -f configmap.yaml -n nomedonamespace
kubectl apply -f service.yaml -n nomedonamespace
kubectl apply -f statefulset.yaml -n nomedonamespace
```
Para finalizar, executaremos o "port-forward", isso nos possibilitará abrir a interface gráfica do NiFi através do localhost. Para isso execute:
```
kubectl port-forward my-release-nifi-0 8080:8080 -n nomedonamespace
```
Teste se funcionou colando essa url em seu terminal:
```
localhost:8080/nifi
```
# Entendimento  das receitas
A respeito das "receitas"(templates), entendi que são arquivos yaml gerados a partir do values na hora da instalação do NiFi no namespace,
e que posteriormente, são essenciais para configurar o ambiente NiFi.

# Referências

https://docs.rapidminer.com/latest/deployment/kubernetes/

https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl_apply/


