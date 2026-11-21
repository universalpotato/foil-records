# Foil benchmark records

Games between Foil, a self-play model for Magic: The Gathering (Standard), and language models.

24 games per run: 12 deck pairings, both seats. Same pairings and seeds in every run.

| Run | Opponent | Foil | Record | Score [95% CI] | Rating |
|---|---|---|---|---|---|
| `astra-6.2-max__foil-earlier` | Astra 6.2, max effort | earlier checkpoint | 14-10 | 0.58 [0.39, 0.76] | 7.7 |
| `astra-6.2-max__foil-earlier-search` | Astra 6.2, max effort | earlier checkpoint, with search | 14-10 | 0.58 [0.39, 0.76] | 7.5 |
| `astra-6.2-max__foil-final` | Astra 6.2, max effort | final weights | 14-10 | 0.58 [0.39, 0.76] | 7.5 |
| `sol-6.1-high__foil-earlier` | GPT-6.1 Sol, high effort | earlier checkpoint | 15-9 | 0.63 [0.43, 0.79] | 7.3 |
| `sol-6.1-high__foil-final` | GPT-6.1 Sol, high effort | final weights | 15-9 | 0.63 [0.43, 0.79] | 7.2 |
| `fable-5.2-xhigh__foil-final` | Claude Fable 5.2, xhigh effort | final weights | 16-8 | 0.67 [0.47, 0.82] | 6.5 |

- Score: Foil's win rate, Wilson 95% interval.
- Rating: opponent's rating of Foil's play after each game, 1-10, averaged.
- No search unless the run name says so.
- One decision per call. The opponent sees its hand, the board, the stack, recent events, its earlier choices and its decklist.
- Invalid answer: one retry, then first legal option. Never happened.
- Decks: tournament lists from the training pool.
- Earlier checkpoint / final weights: same 17M-parameter model, two points in training.

## Format

`runs/<run>/games.jsonl`, one game per line.

| Field | Meaning |
|---|---|
| `pair`, `foil_seat` | Deck pairing (0-11) and Foil's seat |
| `seed` | Shuffle seed, shared by both games of a pairing |
| `archetypes`, `decklists` | Both decks, in seat order |
| `winner`, `winner_seat`, `turns`, `decisions` | Result and length; decisions count both players |
| `steps` | Each decision: player, kind, number of options, index chosen, text |
| `opponent_usage` | Calls, tokens, latency, retries, fallbacks |
| `opponent_rating_of_foil` | Rating and reason |

Magic: The Gathering is a trademark of Wizards of the Coast. This project is not affiliated with or endorsed by them.
