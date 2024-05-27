# Sobre o código

Tive muita dificuldade em coletar dados do CECAD 2.0, por esse motivo, decidi criar um código que ficasse fazendo a consulta e coletando os dados, armazenando-os em um dataframe.

Para usar, é preciso passar a uf que te atende (`uf` = "AC - Acre") por exemplo, e na sequência uma lista de municípios na variável `municipios`, que no exemplo conta com os municípios do Acre.
No trecho de código a seguir é preciso passar as variáveis do recorte:
```
# Selecionar uma variável de coluna
    coluna_select = Select(driver.find_element(By.NAME, 'var1'))
    coluna_select.select_by_visible_text('Bloco 2 - Existência de banheiro')
    
    # Selecionar uma variável de linha
    linha_select = Select(driver.find_element(By.NAME, 'var2'))
    linha_select.select_by_visible_text('Bloco 8 - Função principal')
```

Além disso, também deixei dois exemplos de filtros possíveis:

```
# Selecionar os checkboxes de faixa de renda
checkbox_values_renda = ["1", "2", "3"]
for value in checkbox_values_renda:
    checkbox = driver.find_element(By.CSS_SELECTOR, f'input[name="filtros[fx_rfpc][]"][value="{value}"]')
    if not checkbox.is_selected():
        checkbox.click()

# Selecionar os checkboxes de faixa etária
checkbox_values_parentesco = ["11", "12"]
for value in checkbox_values_parentesco:
    checkbox = driver.find_element(By.CSS_SELECTOR, f'input[name="filtros[fx_idade][]"][value="{value}"]')
    if not checkbox.is_selected():
        checkbox.click()
```

O primeiro filtro seleciona os boxes 1, 2 e 3, indicando o seletor do filtro no `f'input[name="filtros[fx_rfpc][]"][value="{value}"]'` 
Já para o segundo, coloquei o filtro por idade `f'input[name="filtros[fx_idade][]"][value="{value}"`, selecionando os boxes 11 e 12.

Para adicionar mais filtros, basta copiar a estrutura e encontrar o "name=" do filtro que quiser aplicar.

```
Requisitos:

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import Select, WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.chrome.service import Service as ChromeService
from webdriver_manager.chrome import ChromeDriverManager
import pandas as pd

```

### Tratamento dos dados

O código conta com a função `convert_columns_to_float` que converte as colunas de valores para float.

```


# Arquivo auxiliar

Deixei um arquivo chamado `municipios.xlsx` para auxiliar com os nomes dos municípios de cada estado, para facilitar a coleta de dados. Além dos nomes, também tem o código IBGE para futuras análises ou cruzamento de dados. 

Também deixei um exemplo da saída no arquivo `dados/dados_raspados.xlsx` para que possa ver como os dados são armazenados.