# Api com Flask e Python
Este ReadMe trata sobre a criação de uma api `Flask` usando como linguagem principal `Python`


## Estrutura de pastas
O principal motivo de separar os arquivos em pastas é manter a estrutura do projeto organizada e agrupar cada arquivo de acordo com sua funcionalidade

### models
Esta pasta contem os arquivos que representam as entidades do projeto onde elas vão ser representadas através de classes com seus atributos e alguns métodos de conversão de tipo

Exemplo de um arquivo da classe model
```python
class Carro:
  def __init__(self, id, cor, ano, modelo):
    self.id = id
    self.cor = cor
    self.ano = ano
    self.modelo = modelo

# Este método retorna um objeto que é uma forma padrão de trafego de dados da api
  def toDict(self):
    return {
      "id": self.id,
      "cor": self.cor,
      "ano": self.ano,
      "modelo": self.modelo,
  )

"""
Objeto Carro
{ id: 1, cor: azul, ano: 2026, modelo: SUV }
"""
```

### repositories
Esta pasta é responsável pelo fornecimento de dados, é ela que se conecta e busca os dados de arquivos, do banco ou até mesmo de outras APIs

Ela possui classes com os seguintes métodos:
- buscar_todos() pega todas as entidades contidas no banco de dados
- buscar_por_id() busca uma entidade especifica pelo id
- salvar() salva/adiciona entidades no banco
- atualizar() atualiza uma entidade especifica que é obtida através do id
- deletar() apaga uma entidade especifica obtida pelo id

### services
Esta pasta é responsável pelo gerenciamento e administração de regras da API, é ela que vai receber requisições e decidir o que deve ser feito no repository

Exemplo:
> Não pode haver mais de uma casa com o mesmo número

A partir desta regra ira ser decidido o que o repository deve fazer

### helpers
Esta pasta possui arquivos com funções que podem ser reutilizadas em outras classes ou funções mas que não possuem uma influencia direta nas entidades

Poderiam existir funções para:
- ler um JSON;
- salvar um JSON;
- formatar respostas;
- validar determinados dados;
- converter formatos;
- tratar alguma operação repetitiva.

### app.py
Este arquivo é o ponto principal da API, será através dela que vamos configurar o `Flask` e as rotas e end points

Exemplo:
```python
form flask import Flask

app = Flask(__name__)

# Estas são rotas padrão que toda API contem para fins de testes ou verificação onde uma retorna a versão e a outra o status da api
@app.route("/")
def index():
    return {"version": "1.0.0"}, 200

@app.route("/health")
def health():
    return {"status": "OK"}, 200
```

Também podem haver outros tipos de rotas e cada uma possuindo sua função
- @app.get() define uma rota do tipo get para requisitar dados
- @app.post() define uma rota do tipo post para adicionar novos dados
- @app.delete() define uma rota do tipo delete para apagar dados
- @app.put() define uma rota do tipo put para modificar um dado por completo
- @app.patch() define uma rota do tipo patch para modificar um dado mas apenas em algumas partes

Cada método cumpre uma função especifica e recebem o caminho url em formato de string para indicar o caminho que deve ser acessado para aquele metodo
Exemplo: 
```python
# Este método será executado automaticamente ao acessar http://localhost:5000/getDados
@app.get("http://localhost:5000/getDados")
def getDados():
  # Todo método independente da sua funcionalidade deve ter um retorno
  return dados, 200

  # Este por exemplo retorna os dados de algo e um código 200 que significa sucesso na requisição
```

### requirements.txt
Este arquivo é responsável por listar todas as dependências necessárias para o projeto funcionar corretamente

Exemplo:
```txt
Flask==3.0.4
```
Isto torna possível instalar automaticamente todas as dependências em outro dispositivos com apenas um comando 
```powershell 
pip install -r requirements.txt
```

### venv
Esta pasta é responsável pelo ambiente virtual python, ele serve basicamente como um container privado onde vão ficar armazenados as dependências do projeto servindo como um ambiente separado do python padrão do dispositivo para não haver conflito de versão, esta pasta não deve ser enviada para o repositório git pois pode haver conflito. 
