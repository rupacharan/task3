import requests
from bs4 import BeautifulSoup

# URL of the web page to scrape
url = 'https://www.geeksforgeeks.org/what-is-web-scraping-and-how-to-use-it/'

# Fetch the content of the web page
response = requests.get(url)
if response.status_code == 200:
    # Parse the content of the web page
    soup = BeautifulSoup(response.content, 'html.parser')

    # Extract text content
    text_content = soup.get_text()
    print("Text Content:")
    print(text_content)

    # Extract all links
    links = soup.find_all('a')
    print("\nLinks:")
    for link in links:
        href = link.get('href')
        if href:
            print(href)

    # Extract all images
    images = soup.find_all('img')
    print("\nImages:")
    for img in images:
        src = img.get('src')
        if src:
            print(src)
else:
    print(f"Failed to retrieve the web page. Status code: {response.status_code}")
