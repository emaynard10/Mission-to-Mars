# Mission-to-Mars
![marsjumbo](https://user-images.githubusercontent.com/99676466/175110874-b8a89197-0948-4940-9188-f8b1a0361394.jpeg)

Created a web application with data scraped from various websites presented on an html file.

### Tools: 
Jupyter Notebooks, Beautiful Soup, Splinter, MongoDB, Pandas

### Scraping
The code scrapes the [NASA Mars News](https://redplanetscience.com/) website to get the most recently posted news article and it's descriptive paragraph. This was done by parsing the html with Beautiful Soup.
~~~ 
html = browser.html
news_soup = soup(html, 'html.parser')
slide_elem = news_soup.select_one('div.list_text') 
~~~ 
Next it vists and scrapes the Jet Propulsion Laboratory's [Space Images](https://spaceimages-mars.com/) webpage to gather the featured image for display on the webpage. In order to collect the full size image, I used the following code:
~~~ 
full_image_elem = browser.find_by_tag('button')[1]
full_image_elem.click()~~~ to navigate to a link. 
~~~
In order to list some information about Mars, I visited a [Mars Facts](https://galaxyfacts-mars.com) page and used Pandas to convert the information into a dataframe comparing those facts with Earth: 
~~~
df = pd.read_html('https://galaxyfacts-mars.com')[0]
df.columns=['description', 'Mars', 'Earth']
df.set_index('description', inplace=True)
~~~

![Screen Shot 2022-06-22 at 1 02 22 PM](https://user-images.githubusercontent.com/99676466/175116073-f611a607-85ce-4d5c-b3f0-227fac51a50b.png)

In order to retrieve the full resolution images of the four Mars hemispheres, I visted [Mars Hemisheres](https://marshemispheres.com/) webpage; by clicking on each thumbnail image the full resolution image is displayed. With an empty list to store the images and their titles as a dictionary, I used a for loop to iterate through the four thumbnails. After checking this code all worked in jupyter notebook, I download the code as a python file and continued in VS Code by creating functions, linking the scraping.py file to an app.py to run the website through Flask, and creating an HTML file to display the information. To style the html, I used Bootstrap.

PyMongo was used to establish a connection with MongoDB in order to keep the results in a database. The code renders the HTML file with the records in the database. The page includes a button to 'scrape new data' to get the most up to date images and news articles. 

