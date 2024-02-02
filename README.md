# Buzzwords

This is a simple word game built on the anagramica.com API. The game generates 6 random letters, and the player has to come up with as many words as possible with these letters. Using the anagramica.com API, the app checks the player's words against a dictionary and returns the valid words.

## Tech Stack

- This app uses **Svelte**, **Tailwind**, and **shadcn/ui** for the front end.
- The back end is built with **AWS Lambda** and **API Gateway** (mostly as a wrapper to the anagramica.com API).
- This app is hosted on **Vercel** with automated deployments on pushes to the main branch.
