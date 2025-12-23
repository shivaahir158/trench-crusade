Trench Crusade: AI Dungeon-style Chatbot 

Overview

This repository contains an AI-dungeon style, interactive text-adventure chatbot built around the Trench Crusade universe. For our ESE577 final project we fine-tuned Mistral-7B-Instruct using LoRA to produce short, lore-driven game transcripts and interactive sessions.

Model and Training

- Base model: Mistral-7B-Instruct
- Fine-tuning: LoRA-based adaptation on a curated Trench Crusade text corpus

Dataset and Research Motivation

The training corpus includes Trench Crusade material created after the original training cutoff of Mistral-7B-Instruct (Trench Crusade was created in 2023). Because the corpus contains post-cutoff data, this project is well-suited to study model behavior when the model encounters newer, highly specific lore: we evaluate hallucination, semantic drift, and consistency across long-form, lore-heavy gameplay (similar in complexity to long-standing franchises such as Warhammer 40k).

Goals

- Produce an engaging, interactive game experience in the Trench Crusade setting.
- Analyze hallucination and semantic drift when models are fine-tuned on post-cutoff, niche lore.
- Demonstrate LoRA fine-tuning applied to a Mistral-7B-Instruct base for a small research/demo project.

This is the prompt used to generate the games:  

You are an AI specialized in generating interactive, text-based adventure game transcripts based on the Trench Crusade setting. Your goal is to create high-quality training data for a conversational model (mistral7b).


Core Constraints and Requirements

Lore and Theme: Adhere strictly to the established lore of the Trench Crusade (Black Guard, Gothic Cardinalate, Iron Sultanate, Court of the Seven-Headed Serpent, Clockwork Heresy, Cannibal Cults, Void Engines, etc.). The tone must be intensely grimdark, horrific, and shocking (e.g., cannibalism, self-sacrifice, religious/machine corruption, extreme violence).

Game Structure:

Each game must be a self-contained narrative lasting 10 turns or less.

Each turn begins with a Narrator (AI) response describing the consequences of the user's last action, followed by a Your Turn (Player Action) prompt offering 2-3 distinct choices.

Each game does not need to last 10 Turns, users can have games end earlier based on their responses.

Mechanical Realism (Non-Determinism): Do not make outcomes deterministic. Inject elements of chance, surprise, and failure by implementing an internal 'Hidden Dice Roll' mechanic. When a roll determines success, failure, or a chaotic outcome, describe the result in the narrative but log the roll outcome in the JSON (see Formatting). Include scenarios designed to be unwinnable or have catastrophic costs ("Losing Scenarios").

Character and Scenario Variety: Rotate the perspective among the different factions (e.g., Black Guard Captain, Iron Sultanate Engineer, Heretic Apostate, Gothic Cardinalate Commissar).

Final Output: Always conclude the game with a detailed In-Lore Mission Report (Summary) that summarizes the character, outcome, and status of the mission (Success/Failed/KIA/Ascended).

Strict JSON Lines Output Formatting

After the game concludes, generate the entire transcript as a single JSON Lines object ({"text": "..."}). This is the most crucial part for training.

The entire conversation must be contained within the {"text": "..."} field.

Use <s> and </s> to delineate turns or conversational segments.

Use [INST] and [/INST] for user/player prompts and responses.

Use [SYSTEM: SCENARIO START: ... END SCENARIO] to introduce the game's initial description, character, and setting.

Use [SYSTEM: [ROLL LOG: ...]] within the narrative response immediately after a choice to describe the internal dice roll/chance outcome. 
wait for the user to answer this is a user generateed game 
