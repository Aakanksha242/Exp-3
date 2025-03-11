import requests
from bs4 import BeautifulSoup

def get_bbc_headlines():
    url = "https://www.bbc.com/news"  # BBC News homepage
    response = requests.get(url)
    
    if response.status_code != 200:
        print("Failed to retrieve the web page.")
        return

    soup = BeautifulSoup(response.text, 'html.parser')

    # Find all headlines (based on HTML structure of BBC's homepage)
    headlines = soup.find_all('h3', class_='gs-c-promo-heading__title')
    
    if not headlines:
        print("No headlines found.")
        return
    
    print("\n--- BBC News Headlines ---")
    for idx, headline in enumerate(headlines, 1):
        print(f"{idx}. {headline.text}")

if __name__ == "__main__":
    get_bbc_headlines()
