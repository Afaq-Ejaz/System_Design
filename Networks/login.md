# Login attempts

---> 429 -- too Many requests
When you try to login , there is some sort of rate limiter that prevents from too many requests
Most commonly this rate limit is 100 request per minute , it resets back to zero after every minute
But here comes the problem : if user sends 100 request in last 10 seconds of the minute and then in first ten seconds it 
sends again 100 requests. 

Solution: 
## Token Buckets
--> There ia bucket of tokens for every user that can have max 100 tokens at a time.
when user does a request a token is used from the bucket.
It refills in rate limit time  / rate limit

### if we have multiple servers then ?
It means we have multiple RAMs , we have multiple buckets at every server
for this purpose we use REDIS that provides them the buckets of token.