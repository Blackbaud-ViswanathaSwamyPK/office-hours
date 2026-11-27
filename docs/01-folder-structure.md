# Understanding LLMs: session layout and demo plan

This proposed 30-minute, no-code talk follows one question: how does a large
language model turn a prompt into an answer, and how can we check that answer?

## Where the material belongs

Once the session date and scope are confirmed, use
`sessions/<yyyy-mm-dd>-understanding-llms/` with the actual session date.

| Path within the session | What belongs there |
| --- | --- |
| `notes.md` | The timed agenda, anonymized questions, answers, and follow-ups. |
| `demos/` | The fictional timetable and reusable prompts, if kept as separate files. |
| `slides/` | The presentation deck, only if one is used. |

If all three prompts fit in the notes, keep them there rather than creating
empty folders.

## Three live demos

1. **See the tokens (5 minutes).** Enter `The night train leaves at 8:45.` in
   a tokenizer. Ask the audience to guess the token boundaries before revealing
   them. Replace `8:45` with `eight forty-five` and compare the two displays:
   the departure time is the same, but the input tokens are different.
2. **Predict what comes next (8 minutes).** Ask for completions of
   `At the station, the conductor raised her ___`. Then put
   `The platform was too noisy for anyone to hear her.` before it and vote
   again. Use the changed guesses to illustrate how context affects the next
   token. A model selects a token, adds it to the context, and repeats; the
   audience vote illustrates the idea, not the model's actual probabilities.
3. **Check an answer against evidence (7 minutes).** Give the model a fictional
   timetable entry: `Night train | 8:45 | Platform 3`. Ask which platform to
   use and what the fare is. Have the audience point to the evidence for each
   answer: the entry gives a platform but no fare. Add `Fare: $12` and ask
   again. The comparison works whether the model guessed or declined to guess.

**Q&A and closing check (10 minutes):** Change the fare to `$15`. Ask someone
to explain why the model can now give a different answer without retraining:
the prompt changed, not the model's learned parameters.