# Restaurant and Meals Planning

## Overview

Restaurant and Meals Planning is an AI-powered restaurant recommendation and meal-planning assistant built with n8n. It helps users discover restaurants and plan meals based on their location, budget, group size, cuisine preferences, dietary requirements, and dining date.

The assistant uses a Retrieval-Augmented Generation (RAG) workflow to search a restaurant knowledge base containing information collected from web pages and a Tunisian dishes CSV file.

## Features

- Provides personalized restaurant and meal recommendations.
- Searches a restaurant knowledge base for menus, prices, cuisines, locations, specialties, and other available details.
- Uses current weather information when weather may affect dining plans, such as choosing indoor or outdoor seating.
- Sends restaurant recommendations by email when requested.
- Creates Google Calendar events for dining plans when requested.
- Uses conversation memory to support follow-up questions.
- Collects restaurant information from the Kharjet Tunisia website using Firecrawl.
- Stores documents and embeddings in a Supabase vector store.

## Technologies

- n8n for workflow automation
- Google Gemini for chat responses and embeddings
- Supabase Vector Store for retrieval
- Firecrawl for web research and scraping
- OpenWeatherMap for weather information
- Google Drive for the Tunisian dishes CSV file
- Gmail for sending recommendations
- Google Calendar for scheduling dining plans

## How It Works

### 1. Knowledge-base ingestion

The workflow builds the restaurant knowledge base from two sources:

- A `tunisian_dishes.csv` file downloaded from Google Drive.
- Restaurant information collected from the Kharjet Tunisia website.

The data is processed, converted into embeddings using Google Gemini, and stored in the `restaurant_knowledge` Supabase vector table.

### 2. User interaction

The user sends a message through the n8n chat trigger. The Restaurant & Meal Planning Agent uses Gemini and conversation memory to understand the request and decide which tools are needed.

### 3. Restaurant search and recommendations

The agent searches the Supabase knowledge base for relevant restaurant information. It uses the available information to tailor recommendations to the user's preferences and constraints. Missing details should not be invented.

### 4. Weather checks

When the dining plan depends on weather, the agent can use OpenWeatherMap to retrieve current weather information for the relevant city.

### 5. Email and calendar tools

When requested by the user, the agent can:
- Send restaurant recommendations using Gmail.
- Create a Google Calendar event for a dining plan and invite the user by email.

The assistant should confirm the relevant details before scheduling an event and request the user's email address if it is not already known.

## Requirements

Before running the workflow, configure the required services and credentials in n8n:

- Google Gemini API
- Supabase
- Firecrawl
- Google Drive
- OpenWeatherMap
- Gmail OAuth2
- Google Calendar OAuth2

You also need the Supabase `restaurant_knowledge` table and the retrieval functions configured to match the workflow settings.

## Setup

1. Install or open an n8n instance.
2. Import the exported workflow JSON file into n8n.
3. Reconnect each required credential in your n8n instance.
4. Configure the Supabase vector store and retrieval functions used by the workflow.
5. Make sure the Google Drive CSV file is accessible to the configured account.
6. Run the knowledge-ingestion workflow to populate the restaurant knowledge base.
7. Open the chat workflow and test it with restaurant and meal-planning questions.

Credential connections are not transferred as usable secrets when a workflow is exported. They must be configured in your own n8n instance.

## Example Requests

- Recommend restaurants in Tunis for a group of four within my budget.
- Find restaurants that offer vegetarian dishes.
- Help me plan an outdoor dinner and check the weather for the date.
- Email me the restaurant recommendations.
- Add the selected dining plan to my Google Calendar.

## Security

Do not commit API keys, access tokens, OAuth secrets, passwords, or other sensitive credentials to this repository. Configure credentials securely in n8n.

## Project Status

This repository contains the exported n8n workflow for the Restaurant and Meals Planning assistant. Successful execution depends on configuring the required credentials and services.

## Author

Created as a practical project exploring AI agents, Retrieval-Augmented Generation (RAG), and workflow automation with n8n.
