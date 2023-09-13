# twitter 接口调研

## twitter api v2

### Search Tweets
Searching for Tweets is an important feature used to surface Twitter conversations about a specific topic or event. While this functionality is present in Twitter, these endpoints provide greater flexibility and power when filtering for and ingesting Tweets so you can find relevant data for your research more easily; build out near-real-time ‘listening’ applications; or generally explore, analyze, and/or act upon Tweets related to a topic of interest. 
These endpoints will always return the most recent edit, along with any edit history. Any Tweet collected after its 30-minute edit window will represent its final version. To learn more about Edit Tweet metadata, check out the Edit Tweets fundamentals page.


#### Recent search
The recent search endpoint allows you to programmatically access filtered public Tweets posted over the last week, and is available to all developers who have a developer account and are using keys and tokens from an App within a Project.


#### Full-archive search
The v2 full-archive search endpoint is only available to Projects with Academic Research access or Enteprise access. The endpoint allows you to programmatically access public Tweets from the complete archive dating back to the first Tweet in March 2006, based on your search query.


### Filtered streams


# twitter 
* Free (API list)  
    POST /2/tweets
    DELETE /2/tweets/:id
    GET /2/users/me
* Pro price $5000/month
* Basic price $100/month
    