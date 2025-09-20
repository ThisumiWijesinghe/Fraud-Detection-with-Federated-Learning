Problem - real world financial transaction datasets are hard to access due to privacy and regulations, fraud detection research suffers because there are almost no public dataset
‎
‎Paper goal - simulate realistic mobile money transactions to produce a synthetic dataset researchers can use without needing sensitive real data
‎
‎Proposed solutions - developed PaySim, Multi agent based simulator for mobile money transactions, built on a sample of real transaction from an African mobile money service 
‎
‎Mthods - agent based modeling with MASON framework (java), transaction probabilities derived from statistical analysis of real logs, clients interact with each other (transfers)
‎
‎Tansaction types - cash out, debit, cash out, payment, transfer 
‎
‎Process - input ( aggregate transaction file per day/hour)
‎          Execution - ( each simulated "step" = 1 day/hour )
‎          Outputs - all details (transaction log) , MySQL database, summery stats, parameter 

Rsults - transaction counts, sums, average, standard deviationa closely match the real data, simulated dataset PS41840 23 million transaction across 5 categories, SSE between real vs synthetic distributions -- minimal error
‎
‎Limitations - paper does not inject fraud or test detection methods; left as future work
