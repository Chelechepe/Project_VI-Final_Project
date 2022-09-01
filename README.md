#

# Project_IV-Final_Project

##  Time series exploration 📈 Crypto Price
### By: Edgard Cuadra
### Date: September 1st 2022

#

![local_picture](./Images/altcoins.jpg)

#
## Hypothesis:
#

Using Data Analitics can we find potential altcoins that have the condition or potential to generate significant returns by their unique characteristics. can we create a predictive model that can generate a moderate prediction for future investments?

#

### Get Started with Web Scrapping:
<br/>

For the project ill be extracting the list of all crypto currencies list from the we page listed in the URL = "https://coinmarketcap.com/"
<br/>

We need web page number of page to be added in the url by using the parameter for the url "/?page=3" since the web page only displays 100 coins per page.
<br/>

By using Selenium we can create a bot that will scroll thought the dynamic page (meaning it loads information while you scroll the page, otherwise it wont give you all the pages information) in order to do this we need to make a loop so that we can perform the same task in all the web pages that have information of value. we will only do this for the first 30 pages out of 97. this is because we are only interested in coins that have a market capital (meaning that a significant investment of money is already in capital of said coin).

<br/>

Code for web scrapping and scrolling selenium:

    current_scroll_position, new_height= 0, 1
    while current_scroll_position <= new_height:
    current_scroll_position += 8
    driver.execute_script("window.scrollTo(0, {});".format(current_scroll_position))
    new_height = driver.execute_script("return document.body.scrollHeight")

    html = driver.execute_script("return document.body.outerHTML;")

Example of what the bot does:
<br/>

![local_picture](./Images/Selenium_bot_WS.gif)

<br/>

Following the extraction of the html with selenium, we need to determine what we want to extract, in this case we can start by gettin the coins name, ticker, market capital, supply and current price. we do this by ispecting the html of the web page and finding the tag of the desired information once we have this we can use Beautiful soup (BS4) to jsonify the html and be able to locate the text and save it into a list  
<br/>

Example of browser html inspect for info:
<br/>

![local_picture](./Images/inspect_html.jpg)
<br/>

Once the information has been extracted and cleaned the text to only have the desired information we temporarly store each colum in a list. meaning that we will have to convert them into a data frame using command for zip list, followed by pandas.dataframe to create a table as following:
<br/>

![local_picture](./Images/sample_cryptolist.jpg)

<br/>

As a result we now have a list of 3000 coins, but how do we determin which ones are the ones we are most interested in and will be using for our analisis?
<br/>

In order to do this we will need to calculate some field to further filter the coins that are of no use to us. 
<br/>

To get started we need to get familiar with some concepts: 

    Market Capital = Money invested in one coin
    Global Market Capital = Amount of money in all crypto
    Circulating supply = Amount of existing coin
    Price = Market Capital / Circulating Supply
<br/>


Knowing this we can use the mathematical rule of three to find out how mucha market capital needs to move in order to get a coin to a specific value. in our particular case we want marginal prices that can spike to the amount of $1. so we create set colum to value $1 and create a column with the new market capital.
<br/>

now that we have a new market capital, it would be best to create a column with the variation of price between the inicial market capital and the new market capital. as a compliment we can add two columns that will tell us the proportion of the new and old market capital represents of the global market capital.
<br/>

Given this information we can start filtering our 3000 coins and narrowing it down to a more sizable sample to explore and predict.
<br/>

We want coins who's:
<br/>

    Price < $1
    Market Capital > $10,000,000.00
    Propotion to Global Market Capital <= 1%
    Variation between new and old market cap <= 1000
<br/>

Afte we apply this filters we get as a result a list of 387 coins, we can now use wisualization tools to examin any particular tendency and behaviour that can be of our interest so that we can futher filter this list to 10 to 20 coins in which we can invest.


#
## Visualization and Storytelling:
#

https://public.tableau.com/app/profile/edgard.cuadra/viz/AltCoins_16617715752970/Alt_coinDash?publish=yes
<br/>

![local_picture](./Images/tableau_before.jpg)
<br/>

![local_picture](./Images/tableau_after.jpg)
<br/>

#
## Predictive Model and Stacionality:
#


#
## Conclusion and Recomendations:
#