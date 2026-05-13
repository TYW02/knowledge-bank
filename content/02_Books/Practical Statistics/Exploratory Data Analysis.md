





## Elements of Structured Data

Data comes from many sources: sensor measurements, events, text, images, and videos

- Data is often unstructured 
	- Images are a collection of pixels with each containing RGB information
	- Text are sequences of words and nonword characters.

A major challenge of data science is to harness raw data into actionable information.

- Unstructured raw data must be processed and manipulated into a structured form
	- One of the most common form of structured data is a table with rows and columns


### There are 2 basic types of structured data
1. Numeric data
	- Continuous (wind speed, time duration)
2. Categorical Data
	- Fixed set of values (Type of TV screen, State name)

Binary data is an important special case of categorical data that takes on only one of 2 values
- 0 / 1
- yes / no
- true / false




> [!Key Terms for Data Types]
> **Numeric**
> 		Data that are expressed on a numeric scale
> 		
> 	**Continuous**
> 			Data that can take on any value in an interval (Synonyms: interval, float, numeric)
> 			
> 	**Discrete**
> 			Data that can take on only integer values, such as counts. (Synonyms: integer, count)
> 			
> 	**Categorical**
> 			Data that can take on only a specific set of values representing a set of possible categories (Synonyms: enums, enumerated, factors, nominal)
> 			
> 		**Binary**
> 			A special case of categorical data with just two categories of values, e.g. 0/1, true/false. (Synonyms: dichotomous, logical, indicator, boolean)
> 			
> 		**Ordinal**
> 			Categorical data that has an explicit ordering. (Synonym: ordered factor)



> [!Key Ideas]
> - Data is typically classified in software by type.
> - Data types include numeric (continuous, discrete) and categorical (binary, ordinal)
> - Data typing in software acts as a signal to the software on how to process the data






# Rectangular Data

The typical frame of reference for an analysis in data science is a *rectangular data* object, like a spreadsheet or database table.

Rectangular data is the general term for a two-dimensional matrix with rows indicating records and columns indicating features
- Unstructured data must be processed and manipulated so that it can be represented as a set of features in the rectangular data


> [!Key Terms for Rectangular Data]
> **Data Frame**
> 	Rectangular data (like a spreadsheet) is the basic structure for statistical and machine learning models.
> 	
> **Feature**
> 	A column within a table is commonly referred to as a feature
> 	Synonyms
> 		attribute, input, predictor, variable
> 		
> **Outcome**
> 	Many data science projects involve predicting an outcome - often a yes/no outcome. The features are sometimes used to predict the outcome in an experiment or a study.
> 		Synonyms
> 			dependent variable, response, target, output
> 			
> **Records**
> 	A row within a table is commonly referred to as a record
> 	Synonyms
> 		case, example, instance, observation, pattern, sample



![[Pasted image 20250816125059.png]]

In Table 1-1, there is a mix of measured or counted data (e.g., duration and price) and categorical data (e.g., category and currency). As mentioned earlier, a special form of categorical variable is a binary (yes/no or 0/1) variable, seen in the rightmost column in Table 1-1
- This indicator variable also happens to be an outcome variable, when the scenario is to predict whether an auction is competitive or not.


# Data Frames and Indexes

Traditional database tables have one or more columns designated as an index, essentially a row number. This can vastly improve the efficiency of certain database queries. 
In Python, with the pandas library, the basic rectangular data structure is a DataFrame object.


# Nonrectangular Data Structures

There are other data structures besides rectangular data.

Time series data records successive measurements of the same variable. 
- It is the raw material for statistical forecasting methods, and it is also a key component of the data produced by devices - IoT

Spatial data structure, which are used in mapping and location analytics, are more complex and varied than rectangular data structures.
- In _object_ representation, the focus of data is an object (e.g. house) and its spatial coordinates.
- The _field_ view, by contrast, focuses on small units of space and the value of a relevant metric (pixel brightness, for example).

Graph (or network) data structure are used to represent physical, social, and abstract relationships.
- For Example, a graph of a social network, such as Facebook or LinkedIn, may represent connections between people on the network.
- Distribution hubs connected by roads are an example of a physical network.
- Graph structures are useful for certain types of problems, such as network optimization and recommender systems.

> [!KEY IDEAS]
> 
> - The basic structure in data science is a rectangular matrix in which rows are records and columns are variables (features).
> - Terminology can be confusing; there are a variety of synonyms arising from the different disciplines that contribute to data science (statistics, computer science, and information technology) 








































