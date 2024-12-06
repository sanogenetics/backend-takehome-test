# Backend Take-home Test

The task is split in two parts, the first part is to implement a parser for a proprietary genetic data format, and the
second part is to implement an API that allows for retrieving genetic results stored in the proprietary format.

You can complete this task in any programming language of your choice, but we ask that you use a language that you are 
comfortable answering detailed questions about.

We understand that balancing this task with other responsibilities is important, so we estimate that completing it should take around 3 to 4 hours.
While we suggest aiming for that time frame, feel free to exceed it if necessary, though we remain mindful of respecting your time.

When reviewing your submission, we'll be looking for pragmatic solutions that are easy to understand and maintain. How you choose to test this
is up to you, but we will be expecting a tested solution that covers some potential edge cases you can think of.

> [!TIP]
> This is a big task and you won't have time to implement everything perfectly in the suggested time frame, we understand (and expect) you to have
> to make tradeoffs when implementing this, so aim to get a working solution and leave comments where you'd improve things if you had more
> time.

After you've completed the task, take a short [loom](https://www.loom.com/) video (~5 minutes) walking us through how you approached the problem,
what you found difficult and any changes you'd make given you had longer to work on it. Put the loom URL in the README.md of your repo.

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
> For this task, the choice of storage solution (e.g., SQL, in-memory object, file system, etc.) is entirely up to you. The focus is on how you create the abstraction, not on specific database expertise.

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

## Submitting Your Solution
Please create a new private repository on GitHub and commit your solution to it. Once you're done, please invite 
`sano-review` as a collaborator to the repository, as well as letting us know that you've completed the task via email 
with the talent team.

In your README.md, remember to include the URL to your loom video.

> [!CAUTION]
> If you haven't heard back from the talent team within a couple of days of sending your solution, follow up with them
> to check it has been received
