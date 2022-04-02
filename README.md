> **API USER WARNING:** our main domain and api endpoint has moved to **remotive.com**! Please update your api call to make it to https://remotive.com/api/remote-jobs




<p align=center>
<a href="https://remotive.com">
<img src="https://remotive.com/logo"/>    
</a>
</p>

# Remote Jobs Api

## About remotive.com
We're one of the largest Remote Work Community. Check out our:
- Our Remote [Job Board](https://remotive.com)
- Our vibrant [Slack Community](https://remotive.com/community)
- Read our [Manifesto](https://remotive.com/manifesto)!



## Disclaimer
### Terms of Services

Please note that API documentation and access is granted so that developers can share our jobs further. Please do not submit Remotive jobs to third Party websites, including but not limited to: Jooble, Neuvoo, Google Jobs, LinkedIn Jobs. 

**Please link back to the URL found on Remotive AND mention Remotive as a source in order to Remotive to get traffic from your listing**. If you don't do that, we'll terminate your API access, sorry! 

Jobs displayed are delayed by 24 hours, the goal being that jobs are attributed to Remotive on various platforms. Displaying our jobs in order to collect signups/email addresses to show a listing constitutes a breach of our terms of services. We offer a private, paid-for API, please email us at hello(at)remotive(dot)com for more information.

### Request Rate Limiting

Please note that there is absolutely no need to request Remotive Job data too frequently. Typically, you only need to GET Remotive job data through this API a couple of times a day (we advise max. 4 times a day). Our data is not changing much faster than that anyway. Note that excessive requests (more than 2x per minute) will be blocked.

## Documentation

This API returns the list of all **active** remote job listings on Remotive job board. 
Filtering is available using optional querystring parameters as described below.
Remote job listings are sorted by publication date on Remotive job board.

### URL endpoint for HTTP Request

> GET [https://remotive.com/api/remote-jobs](https://remotive.com/api/remote-jobs)

### Optional Querystring Parameters

Following **optional** querystring parameters can be used to filter job listings.

| Parameter | Description | Example
| ------ | ------ | ------ |
| category | Retrieve jobs only for this category. Category name or category slug must be provided here. Existing categories are available at [this endoint](https://remotive.com/api/remote-jobs/categories). | https://remotive.com/api/remote-jobs?category=software-dev
| company_name | Filter by company name. Case insensitive, partial match ('ilike') will be used here to filter job listings based on provided company name. | https://remotive.com/api/remote-jobs?company_name=remotive
| search | Search job listing title and description. Case insensitive, partial match ('ilike') will be used here to filter job listings. | https://remotive.com/api/remote-jobs?search=front%20end
| limit | Limit the number of job listing results (default: all). An integer must be provided. | https://remotive.com/api/remote-jobs?limit=5

### Response

For example, the following request:
> curl 'https://remotive.com/api/remote-jobs?limit=1'

Would return a JSON response with the following format:
```python
{
    "0-legal-notice": "Remotive API Legal Notice",
    "job-count": 1, # Number or jobs matching the query == length of 'jobs'list
    "jobs": # The list of all jobs retrieved.
    [
        # Then for each job, you get:
        {
            # Unique Remotive ID
            "id": 123, 
            # Job listing detail url
            "url": "https://remotive.com/remote-jobs/product/lead-developer-123", 
            # Job title
            "title": "Lead Developer", 
            # Name of the company which is hiring
            "company_name": "Remotive", 
            # URL to the company logo
            "company_logo": "https://remotive.com/job/123/logo", 
             # See https: # https://remotive.com/api/remote-jobs/categories for existing categories
            "category": "Software Development",
            # full_time/contract/part_time/freelance/internship here.It 's optional and often not filled.
            "job_type": "full_time", 
            # Publication date and time on remotive.com
            "publication_date": "2020-02-15T10:23:26",
            # Geographical restriction for the remote candidate, if any.
            "candidate_required_location": "Worldwide", 
            # salary description, usually a yearly salary range, in USD. Optional.
            "salary": "$40,000 - $50,000", 
            # HTML full description of the job listing
            "description": "The full HTML job description here", 
        },
    ]
}
```

### Prefer using RSS Feeds?

We've got you covered!

Check out our [XML feeds](https://github.com/remotive-io/remote-jobs-feed).

