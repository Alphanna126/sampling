# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Ann Paul

```
So here initially in simulate_event(m) a subset of event attendees is randomly infected based on a fixed attack rate of 10% (i.e ATTACK_RATE = 0.10). in this initial sampling, the sample size is 1000*10% which 100 people are infected. the sampling frame is the entire 1000 people. np.random.choice() indicates the sample is chosen without replacement and as random sampling.

Next in primary contact tracing: Among infected individuals, a subset is randomly chosen to be successfully traced, based on the trace success rate of 20% (i.e.TRACE_SUCCESS).in the second level of sampling the sample Size: 100×20%=20 individuals traced. the sampling Frame is the 100 infected individuals.in this each infected person has a 20% probability of being traced, using np.random.rand() < TRACE_SUCCESS

In Sampling for Secondary Contact Tracing: Here Events where at least 2 primary cases that are traced are selected for event-wide secondary tracing.in this case ,Sample Size varies per simulation but depends on how many events meet the threshold.and the sampling Frame is all events where at least one infected individual was traced.Looks like here we have Threshold-based sampling -something like a condition to be considered and not just random.

while running the code as it, i see the difference such that for infections centers on 20%, with some variation around that. and traces  is also seen within 20% in the code. But in blog, the observed population is around 50%. 
The blog post explains how contact tracing overrepresents infections in structured, traceable settings (e.g., weddings) while underrepresenting unstructured gatherings (e.g., brunches).

I modified the code as: results = [simulate_event(m) for m in range(100)] to Modify the number of repetitions in the simulation to 100. each time i ran the python file, the graph plot varied and gave me different result set. This is mainly because we did not set the sees in the initial part of the program.

Inorder to introduce reproducibility, we can issue, the below code line:

np.random.seed(42)
This will ensure the same result is seen everytime the python file is run. the histogram will be identical final result set will be the same always in props_df


```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 16/02/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `assignment-1`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
