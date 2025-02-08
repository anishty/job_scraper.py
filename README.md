import requests
from bs4 import BeautifulSoup

# URL of the job website (TimesJobs)
URL = "https://www.timesjobs.com/candidate/job-search.html?searchType=personalizedSearch&from=submit&txtKeywords=python&txtLocation="

# Fetch the webpage
response = requests.get(URL)
soup = BeautifulSoup(response.text, "html.parser")

# Find job postings
jobs = soup.find_all("li", class_="clearfix job-bx wht-shd-bx")

# Display job results
for index, job in enumerate(jobs[:5]):  # Get first 5 jobs
    company_name = job.find("h3", class_="joblist-comp-name").text.strip()
    skills = job.find("span", class_="srp-skills").text.strip()
    more_info = job.header.h2.a["href"]

    print(f"{index+1}. Company: {company_name}")
    print(f"   Skills Required: {skills}")
    print(f"   More Info: {more_info}")
    print("-" * 50)

