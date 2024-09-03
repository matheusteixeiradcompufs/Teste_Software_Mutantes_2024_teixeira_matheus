# Tutorial para Análise de Cobertura e Testes de Mutação com `pycalculator`

Este tutorial descreve as etapas para analisar a cobertura de testes e realizar testes de mutação em um projeto Python utilizando as ferramentas `pytest`, `pytest-cov` e `mutmut`. O projeto utilizado como exemplo é o `pycalculator`, que está disponível no GitHub.

## 1. Clonagem do Repositório

Primeiro, escolha um projeto no GitHub que contenha casos de teste para trabalhar. Neste exemplo, utilizaremos o projeto `pycalculator`, que pode ser clonado com o seguinte comando:

```bash
git clone https://github.com/juliotrigo/pycalculator
````

## 2. Preparação do Ambiente

Após clonar o repositório, abra o terminal na pasta do projeto. Certifique-se de que o ambiente virtual está instalado e ativado, e instale os requisitos do projeto:

```bash
pip install -r requirements.txt
```

## 3. Instalação das Ferramentas Necessárias
Instale as ferramentas pytest, pytest-cov e mutmut, que serão utilizadas para realizar os testes e a análise de mutação:

```bash
pip install pytest pytest-cov mutmut
```

## 4. Execução dos Testes
Para verificar se todos os testes do projeto estão funcionando corretamente, utilize o comando:

```bash
pytest
```

## 5. Análise de Cobertura
Para verificar a cobertura dos testes, execute o comando abaixo:

```bash
pytest --cov=pycalculator --cov-branch --cov-report html
```

Este comando irá gerar um relatório de cobertura em HTML, que pode ser visualizado abrindo o arquivo index.html na pasta htmlcov gerada.

## 6. Execução do mutmut
Agora, vamos utilizar o mutmut para realizar testes de mutação no código. Execute o seguinte comando para gerar as mutações:

```bash
mutmut run --paths-to-mutate=path_do_projeto
```

Como resultado, você verá o número total de mutações criadas, quantas foram mortas, quantas são suspeitas e quantas sobreviveram.

## 7. Gerar Relatório do mutmut
Para visualizar o relatório gerado pelo mutmut em formato HTML, utilize o comando:

```bash
mutmut html
```

## 8. Seleção e Correção de Mutante
Com base no relatório de cobertura, selecione um arquivo com grande cobertura para analisar os mutantes. Neste exemplo, o arquivo grammar.py foi escolhido, onde o mutante 38, que modifica a operação de subtração de - para +, foi identificado como relevante.

### Novo Caso de Teste
Para matar esse mutante, foi desenvolvido um novo caso de teste que verifica a operação de subtração. O código abaixo é um exemplo de como o teste pode ser implementado:

```python
def test_subtraction_mutation(self):
        analyzer = Analyzer("10 - 5")
        result = analyzer.analyze()
        self.assertEqual(result, 5, f"Expected 5 but got {result}")
```

Após a adição desse teste, execute novamente o mutmut:

```bash
mutmut run --paths-to-mutate=path_do_projeto
```
Verifique os resultados para garantir que o mutante foi morto.

## 9. Conclusão
Após a reexecução do mutmut, o número de mutações sobreviventes deve diminuir, indicando que os novos testes estão mais eficazes.

Para mais detalhes e acesso ao código, consulte o repositório:

https://github.com/matheusteixeiradcompufs/Teste_Software_Mutantes_2024_teixeira_matheus
