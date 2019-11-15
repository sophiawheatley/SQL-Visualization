# SQL-Visualization: declarative visualization language, based on SQL syntax

In our experience, visualization tools are either:

- Too specific, i.e. there is no application agnostic declarative visualization language (to our knowledge).
- Too verbose, i.e. a lot of boilerplate text is needed to create a simple plot.
- Too technical, i.e. knowledge about the inner workings of the tool is required.

In response to this, we envision that a well-adopted declarative visualization language could provide a convenient way of creating and sharing visualizations.
With the further benefit of decoupling the language and the underlying plotting-tool.

The following two ideas form the core of our approach:
- SQL syntax: We choose to adopt and adapt the SQL syntax for our visualization language. This is because, the SQL syntax is well known to both developers as well as non-developers (fast adoption), and allows for advanced data querying (see following bullet point).
- Coupling of visualization and data (querying): Preparing the data for the visualization, e.g. calculating statistics, is an integral part of creating visualizations. Thus, we think it is a benefit if the language supports sophisticated data analysis. The benefit is improved usability and portability.

As a prototype, we adapt the SQL language by attaching meaning to the naming convention of column names of the resulting table. By
 resulting table we mean the table generated by the SQL query, together with the assigned column names thereof.

For example, if declaring a (2-dimensional) scatter plot, we need to define what are the x-values and what are the y-values.
Each row of the resulting table will represent a data point in the final plot, and each data point consists of an x-value and a y-value.
This can be achieved by assigning one column to hold the x-values, and one column the y-values.

In our prototypical implementation, this is done by assigning the x-value column the name 'x', and the y-value column the name 'y'.
Further, declaring the plot to be a scatterplot, is done by assigning the value scatterplot as column 'plottype' (for each data record; this is perhaps an odd way of assigning a value that is not relevant to individual data records).
Even further, if we would like to separate the data points between groups (hue), the group identifier of each record is assigned to the column by name 'group'.
This example is highlighted in the following SQL-code snippet.

```
# Example 1: query that plots (scatterplot) the relation of age and weight for men versus women, labelling the x and y axis with corresponding labels
# data = [
#   {'age': 20, 'weight': 82, 'sex': 'm' },
#   {'age': 21, 'weight': 72, 'sex': 'f' },
#   {'age': 40, 'weight': 86, 'sex': 'm' },
#   {'age': 37, 'weight': 75, 'sex': 'f' },
# ]

SELECT
    age AS 'x',
    weight AS 'y',
    sex AS 'group',
    'scatterplot' AS 'plottype',
    'age' AS 'xlabel',
    'weight' AS 'ylabel'
FROM
    data
```

The implementation (see SQL-Visualization.ipynb), extracts the relevant plot-metadata from the results table, this includes the plottype, xlabel and ylabel.
The metadata is used to find the correct plot-method (scatterplot), as well as applying the correct decorating functions (xlabel, ylabel, etc.).
The remaining columns are then applied to the plot-method (x, y, group).
The application relies on existing technologies and tries to mirror the terminology and structure of existing plotting tools (matplotlib etc.) and data analysis tools (SQL, pandas, etc.).

The prototypical implementation shows that this approach is possible.
Future challenges involve:
further developing and adapt the language to the likes of the users;
make a robust underlying engine that produces beautiful (beautiful is inevitably subjective) plots based on SQL-Visualization query inputs.
It remains a difficult task.

## Definitions:
- **Declarative:**
Declarative languages describe the desired results, and not the steps that cause the results
[wikipedia](https://en.wikipedia.org/wiki/Declarative_programming)

- **Visualization:**
Visual representation of data (scientific visualization)
[wikipedia](https://en.wikipedia.org/wiki/Visualization_\(graphics\))

- **SQL syntax:**
Structured Query Language, commonly used for managing data in Database Management Systems. SQL syntax refers to the grammartical structure of the SQL language.
[wikipedia](https://en.wikipedia.org/wiki/SQL)
