## This can be your internal website page / project page

**Project description:** Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

### 1. Suggest hypotheses about the causes of observed phenomena

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

```python
#importing
from bs4 import BeautifulSoup
import requests
import pandas as pd
#Here I chose the first 6 pages
pages = ["http://books.toscrape.com/",
         "http://books.toscrape.com/catalogue/page-2.html",
         "http://books.toscrape.com/catalogue/page-3.html",
         "http://books.toscrape.com/catalogue/page-4.html",
         "http://books.toscrape.com/catalogue/page-5.html",
         "http://books.toscrape.com/catalogue/page-6.html"]
prices=[]
products=[]
ratings=[]
ident=[]
r=[]
#parsing
for i in pages:
    page = requests.get(i)
    soup = BeautifulSoup(page.content, 'html.parser')
 
#class is 'col-xs-6 col-sm-4 col-md-3 col-lg-3'
#Now, we can use the find_all method to search for items by class 
#In our case, we are looking for all li elements with this specific class.
#after that, we can find specific objects by specifing the tag or class, and then use get text to get the price and name. 
#for the rating I just used p['class'] since the rating was the class already, however it included the string 'star rating' so 
#I removed that with strip, it also had the numbers worded so I had to convert the words into integers using if statements

    for a in soup.find_all('li', class_='col-xs-6 col-sm-4 col-md-3 col-lg-3'):
        product_price=a.find(class_="price_color")
        product_name=a.find('h3')
        product_rating=a.p['class']
        #print(product_rating)
        price=product_price.get_text().strip().strip('Â£')
        name=product_name.get_text()
        #rating=product_rating.strip().strip('star rating')
        #print(rating)
        prices.append(price)
        products.append(name)
        ratings.append(product_rating)
    
for i in range(0, len(prices)):
	ident.append(i)
#since ratings had lists within lists 
for i in range(0, len(ratings)):
    r.append(ratings[i][1])

for i in range(0, len(ratings)):
    if r[i]=='One':
        r[i]=1
    elif r[i]=='Two':
        r[i]=2
    elif r[i]=='Three':
        r[i]=3
    elif r[i]=='Four':
        r[i]=4
    elif r[i]=='Five':
        r[i]=5

df = pd.DataFrame({'id':ident,'Product Name':products,'Price':prices, 'Rating':r}) 
df.to_csv('all.csv', index=False, encoding='utf-8')

```

### 2. Assess assumptions on which statistical inference will be based

```javascript
if (isAwesome){
  return true
}
```

### 3. Support the selection of appropriate statistical tools and techniques

<img src="images/Figure_1.png"/>
<img src="images/Figure_2.png"/>
<img src="images/Figure_3.png"/>

### 4. Provide a basis for further data collection through surveys or experiments

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
