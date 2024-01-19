# LinkedIn-Scraper-Bot

The LinkedIn-Scraper-Bot is a sophisticated tool designed to automate the process of extracting job listings from LinkedIn based on specific keywords and locations. Crafted as a Python class object named LinkedInBot, it offers a seamless experience in data extraction.

### Setting Up
Before diving into the capabilities of LinkedIn-Scraper-Bot, ensure your environment is ready by installing the necessary dependencies:

```bash
pip install -r requirements.txt
```

### Quick Start
The core functionality of the bot is encapsulated in the `run` method. This method orchestrates the login process, navigates to the job section, performs a search based on your specified criteria, and scrapes the job listings from the first 8 pages. The data, including job title, company, location, and job description, is conveniently saved in a SQLite database located at `data/linkedin_data.db`.

```python
EMAIL = "your email"
PASSWORD = "your password"

bot = LinkedInBot()
bot.run(EMAIL, PASSWORD, "Data Scientist", "Canada")
```

### Cookie Reuse for Efficiency
To enhance efficiency, LinkedIn-Scraper-Bot stores browser cookies after the initial login. This allows for quicker subsequent sessions without the need to log in each time.

### Customizing Your Scraping Session
For those who prefer a more hands-on approach, you can craft your scraping session using the building blocks provided by the bot:

```python
# Log in and save cookies:
bot.login(email=EMAIL, password=PASSWORD)
bot.save_cookie("data/cookies.txt")

# Navigate to the jobs page and initiate a search:
keywords = "desired job title or field"
location = "preferred location"
bot.search_linkedin(keywords, location)
bot.wait()  # Pause to ensure the page has loaded

# Iterate through the job listings, extracting the relevant data:
jobs = bot.driver.find_elements_by_class_name("occludable-update")
for job in jobs:
    bot.scroll_to(job)
    [position, company, location, details] = bot.get_position_data(job)

    # Process the data as you see fit...

# Conclude the session:
bot.close_session()
```

### Final Thoughts
The LinkedIn-Scraper-Bot is a powerful ally in your job search or market analysis endeavors, streamlining the data collection process and providing you with rich, actionable insights.