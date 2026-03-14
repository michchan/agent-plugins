/skill-creator I want to create a skill based on @plugins/personal-investing-and-wealth-management/skills/equity-analysis-workflow/requirements.md. Put the skill on the same folder. I want to leverage the "financial-services-plugins" by anthropics. 

However, I won't have the required MCP servers conneceted for data sources. In order to optimize token cost, please help optimize any web search action in the skill. For example, like these ways from most to least impactful:

1. Fetch once, pass forward (biggest win)
The initiation workflow's 5 tasks each independently searching for the same company is the main culprit. The skill should front-load a single structured data fetch in Task 1 and save the output to a markdown file, then Tasks 2–5 Read that file rather than re-fetching.

2. Targeted WebFetch prompts
WebFetch's prompt parameter is the filter. Instead of fetching a full page and loading everything into context, a tight prompt like "Extract: revenue, operating income, FCF, and debt for last 4 quarters only" dramatically cuts what comes back. Skills that just say "research the company" leave this wide open.

3. Prefer structured sources
SEC EDGAR (/cgi-bin/browse-edgar) returns clean structured data at a fraction of the tokens of a news article or investor relations page that's full of navigation chrome, disclaimers, and prose. For financials specifically, EDGAR + a focused prompt is the most token-efficient path.