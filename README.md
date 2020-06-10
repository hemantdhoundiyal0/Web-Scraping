# Web-Scraping
Here, I have scraped the one page of flipkart having t-shirts.

# lets scrape the filpkart data, only 1 page(having t-shirts ranging between rupees 1000-1500)

#importing the Necessary Libraries
import requests
from bs4 import BeautifulSoup
import pandas as pd

#using the requests library to get the source data
source_code=requests.get("https://www.flipkart.com/search?q=t+shirts&as=on&as-show=on&otracker=AS_Query_TrendingAutoSuggest_4_0_na_na_na&otracker1=AS_Query_TrendingAutoSuggest_4_0_na_na_na&as-pos=4&as-type=TRENDING&suggestionId=t+shirts&requestId=027015f7-10b4-47e3-b5df-c187eaa75d89&p%5B%5D=facets.price_range.from%3D1000&p%5B%5D=facets.price_range.to%3D1500").text
#print(source_code)

#lets use BeautifulSoup parser "lxml"
soup=BeautifulSoup(source_code,"lxml")
#print(soup.prettify())

# first examing the source code for one t-shirt only
#and pass it in a variable(i.e., 't-shirt')
t_shirt=soup.find('div',class_="IIdQZO _1SSAGr")
print(t_shirt.prettify())

#fetching some data for all t-shirts on 1st page
for article in soup.find_all('div',class_="IIdQZO _1SSAGr"):
    try:
        shirt_name=article.find('div',class_='_2B_pmu').text
        print("Shirt:", shirt_name)
        link= article.a["href"]
        #print(link)
        real_link=f"https://www.flipkart.com{link}"
        print("Link:", real_link)
        #shirt_title=tag.a.title.text
        price=article.find('div',class_="_1vC4OE").text
        print("Price:", price)
        off_perc=article.find('div',class_="VGWI6T").text
        print("Off_%:", off_perc)
        print()
    except:
        print("None")
        print()
        pass
    
    
