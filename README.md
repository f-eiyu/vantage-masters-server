# Vantage Masters Revisited
Based off of my original Vantage Masters project from back in the day, this capstone will create an even better port of Vantage Masters and so has several key aims:
- Create a server (using Express and Mongoose) for the original Vantage Masters project, which will include:
  - Account functionality (to keep track of wins and losses, save decks, share decks, etc).
  - All gameplay handling on the server side, including damage calculation and all AI behavior
  - `node-cache` (or similar package) utilization on the back end to avoid excessive database calls and allow users to resume games if they close the browser.
- Create the back end using Typescript.
- Fix the bugs with aura passive abilities that were present in the original game.
- Implement the originally desired deck builder and incorporate it smoothly into the account system.

Some stretch goals beyond this involve expanding on the AI behaviors and creating custom decks for AI opponents instead of simply randomizing them.

# Planning
## Routes
|Action|Path|HTTP|Description|
|----|----|----|----|
|Index|`/`|GET|Title screen|
|New Game|`/game/options`|GET|Deck selection and options for starting a game|
||`/game/options`|POST|Send deck and options to the server|
|Play!|`/game/board`|GET|Render the game board|
||`/game/board`|PUT|Send current board state and player's selected action to the server|
|&nbsp;
|Sign Up|`/account/sign-up`|POST|
|Sign In|`/account/sign-in`|POST|
|Sign Out|`/account/sign-out`|DELETE|
|Settings|`/account/settings`|PATCH|
|&nbsp;
|Index|`/decks`|GET|Shows all decks for the current user|
|New|`/decks/new-deck`|GET|Interface to create a new deck|
|Create|`/decks/new-deck`|POST|Validates and creates the new deck|
|Show|`/decks/:id`|GET|Shows a particular deck|
|Edit|`/decks/:id/edit`|GET|Interface to edit the selected deck|
|Update|`/decks/:id`|PUT|Validates and updates the selected deck|
|Destroy|`/decks/:id`|DELETE|Removes a particular deck permanently|

## ERDs
Decks will be the main model that regular users have access to and can edit, so they will be the only model with full CRUD. As a stretch goal, it would be nice to have an "admin" account type that has full CRUD permissions on cards as well, with a corresponding front end, but that's exactly that -- a stretch goal.

Thus, the ERD for this project should actually be extremely simple. I literally just moved (for one final time!) yesterday and my notebook is still in a suitcase somewhere, so I can't offer my usual terribly drawn ERD, but if I *could*, it might look something like the following:

`user ─∈ deck ─∈ card`

This is not meant to be the complicated part of the project. :)

## Seed Data
I will be creating two or three "starter" decks for users to play with, so that they will not need to create their own deck from scratch before even playing the game. This is a bit too time-consuming to generate right now before the project even gets approved, but it will be a part of the final product. 

An example deck using card names (the implementations of the prebuilt decks will use IDs, not names) might look like: `[Bard (master), Uptide, Uptide, Uptide, Requ, Requ, Requ, Zamilpen, Zamilpen, Zamilpen, Neptjuno, Neptjuno, Neptjuno, Kyrier-Bell, Kyrier-Bell, Guene-Foss, Guene-Foss, Guene-Foss, Magic Crystal, Magic Crystal, Magic Crystal]`.

All of the cards that were in the game before will also be in the database, so I suppose that is a sort of seed data as well.