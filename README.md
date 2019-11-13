# SQL-Visualization: declarative visualization language, based on SQL syntax

<!-- Why -->
In our experience, current visualization tools are either:

- Too specific, i.e. there is (to our knowledge) no application agnostic declarative visualization language.
- Too verbose, i.e. a lot of boilerplate text is needed to create a simple plot.
- Too technical, i.e. knowledge about the inner workings of the tool is required

In response to this, we envision that a well-adopted declarative visualization language could provide a convenient way of creating and sharing visualizations.
With the further benefit of decoupling the language from the underlying plotting-tool.

<!-- What -->
The following two ideas form the core of our approach:
- SQL syntax: We choose to adopt and adapt the SQL syntax for our visualization language. This because, the SQL syntax is well known to both developers as well as non-developers (thus easy adoption), and because, the SQL syntax allows for advanced data querying (see following bullet point)
- Coupling of visualization and data (querying): Preparing the data for the visualization, e.g. calculating statistics, is an integral part of creating visualizations. Thus, we think it is a benefit if the language supports sophisticated data analysis, in order to make it portable.

<!-- How -->


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
