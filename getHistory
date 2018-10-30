"""BeautifulSoup4 needs to be installed first if you're using Python 3.x. 
If you're using Python 2.x you can use the old BeautifulSoup"""

import urllib.request
from bs4 import BeautifulSoup
import numpy as np

def getHistory(stock):
    contents = urllib.request.urlopen("http://eoddata.com/stockquote/NASDAQ/"+stock+".htm").read()
    soup = BeautifulSoup(contents)
    
    """
    This is just a demo and gets you the latest 10 days' EOD prices for the specified stock symbol.
    If the market is open at the time that this program is run, the first row corresponds to the current prices.
    """
    
    data = []
    table = soup.find('table', attrs={'class':'quotes'})
    rows = table.find_all('tr')

    for row in rows:
        cols = row.find_all('td')
        cols = [ele.text.strip() for ele in cols]
        if len(cols)>0:
            data.append([ele for ele in cols if ele])
    
    dataNP = np.array(data)
    history = {
      "Open":dataNP[:,1],
      "High":dataNP[:,2],
      "Low":dataNP[:,3],
      "Close":dataNP[:,4],
      "Volume":dataNP[:,5]
    }
    return (history)

#Test
stockDetails = getHistory("AAPL")
print(stockDetails)
