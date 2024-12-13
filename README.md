# Technical SEO SaaS
https://github.com/joshcarty/google-searchconsole
https://developers.google.com/speed/docs/insights/v5/get-started
https://www.abuseipdb.com/api.html


A Python-based SEO audit tool for analyzing technical SEO aspects of websites.
```
mehernigarcu@gmail.com
```

### Features
i. Domain Check
```
- who.is (Register & Expire)
- DA 
- Link
- Top Linking Domain
- Ranking Keywords
- Subdomain Finder
- DNS Report - https://who.is/dns/gopjobs.gop
- Hosting IP reputation - https://www.abuseipdb.com/check/172.67.197.142
- indexed pages : 
```
```
https://mxtoolbox.com/
https://www.link-assistant.com/free-tools/domain-authority-checker-tool.html
https://moz.com/domain-analysis
https://seomator.com/free-domain-authority-checker
https://seomator.com/free-backlink-checker-tool
https://seranking.com/domain-trust-checker.html?
https://www.dnscolos.com/free-dns-report.html
https://www.clickminded.com/domain-authority-checker/
https://www.whois.com/whois
who.is
https://pro.similarweb.com/#/digitalsuite/websiteanalysis/overview/website-performance/*/999/1m?webSource=Total&key=bluearrayacademy.com
```
i. Technical Check:
```
01. Sitemap Check
02. Robots.txt Check
03. Loading Time (https://developers.google.com/speed/docs/insights/v5/get-started)
04. Page Size
05. JS Blocking  (Pre-render - Re-render)
06. HTML Structure Error
07. Schema Found
08. Security - Insecure Pages
09. Pagination
```
ii. User Exprience Check
```
10. favicon check
10. Crawl Mobile Version
11. AMP (Accelerated Mobile Pages) Support
12. Viewport Meta Tag Check (Mobile)
13. Breadcrumb Navigation
14. Policy (Cookie, Content-Security)
15. Multi Language Support
15. Site navigation - header footer menu body
```
iii. Content Check
```
16. Title & Meta
16.1 Post Data & Update Date
17. H1, H2, H3 Parent-Child Order
18. Thin Content
19. Duplicate Content
20. Canonical Tag
21. Content Freshness
22. Content Readability
23. Report of Un update content with filtering sitemap
```
iv. Linking Check
```
23. 404 Error Check
24. Internal Linking (Do follow/No follow)
25. External Linking (Do follow/No follow)
26. Follow & Nofollow and Anchor Text
27. Redirect Check (Redirect time)
```
v. Images Check
```
28. Image Size
29. Lazy Loading for Images
30. Image Alt Text Check
```

