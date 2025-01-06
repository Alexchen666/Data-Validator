# Data-Validator
A user-friendly, interactive, UI-based data validation tool built with Marimo and Patito. Define your data validation rules using familiar Pydantic syntax and get instant feedback on your CSV data quality.

## Features

* Interactive web interface powered by Marimo notebooks
* Define column constraints using UI or intuitive Pydantic-style syntax
* Validate multiple aspects of your data:
  * Data types (string, integer, float, categorical, etc.)
  * Value ranges (min/max)
  * Missing values handling
  * Custom validation rules
* Comprehensive validation report generation
* Real-time feedback on validation results

## Installation

1. Clone the repo.
2. Create a Python environment as specified in `pyproject.toml`.
3. Execute `data_validator.py` using `marimo run data_validator.py`.

## Quick Start

1. Launch the validator using `marimo run data_validator.py`.
2. Upload your CSV file through the interface.
3. Define your validation rules using UI or Pydantic syntax:

```python
# the example is based on test_data.csv

class P(pt.Model):
    ID: int = pt.Field(unique=True)
    Species: Literal['Gentoo penguin (Pygoscelis papua)', 
                     'Adelie Penguin (Pygoscelis adeliae)', 
                     'Chinstrap penguin (Pygoscelis antarctica)']
    Island: Literal['Torgersen', 'Biscoe', 'Dream']
    Clutch_Completion: Literal['Yes', 'No']
    Culmen_Length: float = pt.Field(constraints=[pl.col('Culmen_Length') > pl.col('Culmen_Depth'),
                                                 pl.col('Body_Mass') > pl.col('Culmen_Length')])
    Culmen_Depth: float
    Flipper_Length: int
    Body_Mass: int
    Sex: Literal['MALE', 'FEMALE']
    Comments: Optional[str]
    Island_Code: int
```

4. Run the validation and view the results

## Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Note
This is an early-stage side project and the API may change. Please report any bugs or feature requests through the GitHub issues page.

## Source of `test_data.csv`

https://github.com/allisonhorst/palmerpenguins/tree/main

https://www.kaggle.com/datasets/parulpandey/palmer-archipelago-antarctica-penguin-data

Gorman KB, Williams TD, Fraser WR (2014). Ecological sexual dimorphism and environmental variability within a community of Antarctic penguins (genus Pygoscelis). PLoS ONE 9(3):e90081. https://doi.org/10.1371/journal.pone.0090081
