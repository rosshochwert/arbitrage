My attempt at the Priceonomics puzzle: http://priceonomics.com/jobs/puzzle/

### How it Works

The basic premise of arbitrage is to buy something for one price and instantly sell it for another. In our case, we want to find a currency with a price discrepancy, e.g. one where converting between multiple currencies will eventually lead you to make more money in your starting currency than you began with. If we assume we have $1, our goal is to convert our money until we end up with x<$1.

We turn each currency into a node and each conversion into an arc. This setup creates a directed graph where the weights of each edge is the conversion rate (i.e. USD to EUR is .67 but USD to EUR is 1.5). Utilizing a neat high school math trick, we can log() each conversion rate which then makes addition of logged conversions really multiplication of unlogged. Utilizing a neat little middle school trick, we can apply a negative sign to each number to make it negative. 

Now, all we need to do is apply the Bellman-Ford algorithm to detect a negative loop, which indicates an aribitrage opportunity. Why? Because a negative loop indicates you can cycle along this path infinitely, at increasing negative cost. When we unlog our numbers and reverse the negative sign, this translates to a loop that can start with $1 and infinitely increase it as it follows this loop.

Once the Bellman-Ford detects a negative loop, we trace back the loop in the negative_trace function and spit out the answer.

### Thanks

Shoutout to Sedgewick for the arbitrage idea: http://algs4.cs.princeton.edu/44sp/

Special thanks to Joninviski for the Bellman-Ford python code: https://gist.github.com/joninvski/701720