## i Domain
```py
from playwright.sync_api import sync_playwright
from time import sleep

args=[
     '--disable-blink-features=AutomationControlled',
     '--start-maximized',
     '--disable-infobars',
     '--no-sandbox',
     '--disable-dev-shm-usage',
     '--disable-extensions',
     '--remote-debugging-port=0',
     '--disable-web-security',
     '--enable-features=WebRTCPeerConnectionWithBlockIceAddresses',
     '--force-webrtc-ip-handling-policy=disable_non_proxied_udp',
 ]

path = 'chrome-win/chrome.exe'

site_list = ['who.is','github.com','shop.torklaw.com','bluearrayacademy.com']
for site in site_list:
    with sync_playwright() as p:
        browser = p.chromium.launch(headless=False, 
                                    executable_path=path,
                                    args=args,
                                     proxy={
                                    "server": "http://gw.dataimpulse.com:823",  # Your rotating proxy server
                                    "username": "5505791abd",  # Your proxy username   0cd522901c__cr.us
                                    "password": "f5d3919"  # Your proxy password   c504d8fc9
                                })
        context = browser.new_context(no_viewport=True)
        page = context.new_page()
        page.goto(f'https://moz.com/domain-analysis?site={site}', timeout=60000) # 1 min
        sleep(5)
        browser.close()

```
# i. Technical Check
## 01. Sitemap Check
```py
import requests

def check_sitemap(url):
    sitemap_url = url + "/sitemap.xml"
    response = requests.get(sitemap_url)
    if response.status_code == 200:
        print("Sitemap found!")
    else:
        print("No sitemap found.")
```
## 02. Robots.txt Check
```py
def check_robots_txt(url):
    robots_url = url + "/robots.txt"
    response = requests.get(robots_url)
    if response.status_code == 200:
        print("robots.txt found!")
    else:
        print("No robots.txt found.")
```
## 03. Loading Time
```py
import time

def check_loading_time(url):
    start_time = time.time()
    response = requests.get(url)
    loading_time = time.time() - start_time
    print(f"Loading time: {loading_time} seconds")
```
## 04. Page Size
```py
def check_page_size(url):
    response = requests.get(url)
    page_size = len(response.content)
    print(f"Page size: {page_size} bytes")
```
## 05. JS Blocking
```py
def check_js_blocking(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    scripts = soup.find_all('script')
    for script in scripts:
        if script.get('src'):
            print(f"JavaScript found: {script.get('src')}")
```
## 06. HTML Structure Error
```py
def check_html_structure(url):
    try:
        response = requests.get(url)
        soup = BeautifulSoup(response.text, 'html.parser')
        print("HTML structure is valid.")
    except Exception as e:
        print(f"HTML structure error: {e}")
```
## 07. Schema Error
```py
def check_schema(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    schemas = soup.find_all('script', {'type': 'application/ld+json'})
    if schemas:
        print("Schema found.")
    else:
        print("No schema found.")
```
## 08. Security - Insecure Pages
```py
def check_insecure_content(url):
    response = requests.get(url)
    if not url.startswith('https'):
        print("Insecure page detected.")
    else:
        print("Page is secure.")
```
## 09. Pagination
```py
def check_pagination(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    pagination = soup.find_all('a', {'rel': 'next'})
    if pagination:
        print("Pagination found.")
    else:
        print("No pagination found.")
```



# ii. User Exprience Check
## 10. Crawl Mobile Version
```py
def crawl_mobile_version(url):
    headers = {
        "User-Agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 13_2_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.3 Mobile/15E148 Safari/604.1"
    }
    response = requests.get(url, headers=headers)
    print(f"Mobile version crawl status: {response.status_code}")
```
## 11. AMP (Accelerated Mobile Pages) Support
```py
def check_amp(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    amp_html = soup.find('link', {'rel': 'amphtml'})
    if amp_html:
        print(f"AMP page found: {amp_html.get('href')}")
    else:
        print("No AMP page found.")
```
## 12. Viewport Meta Tag Check (Mobile)
```py
def check_viewport_meta(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    viewport = soup.find('meta', {'name': 'viewport'})
    if viewport:
        print("Viewport meta tag found.")
    else:
        print("No viewport meta tag found.")
```
## 13. Breadcrumb Navigation
```py
def check_breadcrumbs(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    breadcrumbs = soup.find('nav', {'aria-label': 'breadcrumb'})
    if breadcrumbs:
        print("Breadcrumb navigation found.")
    else:
        print("No breadcrumb navigation found.")
```
## 14. Policy (Cookie, Content-Security)
```py
def check_cookie_compliance(url):
    response = requests.get(url)
    if 'Set-Cookie' in response.headers:
        print("Cookies are being set on this page.")
    else:
        print("No cookies found.")

def check_csp(url):
    response = requests.get(url)
    csp = response.headers.get('Content-Security-Policy')
    if csp:
        print(f"Content Security Policy found: {csp}")
    else:
        print("No Content Security Policy found.")

```
## 15. Multi Language Support
```py
def check_hreflang(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    hreflangs = soup.find_all('link', {'rel': 'alternate', 'hreflang': True})
    if hreflangs:
        for lang in hreflangs:
            print(f"Language version found: {lang['hreflang']} -> {lang['href']}")
    else:
        print("No hreflang tags found.")
```





