# Backend Take-home Test

The task is split in three parts:
- The first part is to implement a parser for a proprietary genetic data format
- The second part is to implement an API that allows for retrieving genetic results stored in the proprietary format.
- The final part is a short loom video (~5 mins) outlining your solution

You can complete this task in any programming language of your choice, but we ask that you use a language that you are 
comfortable answering detailed questions about.

We understand that balancing this task with other responsibilities is important, so we estimate that completing it should take a few hours.
While we suggest aiming for that time frame, feel free to exceed it if necessary, though we remain mindful of respecting your time.

We are interested in understanding how you would structure and architect production-grade backend code for a medium to large codebase. Please organize your solution in a way that reflects how you would build a maintainable service in a real production environment.

> [!TIP]
> This is a big task and you won't have time to implement everything perfectly in the suggested time frame, we understand (and expect) you to have
> to make tradeoffs when implementing this, so aim to get a working solution and leave comments where you'd improve things if you had more
> time.

## AI usage

You're welcome to use AI tools whilst completing this task. We won't mark candidates down for using AI.

What we do expect is that you fully own the submission:

- you understand the code that you submit
- you can explain your design and tradeoffs
- you can discuss what you would improve with more time

If you'd like to share how you used AI (for example what it helped with, what you refined, and what you verified yourself), that context is welcome in your submission.

### Part 1: Genetic Data Parser
You'll be writing a parser for a proprietary genetic data format. The format is a text file whose format contains
genetic data for a single individual. The first line of the file is a header (line starts with a `#`) that contains:
- Variant ID (string, unique identifier for the genetic variant, e.g. `rs12345`)
- Chromosome (1-22, X, Y)
- Position on chromosome (integer greater than 0)
- Reference allele (single character representing a nucleotide: `[A, C, G, T]`)
- Alternate allele (single character representing a nucleotide: `[A, C, G, T]`)
- Alternate allele frequency (float, between 0 and 1)

Each of these fields is separated by a comma (`,`). The header line will always contain these fields (and only these 
fields) but the order may vary.

The rest of the file contains the genetic data for the individual. Each line contains values for the fields in the 
header in the same order as the header. The values are separated by a comma (`,`).

If any of the data is missing or invalid, the parser should return an error.

A valid sample file for an individual is provided in this repo [here](./individual123.sano).

### Part 2: Genetic Results API
You'll be writing an API that allows for uploading and retrieving genetic results. We expect you to use your parser from
Part 1 to parse the genetic data that is uploaded and store it for retrieval later.

> [!IMPORTANT]
> For this task, the choice of data store (e.g., in-memory object, SQL, file system, etc.) is entirely up to you. The focus is on how you create the abstraction, not on specific database expertise.

Your API should implement the following endpoints:
- `GET /individuals`: returns a list of individual IDs
- `GET /individuals/<individual_id>/genetic-data?variants=rs123,rs456`: returns all the genetic data for a single individual, optionally filtered by variant IDs
- `POST /individuals`: creates a new individual given an ID
- `POST /individuals/<individual_id>/genetic-data`: takes a sano file and stores the genetic data for that individual to be queried later

Include a `README.md` file with instructions on how to run your API and how to interact with it to fulfill the use cases
described below:
1. Create an individual with ID `individual123` using the `POST /individuals` endpoint
2. Show that the individual is present by querying the `GET /individuals` endpoint
3. Upload some genetic data from a file to the individual via the `POST /individuals/individual123/genetic-data` endpoint
4. Show that all the data is queryable via the `GET /individuals/individual123/genetic-data` endpoint, and then show that the filtering works successfully by calling the same endpoint again, but this time filtering for only 2 variants present in the file


### Part 3: Loom video

Create a short [loom](https://www.loom.com/) video (~5 minutes) walking us through your submission and include the link your README.

This is your opportunity to explain the submission to the team. The content of the video is up to you, but we want to hear about your decision making process as an engineer as opposed to a demonstration of each endpoint.

Try and include:
- How you approached the problem, solutions considered, and the tradeoffs involved
- What you found difficult
- Any changes you'd make given you had longer to work on it

## Submitting Your Solution
Please create a new private repository on GitHub and commit your solution to it. Once you're done, please invite 
`sano-review` as a collaborator to the repository, as well as letting us know that you've completed the task via email 
with the talent team.

In your README.md, remember to include the URL to your loom video.

> [!CAUTION]
> If you haven't heard back from the talent team within a couple of days of sending your solution, follow up with them
> to check it has been received
