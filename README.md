# AI Newsletter Automation (n8n)

An n8n workflow that researches a topic, drafts newsletter sections with an LLM, edits the combined draft into a final copy, and emails it through Gmail.

![Workflow diagram](images/workflow-diagram.png)

## How it works

1. **Trigger.** The workflow starts from a chat message containing the newsletter topic, or from a manual "Execute workflow" run for testing. A Schedule Trigger can be added for recurring sends.
2. **Initial research.** A search node pulls source material for the topic from the query you supply.
3. **Section Writer Agent.** An OpenAI chat model writes each newsletter section from the research.
4. **Aggregate.** The section outputs are combined into a single draft.
5. **Editor Agent.** A second agent edits the full draft into final copy. A Structured Output Parser keeps the response in a consistent format.
6. **Send a message.** The Gmail node sends the final newsletter.

## Sample output

![Sample output](images/sample-output.png)

## Prerequisites

- [n8n](https://n8n.io/) (self-hosted or cloud)
- An OpenAI API key
- A search tool credential for the research node
- A Gmail account connected to n8n through OAuth

## Setup

1. In n8n, go to **Workflows → Import from File** and select `workflow/newsletter-workflow.json`.
2. Create credentials for each node that shows a warning icon: OpenAI, the research/search tool, and Gmail.
3. Set the newsletter topic in the chat trigger or the research node's `query` field.
4. Replace the recipient address in the Gmail node.
5. Click **Execute workflow** to test. Once it works, activate the workflow.

## Configuration

| Setting | Where | Notes |
|---|---|---|
| Topic | Chat trigger / `query` field | Free text |
| Model | OpenAI Chat Model nodes | Use the same or a cheaper model for each agent |
| Recipient | Gmail node | Your address or a distribution list |
| Schedule | Trigger node | Add a Schedule Trigger for recurring sends |

## Project structure

```
your-repo/
├── README.md
├── workflow/
│   └── newsletter-workflow.json
└── images/
    ├── workflow-diagram.png
    └── sample-output.png
```

## Notes and limitations

- Output quality depends on the research source. Review drafts before sending to an external audience.
- Credentials are stored in n8n, not in this repository.
- Financial or market content is for information only and is not investment advice.

## License

Choose a license, for example MIT.