# iii. Content Check
## 16. Title & Meta
```py
def check_title_meta(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    title = soup.find('title').text
    meta_description = soup.find('meta', {'name': 'description'})
    print(f"Title: {title}")
    if meta_description:
        print(f"Meta Description: {meta_description.get('content')}")
    else:
        print("No meta description found.")
```
## 17. H1, H2, H3 Parent-Child Order
```py
def check_heading_order(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    headings = soup.find_all(['h1', 'h2', 'h3'])
    for heading in headings:
        print(heading.name, heading.text.strip())
```
## 18. Thin Content
```py
def check_thin_content(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    text = soup.get_text()
    word_count = len(text.split())
    if word_count < 300:
        print(f"Thin content detected with {word_count} words.")
    else:
        print(f"Content is OK with {word_count} words.")
```
## 19. Duplicate Content
```py
def check_duplicate_content(url, other_url):
    content1 = requests.get(url).text
    content2 = requests.get(other_url).text
    if content1 == content2:
        print("Duplicate content detected.")
    else:
        print("No duplicate content.")
```
## 20. Canonical Tag
```py
def check_canonical(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    canonical = soup.find('link', {'rel': 'canonical'})
    if canonical:
        print(f"Canonical URL: {canonical.get('href')}")
    else:
        print("No canonical URL found.")
```
## 21. Content Freshness
```py
def check_content_freshness(url):
    response = requests.head(url)
    last_modified = response.headers.get('Last-Modified')
    if last_modified:
        print(f"Page last modified on: {last_modified}")
    else:
        print("No Last-Modified header found.")
```

## 22. Content Readability
```py
import textstat

def check_content_readability(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    text = soup.get_text()
    readability_score = textstat.flesch_reading_ease(text)
    print(f"Readability score: {readability_score}")
```






# iv. Linking Check
## 23. 404 Error Check
```py
def check_404(url):
    response = requests.get(url)
    if response.status_code == 404:
        print(f"{url} is a 404 error.")
    else:
        print(f"{url} is accessible.")
```
## 24. Internal Linking
```py
def check_internal_links(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    links = soup.find_all('a', href=True)
    for link in links:
        if url in link['href']:
            print(f"Internal link: {link['href']}")
```
## 25. External Linking
```py
def check_external_links(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    links = soup.find_all('a', href=True)
    for link in links:
        if url not in link['href']:
            print(f"External link: {link['href']}")
```

## 26. Follow & Nofollow and Anchor Text
```py
def check_follow_nofollow(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    links = soup.find_all('a', href=True)
    for link in links:
        rel = link.get('rel')
        if rel and 'nofollow' in rel:
            print(f"Nofollow link: {link['href']} with anchor text: {link.text.strip()}")
        else:
            print(f"Follow link: {link['href']} with anchor text: {link.text.strip()}")
```
## 27. Redirect Check
```py
def check_redirect(url):
    response = requests.get(url)
    if response.history:
        print(f"Redirect found for {url}")
    else:
        print(f"No redirect for {url}")
```




## v. Images Check
## 28. Image Size
```py
from bs4 import BeautifulSoup
def check_image_size(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    images = soup.find_all('img')
    for img in images:
        img_url = img.get('src')
        img_response = requests.get(img_url)
        img_size = len(img_response.content)
        print(f"Image {img_url} size: {img_size} bytes")
```

## 29. Lazy Loading for Images
```py
def check_lazy_loading(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    images = soup.find_all('img')
    for img in images:
        if img.get('loading') == 'lazy':
            print(f"Image {img.get('src')} uses lazy loading.")
        else:
            print(f"Image {img.get('src')} does not use lazy loading.")
```

## 30. Image Alt Text Check
```py
def check_image_alt_text(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.text, 'html.parser')
    images = soup.find_all('img')
    for img in images:
        alt_text = img.get('alt')
        if alt_text:
            print(f"Image {img.get('src')} has alt text: {alt_text}")
        else:
            print(f"Image {img.get('src')} is missing alt text.")
```



