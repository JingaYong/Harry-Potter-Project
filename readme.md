# Harry Potter Characters Relationship Networking
Project Idea - Thu Vu Data Analytics.
#### In this projects we will basically be focusing concepts related to web scrapping and network analysis.

## Data Mining and Cleaning
### Import Libraries
First we will be importing the libraries.\
We will be using selenium for web scrapping in thsi project, other options beautiful soap, scrapy(for large projects)
* Selenium WebDriver is a web framework that permits you to execute cross-browser tests. This tool is used for automating web-based application testing to verify that it performs expectedly.
* webdriver_manager - is reuired to install the ChromeDriverManager(), which is used to open the chrome app
#
###### Jump to Web Scrapping Part 2 incase you are trying to execute this project
### Web Scrapping 
* The interesting part, we specify the url from which we would like to scrape content, and suggest the driver to open it.
* Next after the inspecting the web page I identified that the webpage had the characters seperated in different web pages alphabetical.
* So I created a list of links for each alphabet.
* Next we get the elements(character names) by the itemprop of the span tags and their respective description by the class name of the div tag. For this we first inspect the web page to identify the any specific identifier to get the elements. Add the character name along with its respective desciption into a description. Then we convert it into dataframe, which will be helpful in further cleaning and wrangling.

### Data Preprocessing
###### import re #(regex-regular expressions)
* First I create a sepearate column to strore the bracketed info from the character name, and removed it from the character name
* Next I removed rows without descriptions
* Then dropped duplicate rows
* Next I dropped rows, where the character name had more than 4 elements or the starting alphabet was lower
* Then I did a few modifications for character names containing the/The
* After all this I gave up, because I thought of a better approach, a more simple one to be honest

### Web Scrapping Part-2
* Here I used a web page with that contained a limited number of character
* I used the google search and another website

### Data Preprocessing Part-2
* After getting the character names, I added both the list contents
* Removed duplicates
* Converted the list into a dataframe
* Created a new column called firstname for the character's firstname
* Finally, saved the dataframe into a csv file


## Extracting the relationships among the characters

### Import Libraries
* spacy - this is required to handle text data
* networkx - 
* pyvis - 

### Load the books
* Get all the books(.txt files)
* We will be using the first book to demonstrate the network analysis of the characters
* Next I have read the first book, and used the spacy lib to remove informities from the book's text

### Getting the entities of each sentence in the book
* We iterate through the entire book and append a dictionary containing the sentence and a list of its entities to an outer list
* Next we filter the entity list by removing entities that are not character names 

### Creating the relationship
* We take a window size, which basically means the number of sentences we take to consider a relationship among characters. 
* If 2 characters appear within the the range of the window size implies, they have a relation.
* For ex - window size = 5, this implies if 2 character names appear in the range of 5 sentences
* If you didn't understand the above explanation - Listen
* We add the entities' list for every 5(window size) sentences in the se_df(dataframe), therefore the entities within the added list(char_list) have relations with each other.
* Next we need to remove duplicates from the added list(char_list), because a character cannot have a relation with themselves.
* After that we create dictionaries for each element in the char_unique list, where they are the source and the characters ahead are their respective targets.
* We append each dictionary to an outer list
* Finally convert the list into a dataframe

### Organising the relations
* First we rearrange the source and target alphabetically
* ex - Source=Harry Potter Target=Hedwig ; Source=Hedwig Target=Harry Potter ; These two mean the same, thus we need to convert all such rows to a single form
* Therefore we sort the values column wise meaning in the above example,  Source=Hedwig Target=Harry Potter => Source=Harry Potter Target=Hedwig
* Next we add a new column to the sorted dataframe, giving it a default value of 1
* Next we add the weights by grouping similar rows, thus getting the weightage of each relationship.

### Creating the Graph
* We use the networkx lib, and the give the relations dataframe, with the column names for the respective arguments, and create the graph
* We need to import scipy to run this part
* We chose a network positions layout, and draw the network structure of the relations among the characters, where each node represents a character and the line joining the nodes their relationship.
* But this is not an interactive network graph, rather a static image.

### Interactive Network Analysis
* Here we use the network module of the pyvis lib
* Initialize a Network variable with the appropriate arguments
* Customizing the node size based on the degree(node size increases with more relations, the degree is the angle between each relation)

### Calculating centrality parameters of the network graph
* Degree Centrality, and their respective plots
* Closeness Centrality, and their respective plots
* Betweenness Centrality, and their respective plots

### Creating communities from relations network(by assigning different colors to each community)
###### import community as community_louvain
* create communities by partitioning the graph

### Lastly we check the timeline of the character relevance/adaptability throughout the series of books
* Perform all the steps from the reading each book to prepare graphs for each book's sentences' entities' relations
* Then calculate the degree centrality of each graph
* Finally plot the graph of the characters you wish to visualize their character development through all the books


## I would like to thank Thu Vu Ma'am for introducing this concept of network analysis.
