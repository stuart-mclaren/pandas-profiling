# Pandas Profiling

![Pandas Profiling Logo Header](https://pandas-profiling.ydata.ai/docs/assets/logo_header.png)

[![Build Status](https://github.com/ydataai/pandas-profiling/actions/workflows/tests.yml/badge.svg?branch=master)](https://github.com/ydataai/pandas-profiling/actions/workflows/tests.yml)
[![Code Coverage](https://codecov.io/gh/ydataai/pandas-profiling/branch/master/graph/badge.svg?token=gMptB4YUnF)](https://codecov.io/gh/ydataai/pandas-profiling)
[![Release Version](https://img.shields.io/github/release/ydataai/pandas-profiling.svg)](https://github.com/ydataai/pandas-profiling/releases)
[![Python Version](https://img.shields.io/pypi/pyversions/pandas-profiling)](https://pypi.org/project/pandas-profiling/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/python/black)


<p align="center">
  <a href="https://pandas-profiling.ydata.ai/docs/master/rtd/">Documentation</a>
  |
  <a href="https://slack.ydata.ai">Slack</a>
  | 
  <a href="https://stackoverflow.com/questions/tagged/pandas-profiling">Stack Overflow</a>
  |
  <a href="https://pandas-profiling.ydata.ai/docs/master/rtd/pages/changelog.html#changelog">Latest changelog</a>

</p>

Generates profile reports from a pandas `DataFrame`. 

The pandas `df.describe()` function is great but a little basic for serious exploratory data analysis. 
`pandas_profiling` extends the pandas DataFrame with `df.profile_report()` for quick data analysis.

For each column the following statistics - if relevant for the column type - are presented in an interactive HTML report:

* **Type inference**: detect the [types](#types) of columns in a dataframe.
* **Essentials**: type, unique values, missing values
* **Quantile statistics** like minimum value, Q1, median, Q3, maximum, range, interquartile range
* **Descriptive statistics** like mean, mode, standard deviation, sum, median absolute deviation, coefficient of variation, kurtosis, skewness
* **Most frequent values**
* **Histogram**
* **Correlations** highlighting of highly correlated variables, Spearman, Pearson and Kendall matrices
* **Missing values** matrix, count, heatmap and dendrogram of missing values
* **Text analysis** learn about categories (Uppercase, Space), scripts (Latin, Cyrillic) and blocks (ASCII) of text data.
* **File and Image analysis** extract file sizes, creation dates and dimensions and scan for truncated images or those containing EXIF information.

## Announcements

**Spark backend in progress**: We can happily announce that we're nearing v1 for the Spark backend for generating profile reports.
Beta testers wanted! The Spark backend will be released as a pre-release for this package.

**Monitoring time series?**: I'd like to draw your attention to [popmon](https://github.com/ing-bank/popmon). Whereas pandas-profiling allows you to explore patterns in a single dataset, popmon allows you to uncover temporal patterns. It's worth checking out!

---

_Contents:_ **[Examples](#examples)** |
**[Installation](#installation)** | **[Documentation](#documentation)** |
**[Large datasets](#large-datasets)** | **[Command line usage](#command-line-usage)** |
**[Advanced usage](#advanced-usage)** | **[Support](#support)** | **[Go beyond](#go-beyond)** |
**[Support the project](#supporting-open-source)** | **[Types](#types)** | **[How to contribute](#contributing)** |
**[Editor Integration](#editor-integration)** | **[Dependencies](#dependencies)**

---

## Examples

The following example reports showcase the potentialities of the package across a wide range of dataset and data types:

* [Census Income](https://pandas-profiling.ydata.ai/examples/master/census/census_report.html) (US Adult Census data relating income with other demographic properties)
* [NASA Meteorites](https://pandas-profiling.ydata.ai/examples/master/meteorites/meteorites_report.html) (comprehensive set of meteorite landing - object properties and locations) [![Open In Colab](https://camo.githubusercontent.com/52feade06f2fecbf006889a904d221e6a730c194/68747470733a2f2f636f6c61622e72657365617263682e676f6f676c652e636f6d2f6173736574732f636f6c61622d62616467652e737667)](https://colab.research.google.com/github/ydataai/pandas-profiling/blob/master/examples/meteorites/meteorites.ipynb) [![Binder](https://camo.githubusercontent.com/483bae47a175c24dfbfc57390edd8b6982ac5fb3/68747470733a2f2f6d7962696e6465722e6f72672f62616467655f6c6f676f2e737667)](https://mybinder.org/v2/gh/ydataai/pandas-profiling/master?filepath=examples%2Fmeteorites%2Fmeteorites.ipynb)
* [Titanic](https://pandas-profiling.ydata.ai/examples/master/titanic/titanic_report.html) (the "Wonderwall" of datasets) [![Open In Colab](https://camo.githubusercontent.com/52feade06f2fecbf006889a904d221e6a730c194/68747470733a2f2f636f6c61622e72657365617263682e676f6f676c652e636f6d2f6173736574732f636f6c61622d62616467652e737667)](https://colab.research.google.com/github/ydataai/pandas-profiling/blob/master/examples/titanic/titanic.ipynb) [![Binder](https://camo.githubusercontent.com/483bae47a175c24dfbfc57390edd8b6982ac5fb3/68747470733a2f2f6d7962696e6465722e6f72672f62616467655f6c6f676f2e737667)](https://mybinder.org/v2/gh/ydataai/pandas-profiling/master?filepath=examples%2Ftitanic%2Ftitanic.ipynb)
* [NZA](https://pandas-profiling.ydata.ai/examples/master/nza/nza_report.html) (open data from the Dutch Healthcare Authority)
* [Stata Auto](https://pandas-profiling.ydata.ai/examples/master/stata_auto/stata_auto_report.html) (1978 Automobile data)
* [Colors](https://pandas-profiling.ydata.ai/examples/master/colors/colors_report.html) (a simple colors dataset)
* [Vektis](https://pandas-profiling.ydata.ai/examples/master/vektis/vektis_report.html) (Vektis Dutch Healthcare data)
* [UCI Bank Dataset](https://pandas-profiling.ydata.ai/examples/master/bank_marketing_data/uci_bank_marketing_report.html) (marketing dataset from a bank)
* [Russian Vocabulary](https://pandas-profiling.ydata.ai/examples/master/features/russian_vocabulary.html) (100 most common Russian words, showcasing unicode text analysis)
* [Website Inaccessibility](https://pandas-profiling.ydata.ai/examples/master/features/website_inaccessibility_report.html) (website accessibility analysis, showcasing support for URL data)
* [Orange prices](https://pandas-profiling.ydata.ai/examples/master/features/united_report.html) and [Coal prices](https://pandas-profiling.ydata.ai/examples/master/features/flatly_report.html) (simple pricing evolution datasets, showcasing the theming options)

Tutorials:

* [Tutorial: report structure using Kaggle data (advanced)](https://github.com/ydataai/pandas-profiling/blob/develop/examples/tutorials/modify_report_structure.ipynb) (modify the report's structure) [![Open In Colab](https://camo.githubusercontent.com/52feade06f2fecbf006889a904d221e6a730c194/68747470733a2f2f636f6c61622e72657365617263682e676f6f676c652e636f6d2f6173736574732f636f6c61622d62616467652e737667)](https://colab.research.google.com/github/ydataai/pandas-profiling/blob/master/examples/tutorials/modify_report_structure.ipynb) [![Binder](https://camo.githubusercontent.com/483bae47a175c24dfbfc57390edd8b6982ac5fb3/68747470733a2f2f6d7962696e6465722e6f72672f62616467655f6c6f676f2e737667)](https://mybinder.org/v2/gh/ydataai/pandas-profiling/master?filepath=examples%2Ftutorials%2Fmodify_report_structure.ipynb)


## Installation

### Using pip

[![PyPi Downloads](https://pepy.tech/badge/pandas-profiling)](https://pepy.tech/project/pandas-profiling)
[![PyPi Monthly Downloads](https://pepy.tech/badge/pandas-profiling/month)](https://pepy.tech/project/pandas-profiling/month)
[![PyPi Version](https://badge.fury.io/py/pandas-profiling.svg)](https://pypi.org/project/pandas-profiling/)

You can install using the pip package manager by running

```sh
pip install pandas-profiling[notebook]
```

Alternatively, you could install the latest version directly from Github:

```sh
pip install https://github.com/ydataai/pandas-profiling/archive/master.zip
```    
    
### Using conda

[![Conda Downloads](https://img.shields.io/conda/dn/conda-forge/pandas-profiling.svg)](https://anaconda.org/conda-forge/pandas-profiling)
[![Conda Version](https://img.shields.io/conda/vn/conda-forge/pandas-profiling.svg)](https://anaconda.org/conda-forge/pandas-profiling) 
 
You can install using the conda package manager by running

```sh
conda install -c conda-forge pandas-profiling
```

### From source

Download the source code by cloning the repository or by pressing ['Download ZIP'](https://github.com/ydataai/pandas-profiling/archive/master.zip) on this page. 

Install by navigating to the proper directory and running:

```sh
python setup.py install
```

## Documentation

The documentation for `pandas_profiling` can be found [here](https://pandas-profiling.ydata.ai/docs/master/rtd/). Previous documentation is still available [here](https://pandas-profiling.ydata.ai/docs/master/).

### Getting started

Start by loading in your pandas DataFrame, e.g. by using:

```python
import numpy as np
import pandas as pd
from pandas_profiling import ProfileReport

df = pd.DataFrame(np.random.rand(100, 5), columns=["a", "b", "c", "d", "e"])
```
To generate the report, run:
```python
profile = ProfileReport(df, title="Pandas Profiling Report")
```

### Explore deeper

You can configure the profile report in any way you like. The example code below loads the explorative configuration, that includes many features for text (length distribution, unicode information), files (file size, creation time) and images (dimensions, exif information). If you are interested what exact settings were used, you can compare with the [default configuration file](https://github.com/ydataai/pandas-profiling/blob/master/src/pandas_profiling/config_default.yaml).

```python
profile = ProfileReport(df, title="Pandas Profiling Report", explorative=True)
```

Learn more about configuring `pandas-profiling` on the [Advanced usage](https://pandas-profiling.ydata.ai/docs/master/rtd/pages/advanced_usage.html) page.

#### Jupyter Notebook

We recommend generating reports interactively by using the Jupyter notebook. 
There are two interfaces (see animations below): through widgets and through a HTML report.

<img alt="Notebook Widgets" src="https://pandas-profiling.ydata.ai/docs/master/assets/widgets.gif" width="800" />

This is achieved by simply displaying the report. In the Jupyter Notebook, run:

```python
profile.to_widgets()
```

The HTML report can be included in a Jupyter notebook:

<img alt="HTML" src="https://pandas-profiling.ydata.ai/docs/master/assets/iframe.gif" width="800" />

Run the following code:

```python
profile.to_notebook_iframe()
```

#### Saving the report

If you want to generate a HTML report file, save the `ProfileReport` to an object and use the `to_file()` function:
```python
profile.to_file("your_report.html")
```

Alternatively, you can obtain the data as JSON:
```python
# As a string
json_data = profile.to_json()

# As a file
profile.to_file("your_report.json")
```

### Large datasets

Version 2.4 introduces minimal mode. 

This is a default configuration that disables expensive computations (such as correlations and duplicate row detection).

Use the following syntax:

```python
profile = ProfileReport(large_dataset, minimal=True)
profile.to_file("output.html")
```

Benchmarks are available [here](https://pandas-profiling.ydata.ai/dev/bench/).

### Command line usage

For standard formatted CSV files that can be read immediately by pandas, you can use the `pandas_profiling` executable. 

Run the following for information about options and arguments.

```sh
pandas_profiling -h
```

### Advanced usage

A set of options is available in order to adapt the report generated.

* `title` (`str`): Title for the report ('Pandas Profiling Report' by default).
* `pool_size` (`int`): Number of workers in thread pool. When set to zero, it is set to the number of CPUs available (0 by default).
* `progress_bar` (`bool`): If True, `pandas-profiling` will display a progress bar.
* `infer_dtypes` (`bool`): When `True` (default) the `dtype` of variables are inferred using `visions` using the typeset logic (for instance a column that has integers stored as string will be analyzed as if being numeric).

More settings can be found in the [default configuration file](https://github.com/ydataai/pandas-profiling/blob/master/src/pandas_profiling/config_default.yaml) and [minimal configuration file](https://github.com/ydataai/pandas-profiling/blob/master/src/pandas_profiling/config_minimal.yaml).

You find the configuration docs on the advanced usage page [here](https://pandas-profiling.ydata.ai/docs/master/rtd/pages/advanced_usage.html)

**Example**
```python
profile = df.profile_report(
    title="Pandas Profiling Report", plot={"histogram": {"bins": 8}}
)
profile.to_file("output.html")
```

## Support
Need help? Want to share a perspective? Want to report a bug? Ideas for collaboration? 
You can reach out via the following channels:

- [Stack Overflow](https://stackoverflow.com/questions/tagged/pandas-profiling): ideal for asking questions on how to use the package
- [Github Issues](https://github.com/ydataai/pandas-profiling/issues): bugs, proposals for change, feature requests
- [Slack](https://slack.ydata.ai): general chat, questions, collaboration
- [Email](mailto:developers@ydata.ai): project collaboration or sponsoring

## Go beyond

### Popmon

<table>
<tr>
<td>

<a href="https://github.com/ing-bank/popmon">
	<img alt="Popmon" src="https://raw.githubusercontent.com/ing-bank/popmon/master/docs/source/assets/popmon-logo.png" width="900" />
</a>
	
</td>
<td>

For many real-world problems we are interested how the data changes over time. 
The excellent package `popmon` allows you to profile and monitor data trends over time and generates reports in a similar fashion as you're used to using pandas-profiling.
Inspecting the report often shows patterns that are going by undetected during standard data exploration.
Moreover, popmon can be used to monitor the stability of input and output of machine learning models.
The package is fully open-source and you can find it [here](https://github.com/ing-bank/popmon)! 

To learn more on Popmon, have a look at these resources [here](https://github.com/ing-bank/popmon#resources)

</td>
</tr>
</table>


### Great Expectations

<table>
<tr>
<td>

<a href="https://www.greatexpectations.io">
<img alt="Great Expectations" src="https://github.com/great-expectations/great_expectations/raw/develop/generic_dickens_protagonist.png" width="900" />
</a>
	
</td>
<td>

Profiling your data is closely related to data validation: often validation rules are defined in terms of well-known statistics.
For that purpose, `pandas-profiling` integrates with [Great Expectations](https://www.greatexpectations.io). 
This a world-class open-source library that helps you to maintain data quality and improve communication about data between teams.
Great Expectations allows you to create Expectations (which are basically unit tests for your data) and Data Docs (conveniently shareable HTML data reports).
`pandas-profiling` features a method to create a suite of Expectations based on the results of your ProfileReport, which you can store, and use to validate another (or future) dataset.

You can find more details on the Great Expectations integration [here](https://pandas-profiling.ydata.ai/docs/master/rtd/pages/great_expectations_integration.html)

</td>
</tr>
</table>

## Types

Types are a powerful abstraction for effective data analysis, that goes beyond the logical data types (integer, float etc.).
`pandas-profiling` currently, recognizes the following types: _Boolean, Numerical, Date, Categorical, URL, Path, File_ and _Image_.

We have developed a type system for Python, tailored for data analysis: [visions](https://github.com/dylan-profiler/visions).
Choosing an appropriate typeset can both improve the overall expressiveness and reduce the complexity of your analysis/code.
To learn more about `pandas-profiling`'s type system, check out the default implementation [here](https://github.com/ydataai/pandas-profiling/blob/develop/src/pandas_profiling/model/typeset.py).
In the meantime, user customized summarizations and type definitions are now fully supported - if you have a specific use-case please reach out with ideas or a PR!

## Contributing

Read on getting involved in the [Contribution Guide](https://pandas-profiling.ydata.ai/docs/master/rtd/pages/contribution_guidelines.html).

A low threshold place to ask questions or start contributing is by reaching out on the pandas-profiling Slack. [Join the Slack community](https://slack.ydata.ai).

## Editor integration

### PyCharm integration 

1. Install `pandas-profiling` via the instructions above
2. Locate your `pandas-profiling` executable.
    - On macOS / Linux / BSD:
        ```sh
        $ which pandas_profiling
        (example) /usr/local/bin/pandas_profiling
        ```
    - On Windows:
        ```console
        $ where pandas_profiling
        (example) C:\ProgramData\Anaconda3\Scripts\pandas_profiling.exe
        ```
3. In PyCharm, go to _Settings_ (or _Preferences_ on macOS) > _Tools_ > _External tools_
4. Click the _+_ icon to add a new external tool
5. Insert the following values
	- Name: Pandas Profiling
    - Program: _**The location obtained in step 2**_
    - Arguments: `"$FilePath$" "$FileDir$/$FileNameWithoutAllExtensions$_report.html"`
    - Working Directory: `$ProjectFileDir$`
  
<img alt="PyCharm Integration" src="https://pandas-profiling.ydata.ai/docs/assets/pycharm-integration.png" width="400" />
  
To use the PyCharm Integration, right click on any dataset file:

_External Tools_ > _Pandas Profiling_.

### Other integrations

Other editor integrations may be contributed via pull requests.

## Dependencies

The profile report is written in HTML and CSS, which means `pandas-profiling` requires a modern browser. 

You need [Python 3](https://python3statement.org/) to run this package. Other dependencies can be found in the requirements files:

| Filename | Requirements|
|----------|-------------|
| [requirements.txt](https://github.com/ydataai/pandas-profiling/blob/master/requirements.txt) | Package requirements|
| [requirements-dev.txt](https://github.com/ydataai/pandas-profiling/blob/master/requirements-dev.txt)  |  Requirements for development|
| [requirements-test.txt](https://github.com/ydataai/pandas-profiling/blob/master/requirements-test.txt) | Requirements for testing|
| [setup.py](https://github.com/ydataai/pandas-profiling/blob/master/setup.py) | Requirements for Widgets etc. |
