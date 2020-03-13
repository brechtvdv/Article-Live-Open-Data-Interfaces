## Problem Statement
{:#problemstatement}

In the field report, we saw that there is no strict guideline whether to use polling or pushing for a certain dataset. Based on the insights from the field report and related work, we define the following research question:

Research question: Which kind of Web interface for server to client communication is best suited for publishing live Open Data in function of server-side cost, scalability and latency on the client?

Following hypotheses are defined which we’ll be answered in the discussion:

**H1**: Using a Server-Sent Events interface will result in a lower latency on the client, compared to a polling interface.

**H2**: The server-side CPU cost of an HTTP polling interface is initially higher than a Server-Sent Events interface, but increases less steeply when the number of clients increases.

**H3**: From a certain number of clients onward, the server cost of a Server-Sent Events interface exceeds the server cost of a polling interface.
