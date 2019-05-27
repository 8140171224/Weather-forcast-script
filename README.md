# Weather-forcast-script
create  in csv file

## error free 

# IMPORTING important module

    import pandas as pd
    import requests
    from bs4 import BeautifulSoup
    
# TRY for error free environment

    try :
        # past here your link 
        page = requests.get('https://forecast.weather.gov/MapClick.php?lat=34.05349000000007&lon=-118.24531999999999')
        soup = BeautifulSoup(page.content, 'html.parser')
        week= soup.find(id="seven-day-forecast-body")

        items = week.find_all(class_="tombstone-container")
        #print(items[0])

        print(items[0].find(class_="period-name").get_text())
        print(items[0].find(class_="short-desc").get_text())
        print(items[0].find(class_="temp").get_text())

        period_names = [item.find(class_="period-name").get_text() for item in items]
        #print(period_names)

        short_descriptions = [item.find(class_="short-desc").get_text() for item in items]
        #print(short_descriptions)

        temperature = [item.find(class_="temp").get_text() for item in items]
        #print(temperature)

        wether_stuff = pd.DataFrame(
            {'period': period_names,
             'short_descriptions': short_descriptions,
              'temperature': temperature,
            }
        )
        print(wether_stuff)
        wether_stuff.to_csv('first.csv')
    except :

    print("https://forecast.weather.gov \n \n      go there select your location and past url.")
    
    
    
    
    
# Information

## BY aakash padhiyar

## 8140171224
