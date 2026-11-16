# To-do list architecture

## Problem and constraints

Design a small to-do app to add, view, and complete tasks, retaining them when users return. Assume few users; authentication and large-scale design are out of scope.

## Attempt 1

Justin diagrammed task-list, add-task, and update-task flows using browser local storage. The diagram shows an `app_tasks` key, adding to a task array, looking up a task by ID, setting `completed: true`, and returning to the list with a status message. He noted the list would be small and suggested filtering.

[Attempt diagram](attempt.png) (screenshot of the visible canvas; the top is partly obscured by the toolbar).

**Score: 4/5.** The design addresses the three operations and persistence with an appropriately simple client-side choice. Its scope and update mechanics need clarification: local storage is per browser and device, and finding an item does not itself persist an update.

**Feedback:** State the same-browser assumption and explain the cross-device limitation. For completion, read and parse the array, find the task by ID, update it, serialize and save the array, then update the UI; handle a missing ID or failed save. Clarify that the boxes are client-side routes and that the storage boxes represent the same store. Avoid optimizing list rendering without evidence of a problem.

## Follow-up: Access from another device

Asked what happens on another device, Justin explained that its local storage is separate, so saved tasks would not appear. He proposed moving the storage structure to a remote web server backed by a relational database with users and tasks tables.

**Score: 4/5.** He correctly identified the limitation and proposed a suitable shared persistence architecture. The answer does not yet explain how the server identifies the user or associates and retrieves their tasks.

**Feedback:** Explain that tasks have an owner (for example, a `user_id` foreign key), and that the server needs a way to identify the current user before querying their tasks. Authentication was out of scope for the original prompt, but becomes relevant when accessing the same user's private data across devices. Outline how existing local tasks would be migrated if preserving them matters.

## Educator's summary

Justin has demonstrated the ability to map core user actions to a simple storage-based design and to consider completion state and user feedback. His follow-up correctly identified local storage's device limitation and proposed shared server-side persistence. The full update operation and user identification remain uncertain.

2026-11-16 — Evaluator: gpt-6.1-terra
