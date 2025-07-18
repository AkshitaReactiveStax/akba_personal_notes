1. Api gateway pattern :

benifits :  single point of entry , authentication , authorization , rate limiting , throttling , logging , orchestration , payload transformation . 

vendors : apigee owned by google , kong , MuleSoft , CA api gateway , IBM API connect , Amazon api gateway .

2. circuit-breaker pattern : 3 states of the pattern are  -> open , closed , half-open .

benifits : retry , rate limit , throttling , time limitter , cache , fallback , bulkhead  

vendors : redilience4j 

3. Externalized-Configuration pattern : 