# ICP & Buyer Intent Assessment Workflow
This repository consists of a workflow designed to help sales professionals (or really, anyone who wants to more leads) source additional leads based on job postings and specific buyer intent factors. 

## Required Tech Stack
The ICP & Buyer Intent Assessment workflow runs on a more complex tech stack than some of the other automations on my GitHub. The following tech is necessary to run the workflow:
- Slack: You will need to create a dedicated channel in Slack to be able to implement this automation. However, it should be noted that you do not need to be using a paid version of Slack for this automation to work!
- Perplexity: Perplexity is an AI search model that I'm using to fill the role of scrapers throughout certain parts of the automation, where the information I need is more readily available through web search. However, if you prefer to use a scraper instead, go ahead and swap out those nodes!
- An AI Model: In my automation, I'm using an AI model to organize some of the data, mainly because I got tired of using an endless number of JS functions to clean up the data I was grabbing. I personally went with GPT because it's the best at following instructions in my opion. If you feel more comfortable using JS, however, I encourage you to clean up the automation with a few better-written JS functions to extract the data from Perplexity searches. 
- ScrapingDog API (or another scraping service): I'm using the ScrapingDog API to scrape LinkedIn for specific job posts - which is the one job that I didn't trust Perplexity enough to do.

## The Workflow:
The workflow itself functions in three key stages, each of which has its own purpose.

### Scraping Data:
The first stage of the automation is where we scrape for specific job postings. More specifically, when setting up this automation, you'll want to look for companies that are hiring for positions that indicate they might need your service. In the example file, we're looking for companies that want contract Business Development employees.

I'm using three different ScrapingDog API calls to look through the first three pages of LinkedIn job postings every 24 hours. You can scale that up/down as you see fit. All the scraped data is then merged back onto one path.

### Company Evaluation Against ICP:
The next stage of the automation looks to compare the companies hiring against an ICP (Ideal Client Profile). A Perplexity node is looped to run a search on each hiring company, looking for specific insights. After each search, a 5 second pause is used to prevent the API from overloading. You can customized the Perplexity prompt to unearth whatever insights make the most sense for your ICP.

Once the searches are finished, a JS function evaluates the findings against a scoring system, providing a score for each hiring company based on how well they match with the specific ICP. From there, an IF node redirects hiring companies for additional valuation if they are a semi-match with the ICP.

### Buyer Intent Evaluation:
The final stage of the automation measures buyer intent. Once again, a Perplexity search is used to look for specific factors that indicate the hiring company may be looking for your service. Examples include recent hiring, content engagement, thought leadership posts, fundraising activity, blog content, M&A activity, etc. This data is then cleaned and processed with a combination of JS functions and an AI agent, before running through another JS scoring function. If the score is high enough, a message is sent to a Slack channel to alert sales reps of the fact that a company could be a good prospect.

## Future Improvements:
If I were to expand this automation in the future, I would connect it to Apollo and HubSpot (assuming I had the tools available) and make this a full circle sales automation. If a company matched the ICP and had a certain buyer intent threshold, I would call the Apollo API to grab contact information for a few key contacts, then import those contacts into HubSpot to run another automated campaign. This would effectively allow the user to source and target leads with sales outreach, entirely on autopilot.
