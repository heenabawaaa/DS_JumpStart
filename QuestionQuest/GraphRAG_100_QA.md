# Graph RAG — 100 Questions & Answers
### From Beginner to Expert (with follow-up "counter-questions" and real-world scenarios)

> **How to read this file:** Every answer is written as if you have *never* studied graphs, databases, or AI internals before. Whenever an answer introduces a new idea (like "embeddings" or "community detection"), a small **🔁 Follow-up Question** is added right after it to dig one level deeper — because one good question always hides another. Questions marked **🎯 Scenario** describe a real situation you might face at work, instead of asking for a plain definition.
>
> **Difficulty flow:** Part 1 = Beginner (Q1–35) → Part 2 = Intermediate (Q36–70) → Part 3 = Expert (Q71–100).

---

## Part 1 — Beginner Level (Q1–Q35)
*Goal: build a mental picture of what a "graph" even is, before touching AI at all.*

---

**Q1. What is a graph, in the simplest possible terms?**
A graph is just a way of drawing "things" and "how they connect." Imagine a piece of paper where you draw circles for people you know, and you draw a line between two circles if those two people are friends. That's a graph. The circles are called **nodes** (or "entities"), and the lines are called **edges** (or "relationships"). Nothing more mysterious than a friendship map.

🔁 **Follow-up: Is a graph the same as a chart, like a bar chart?**
No — a "chart" in the everyday sense (bar chart, pie chart) shows *numbers*. A "graph" in computer science shows *connections*. It's an unfortunate naming overlap; in this document, "graph" always means the network-of-dots-and-lines kind.

---

**Q2. What is a node?**
A node is one single "thing" in your graph — a person, a company, a product, a city, a medicine, anything you can name. Think of it as one sticky note on a wall.

---

**Q3. What is an edge?**
An edge is the line connecting two nodes, and it usually has a *label* describing the relationship — like "works at," "married to," "located in," or "causes." If nodes are sticky notes, an edge is the piece of string you tape between two notes, with a small tag on it explaining *why* they're connected.

---

**Q4. What is RAG (Retrieval-Augmented Generation)?**
RAG is a technique where an AI model, before answering your question, first goes and *fetches* relevant information from an external source (like a document library), and then uses that fetched information to write its answer. It's like an open-book exam: instead of relying purely on memory, the AI is allowed to flip through reference material first.

🔁 **Follow-up: Why not just let the AI answer from memory alone?**
Because a language model's memory is frozen at training time and can be wrong or outdated. Giving it fresh, specific documents to read before answering reduces made-up facts ("hallucinations") and lets it answer about things it was never trained on, like your company's private files.

---

**Q5. So what is Graph RAG?**
Graph RAG is RAG's cousin that uses a **graph** (nodes + edges) as the reference material instead of, or in addition to, plain text documents. Rather than handing the AI a pile of loose paragraphs, you hand it a connected map of facts — so it can "walk" from one fact to a related fact, the way you'd trace a family tree with your finger.

---

**Q6. How is Graph RAG different from regular (plain-text) RAG?**
Plain RAG chops documents into small chunks of text and finds chunks that *sound similar* to your question. Graph RAG instead stores facts as connected nodes and edges, so it can find information that is *related by meaning or structure*, even if the wording is completely different. Plain RAG is like searching a pile of index cards for similar sentences; Graph RAG is like following a trail of labeled string between index cards.

🔁 **Follow-up: What does "chunking" mean in plain RAG?**
Chunking means slicing a long document into smaller pieces (say, 300–500 words each) so the system can search and retrieve manageable bits of text instead of whole books at once.

---

**Q7. Why would anyone need graphs instead of just plain text search?**
Because many real questions aren't about *matching words* — they're about *following relationships*. Example: "Which of our suppliers are indirectly affected by the factory fire in Vietnam?" You can't answer that by searching for the words "factory fire." You need to trace: factory → supplies parts to → Company A → is a supplier of → Company B, and so on. Graphs are built exactly for that kind of tracing.

---

**Q8. What is a "knowledge graph"?**
A knowledge graph is a large graph built specifically to store real-world facts and how they relate — for example, "Paris — is capital of → France," "France — is located in → Europe." It's essentially an organized, connected fact-base that both humans and machines can query.

🔁 **Follow-up: Who builds knowledge graphs?**
They can be built by hand (experts typing in facts), automatically (AI reading documents and extracting facts), or a mix of both — automatic extraction followed by human review.

---

**Q9. What does "entity" mean in this context?**
"Entity" is just a more formal word for "node" — a distinct real-world thing: a person, place, organization, event, or concept that deserves its own dot on the graph.

---

**Q10. What does "relationship" or "relation" mean?**
It's the formal word for "edge" — the labeled connection between two entities, such as "founded," "treats," "part of," or "competes with."

---

**Q11. What is "retrieval" in RAG?**
Retrieval is simply the act of *searching and fetching* the pieces of information the AI will need to answer your question — before it writes anything. Think of a librarian who runs to the shelves and brings back the three most relevant books before you start reading.

---

**Q12. What is "generation" in RAG?**
Generation is the AI actually writing the final answer, using both your question and the retrieved material as its writing material. It's the "essay writing" step after the "research" step (retrieval) is done.

---

**Q13. Why is it called "augmented" generation?**
Because the AI's own built-in knowledge is being *augmented* (boosted, supplemented) with freshly retrieved outside information, rather than the AI answering from memory alone.

---

**Q14. What is a Large Language Model (LLM) in one sentence?**
An LLM is a computer program trained on huge amounts of text that has learned patterns of language well enough to read, summarize, and write human-like responses — think of it as an extremely well-read assistant that predicts the most sensible next words to write.

---

**Q15. Why do LLMs "hallucinate," and how does Graph RAG help?**
LLMs generate text by predicting likely-sounding words, not by looking facts up in a database — so when they don't actually know something, they can still produce a confident, fluent, but *wrong* answer. That's a hallucination. Graph RAG helps because it forces the model to ground its answer in real retrieved facts from the graph, similar to asking someone to point at the actual line in a document that supports their claim, rather than just trusting their memory.

🔁 **Follow-up: Does Graph RAG eliminate hallucination completely?**
No — it greatly reduces it by grounding answers in retrieved facts, but the model can still misinterpret or slightly misstate what the graph told it. Good system design (citing the exact node/edge used) reduces this further but doesn't remove it entirely.

---

**Q16. What is a "vector" or "embedding," in beginner terms?**
An embedding is a way of turning a piece of text (a word, sentence, or paragraph) into a list of numbers that captures its *meaning*, so that texts with similar meaning end up with similar number-lists. Imagine plotting every word on a giant map where "king" and "queen" naturally land close together, while "banana" lands far away — the embedding is just that word's coordinates on the map.

🔁 **Follow-up: Why do we need embeddings at all if we have graphs?**
Because embeddings are what let the system find text that is *similar in meaning* even if it doesn't share exact words — this is useful for the initial retrieval step, and many Graph RAG systems combine embeddings (for fuzzy matching) with graph traversal (for precise relationship-following).

---

**Q17. What is a "vector database"?**
It's a specialized storage system built to hold millions of these number-lists (embeddings) and quickly find the ones that are "closest" (most similar in meaning) to a new query — like a librarian who can instantly find every book with a similar "vibe" to the one you're holding, not just the same title.

---

**Q18. What is a "graph database"?**
It's a specialized storage system built to hold nodes and edges directly (instead of forcing them into rows and tables), so that "find everything connected to X" is a fast, natural operation instead of a slow, complicated one. Neo4j and Amazon Neptune are well-known examples.

---

**Q19. How is a graph database different from a normal (relational/SQL) database?**
A normal database is like a set of neatly organized spreadsheets (tables) with rows and columns; finding a connection between two far-apart pieces of data often means stitching together several tables ("joins"), which gets slow and messy as things get more connected. A graph database stores the *connections themselves* as first-class citizens, so tracing a chain of relationships (A knows B, B works with C, C is based in D) is quick and natural, not a chore.

---

**Q20. What is "knowledge graph construction"?**
It's the process of *building* the graph in the first place — reading through documents, pulling out entities (people, places, things) and relationships between them, and storing those as nodes and edges. This is often the hardest and most important part of any Graph RAG project.

🔁 **Follow-up: Who or what does this extraction — a human or a machine?**
Both are possible. Small, high-stakes graphs (like medical or legal ones) are often built or checked by human experts. Large graphs are usually built automatically by an LLM reading through documents and proposing entities/relationships, sometimes followed by human review of the most important parts.

---

**Q21. What does "unstructured data" mean, and why does it matter here?**
Unstructured data is information that isn't neatly organized into rows and columns — things like emails, PDFs, meeting notes, or web pages, where facts are buried inside free-flowing sentences. Most of the world's information is unstructured, which is exactly why Graph RAG systems need a step to *extract* structured facts (nodes and edges) out of all that messy text.

---

**Q22. 🎯 Scenario: Your manager hands you a folder of 500 unorganized PDFs (contracts, emails, reports) and says, "Turn this into something our AI assistant can actually answer questions about." What's the very first step?**
Gather and prepare those source documents, then feed them to an LLM (or a rule-based tool) whose job is to read each piece of text and pull out "Entity A — relationship — Entity B" triples. This turns messy paragraphs into structured graph pieces — the very first brick of the whole Graph RAG system, before any retrieval or answering logic even comes into play.

---

**Q23. What is a "triple"?**
A triple is the smallest unit of graph knowledge: (Subject, Relationship, Object) — for example, (Marie Curie, discovered, Radium). Two nodes and the edge connecting them, written as one neat sentence-like unit.

---

**Q24. What is "traversal" in a graph?**
Traversal simply means "walking" from one node to another by following edges — like using your finger to trace a path on a subway map, going station to station along the connecting lines.

---

**Q25. What is a "path" in a graph?**
A path is the specific sequence of nodes and edges you passed through while traversing — for example, Alice → (friends with) → Bob → (works at) → Acme Corp is a 2-step path from Alice to Acme Corp.

---

**Q26. What is a "neighbor" node?**
A neighbor is any node directly connected to a given node by one edge — Bob's neighbors are everyone he's directly linked to (friends, employer, city he lives in), without needing to hop through anyone else first.

---

**Q27. What does "1-hop" or "2-hop" mean?**
A "hop" is one jump across a single edge. A 1-hop neighbor is directly connected; a 2-hop neighbor is connected through exactly one other node in between (a friend-of-a-friend). Graph RAG systems often let you control how many hops away from your starting point the system is allowed to explore.

---

**Q28. What is a "subgraph"?**
A subgraph is a smaller slice cut out of a much bigger graph — for instance, "just the nodes and edges within 2 hops of 'Diabetes'" instead of the entire medical knowledge graph. Retrieval in Graph RAG is often really about pulling out the *right small subgraph* to hand to the AI.

---

**Q29. Why can't you just hand the AI the entire graph every time?**
Because real-world graphs can have millions of nodes and edges, and an LLM can only read a limited amount of text at once (its "context window"). Handing it everything would be like asking someone to read an entire encyclopedia before answering one question — slow, expensive, and mostly irrelevant to what was actually asked.

🔁 **Follow-up: What is a "context window"?**
It's the maximum amount of text an LLM can consider at one time when generating a response — measured in "tokens" (roughly word-pieces). If the retrieved information is bigger than this window, it has to be trimmed or summarized before being handed to the model.

---

**Q30. What does "grounding" mean in AI answers?**
Grounding means tying the AI's statements to actual retrieved evidence — real facts from the graph or documents — instead of letting it freely invent things. A well-grounded answer can point to exactly which node/edge or document it used to justify each claim.

---

**Q31. 🎯 Scenario: You're a support agent and a customer asks, "Which of my orders were affected by the shipping delay in Port X last week?" Why would Graph RAG answer this better than a plain text search?**
Because this question requires *connecting* three different facts: which orders belong to this customer, which shipments those orders were part of, and which shipments passed through Port X during the delay window. A plain keyword search for "Port X delay" would only find documents mentioning that phrase — it wouldn't know which specific orders are linked to it. A graph can walk: Customer → Orders → Shipments → Port X → Delay Event, and return the precise, correct list.

---

**Q32. What is meant by "structured" vs. "semi-structured" vs. "unstructured" data?**
Structured data lives neatly in tables (spreadsheets, databases). Unstructured data is free-form text or media (emails, PDFs, images) with no fixed layout. Semi-structured data is in between — it has some organization (like tags in a webpage or fields in a JSON file) but isn't as rigid as a table. Graph RAG typically turns unstructured and semi-structured data into structured graph facts.

---

**Q33. What is a "schema" for a graph?**
A schema is the "rulebook" describing what *types* of nodes and edges are allowed — for example, "a Person can WORK_AT a Company," "a Drug can TREAT a Disease." It keeps the graph organized and prevents nonsense connections, similar to how a form with labeled fields (Name, Age, Address) keeps data organized compared to a blank sheet of paper.

🔁 **Follow-up: Does every Graph RAG system require a fixed schema?**
No — some systems use a flexible/open schema where the LLM decides relationship types freely during extraction (more coverage, less consistency), while others enforce a strict predefined schema for cleaner, more reliable graphs (less coverage, more consistency). This is a real design trade-off.

---

**Q34. What is meant by "explainability" of an AI answer, and how do graphs help?**
Explainability means being able to show *why* the AI gave a particular answer — which facts or reasoning steps led there. Because a graph stores explicit paths between facts, a Graph RAG system can literally show you the chain of nodes and edges it followed (e.g., "Drug A → interacts with → Drug B → is prescribed for → your condition"), giving a transparent trail instead of a black-box answer.

---

**Q35. In one sentence, what problem is Graph RAG ultimately trying to solve?**
It's trying to give AI systems the ability to answer questions that require *connecting multiple, related facts across many documents* — accurately, transparently, and without needing the answer to already exist word-for-word in a single paragraph somewhere.

---

## Part 2 — Intermediate Level (Q36–Q70)
*Goal: understand how Graph RAG systems are actually built and where the hard engineering decisions live.*

---

**Q36. What are the main stages of a typical Graph RAG pipeline?**
Generally: (1) **Ingestion** — collect raw documents; (2) **Extraction** — use an LLM or NLP tool to pull entities and relationships (triples) out of the text; (3) **Graph construction** — store those triples as nodes/edges in a graph database, often merging duplicates; (4) **Indexing** — build helper structures (like embeddings or community summaries) so retrieval is fast; (5) **Retrieval** — given a user's question, pull the relevant subgraph or facts; (6) **Generation** — feed that subgraph plus the question to an LLM to write the final answer.

---

**Q37. What is "entity resolution" (also called "entity linking" or "deduplication")?**
It's the process of realizing that "Apple Inc.," "Apple," and "Apple Computer" all refer to the *same* real-world entity, and merging them into one node instead of three separate, disconnected ones. Without this step, your graph fills up with duplicate nodes that don't "know" they're the same thing, and traversal quietly breaks.

🔁 **Follow-up: How is entity resolution actually done in practice?**
Common approaches include comparing name similarity (string matching), comparing embeddings of surrounding context, or asking an LLM directly, "Are these two mentions referring to the same entity?" — often combined with a human review step for high-stakes graphs.

---

**Q38. What is "co-reference resolution"?**
It's figuring out that words like "he," "she," "it," or "the company" in a sentence refer back to a specific entity mentioned earlier — for example, resolving "Marie Curie... She later won a Nobel Prize" so that "She" is correctly linked to "Marie Curie" and not treated as a separate, mystery entity.

---

**Q39. What is "community detection" in graphs?**
It's an algorithm that automatically groups nodes into clusters ("communities") that are more densely connected to each other than to the rest of the graph — similar to how a school's friendship graph naturally splits into "the chess club," "the soccer team," etc., just by looking at who talks to whom most.

🔁 **Follow-up: Why does Graph RAG care about communities?**
Because you can pre-generate a short *summary* for each community (e.g., "this cluster of nodes is about the company's European supply chain"), which lets the system answer broad, high-level questions quickly by reading summaries instead of thousands of individual facts. This is the core idea behind Microsoft's "GraphRAG" approach.

---

**Q40. What is the difference between "local" and "global" search in Graph RAG?**
Local search answers specific, narrow questions by pulling a small, focused subgraph around one or two entities (e.g., "What medications does Drug X interact with?"). Global search answers broad, thematic questions that require understanding the *whole* dataset's big picture (e.g., "What are the main themes in these 10,000 customer complaints?") — usually by reading community summaries rather than individual facts, since no single subgraph could cover such a broad question.

---

**Q41. What is a "knowledge graph embedding"?**
It's a technique that converts entire nodes and edges (not just text) into number-lists (vectors) based on their position and role in the graph's structure — so two nodes that play a *similar structural role* end up close together numerically, even if they're never directly connected. This helps with tasks like predicting missing links or finding structurally similar entities.

---

**Q42. What is "hybrid retrieval"?**
It's combining two or more retrieval methods together — most commonly, vector/embedding search (finds text that *sounds* similar) plus graph traversal (finds facts that are *structurally* connected) — because each method catches things the other misses. It's like using both a search engine and a family tree to answer "how is this person related to that historical event."

---

**Q43. What is a "cypher query" (or graph query language in general)?**
It's a specialized language used to ask a graph database precise questions, similar to how SQL is used to query regular databases. Cypher (used by Neo4j) lets you write patterns like "find a Person who WORKS_AT a Company that IS_LOCATED_IN a City" in a fairly readable, visual-looking syntax.

🔁 **Follow-up: Does the end user need to know Cypher to use Graph RAG?**
No — in most Graph RAG systems, the LLM itself is prompted to translate the user's natural-language question into the query language behind the scenes (this is sometimes called "text-to-Cypher" or "text-to-query"), so the human never has to write graph queries directly.

---

**Q44. What does "text-to-Cypher" (or "text-to-graph-query") mean?**
It means using an LLM to automatically translate a plain-English question into a formal graph database query, so that non-technical users can simply ask a question in normal language and have the system figure out the technical query underneath.

---

**Q45. What is a "multi-hop question"?**
It's a question whose answer requires chaining together more than one fact/relationship, rather than being answered by a single lookup. Example: "Who is the CEO of the company that acquired the startup founded by my old colleague?" requires hopping: colleague → founded → startup → was acquired by → company → CEO is → answer. This is exactly the kind of question graphs excel at.

---

**Q46. 🎯 Scenario: A pharmaceutical researcher asks, "What are all the known drug interactions, two steps removed, from Drug A?" How would a Graph RAG system approach this?**
It would start at the "Drug A" node, retrieve its direct (1-hop) interaction partners, then continue outward to *their* interaction partners (the 2-hop layer), collecting that entire subgraph. This subgraph — not the whole drug database — gets handed to the LLM, which then summarizes the chains of interaction in plain language, ideally citing each hop so the researcher can verify the path.

---

**Q47. What is "chunk-to-graph linking"?**
Even in a Graph RAG system, you often still keep the original text chunks (the exact sentences a fact came from) linked to the graph nodes they mention. This way, when a node is retrieved, the system can also pull up the *exact source sentence* as supporting evidence — combining the precision of a graph with the verifiability of the original text.

---

**Q48. What is "GraphRAG" (capital-R, as coined by Microsoft Research)?**
It refers to a specific published approach (2024) where an LLM extracts entities/relationships from documents to build a knowledge graph, then runs community detection to cluster related nodes, generates a short summary for each community and each higher-level cluster, and uses those summaries to answer broad "what are the main themes" style questions far better than plain-text RAG can. It's one well-known implementation of the general "Graph RAG" idea, not the only one.

---

**Q49. What is a "property graph"?**
It's a graph model where nodes and edges can carry extra *attributes* (properties), not just labels — for example, a "Person" node might have properties like age=34, city="Berlin," while a "WORKS_AT" edge might have a property like since=2019. Most modern graph databases (like Neo4j) use this property-graph model because it's flexible and expressive.

---

**Q50. What is "RDF" (Resource Description Framework)?**
RDF is an older, standardized way of representing graph facts strictly as (subject, predicate, object) triples, commonly used in academic and semantic-web knowledge graphs (like Wikidata or DBpedia). It's stricter and more standardized than a property graph, but less flexible for attaching rich attributes directly onto relationships.

🔁 **Follow-up: RDF vs. property graph — which does Graph RAG usually use?**
Both exist in practice. Property graphs (Neo4j-style) are more common in newer, LLM-driven Graph RAG projects because they're easier to work with and query; RDF/triple stores are more common in long-established enterprise or academic knowledge graphs.

---

**Q51. What is "PageRank," and why does it come up in graph discussions?**
PageRank is a famous algorithm (originally built for Google Search) that scores nodes by importance based on how many *other important nodes* point to them — think of it as "a node is important if important nodes vouch for it." Graph RAG systems sometimes use PageRank-style scoring to rank which retrieved nodes/facts are most central or trustworthy before showing them to the LLM.

---

**Q52. What is "graph pruning"?**
It's the process of trimming away less-relevant nodes and edges from a retrieved subgraph before sending it to the LLM — removing noise so the model focuses on what matters, similar to cutting the excess branches off a bouquet before handing it to someone.

---

**Q53. What is "re-ranking" in a retrieval pipeline?**
After an initial (often fast but rough) retrieval step pulls back a batch of candidate facts or documents, a re-ranker is a second, more careful model that re-orders those candidates by true relevance to the question — like a first-round intern who quickly grabs 50 possibly-relevant files, followed by an expert who reads them properly and picks the best 5.

---

**Q54. What is a "context window overflow," and how does Graph RAG try to avoid it?**
This happens when the amount of retrieved information (subgraph facts, text chunks) exceeds what the LLM can read in one go. Graph RAG systems avoid it by being selective — pruning subgraphs, summarizing communities in advance, ranking and keeping only the top-K most relevant facts, or compressing facts into terse triples instead of full sentences.

---

**Q55. What does "K" mean when people say "top-K retrieval"?**
K is just the *number* of items you choose to retrieve — "top-5" means the 5 most relevant results, "top-20" means the 20 most relevant. Choosing K is a balancing act: too small and you might miss important facts; too large and you overload the LLM's context window with noise.

---

**Q56. What is "latency" in this context, and why does graph traversal sometimes add it?**
Latency is the delay between asking a question and getting an answer. Graph traversal can add latency because walking multiple hops across a large graph, especially with several rounds of relevance filtering, takes real computation time — more so than a single quick embedding-similarity lookup. System designers often cache common queries or pre-compute summaries to reduce this.

---

**Q57. 🎯 Scenario: Your company's Graph RAG system was built six months ago, but every week there are new contracts, new hires, and new customer tickets. Do you have to rebuild the whole graph from scratch each week?**
No — this is exactly what "incremental graph updates" solves: the ability to add new facts (new documents, new events) into an existing graph without rebuilding it entirely, so the system stays current as new information (this week's tickets, today's news) keeps arriving.

🔁 **Follow-up: Why is this harder than it sounds?**
Because new information might contradict old information (a person changed jobs), might refer to entities already in the graph under different names (needing entity resolution again), and might affect pre-computed summaries (like community summaries) that now need to be regenerated.

---

**Q58. What is "temporal reasoning" in a knowledge graph?**
It's the ability to represent and reason about *when* a fact was true — because facts change over time (someone's job, a company's CEO, a drug's approval status). Some graphs attach time stamps or valid-from/valid-to properties to edges so the system can answer "who was the CEO in 2020?" differently from "who is the CEO now?"

---

**Q59. What is "graph visualization," and is it required for Graph RAG to work?**
It's simply drawing the graph out visually (dots and lines on a screen) so humans can inspect it. It's not required for the AI system to function — the AI reads structured data, not pictures — but it's extremely useful for developers and analysts to debug, validate, and trust the graph they've built.

---

**Q60. 🎯 Scenario: An e-commerce company wants to answer "Which customers who bought Product A are most likely to also want Product B, based on what similar customers bought?" How does graph structure help here compared to a simple recommendation table?**
A simple table can tell you "people who bought A also bought B" as one flat statistic, but a graph can capture *richer, multi-step relationships* — customer-to-purchase, purchase-to-product, product-to-category, customer-to-customer similarity — and can factor in things like shared categories, shared other purchases, or even social/referral connections between customers. The graph lets the retrieval step assemble a nuanced, explainable "neighborhood" of related customers and products rather than a single blunt correlation number.

---

**Q61. What is "query decomposition"?**
It's breaking one complicated question into several smaller sub-questions before retrieval — for example, splitting "Compare the revenue growth of our top 3 competitors last year" into three separate lookups (one per competitor), retrieving facts for each, and then combining the results into a single coherent answer.

---

**Q62. What is a "reasoning chain" or "chain of thought" in an LLM's answer?**
It's the step-by-step logical path the model follows to reach a conclusion, ideally shown explicitly ("First I found X, which led to Y, which means Z"), rather than a single leap straight to the final answer. In Graph RAG, this chain often mirrors the actual graph traversal path, making the answer more trustworthy and checkable.

---

**Q63. What is "provenance" in the context of graph facts?**
Provenance means keeping track of *where a fact came from* — which document, page, or source produced this specific node or edge — so that later, both humans and the AI can verify or trace a claim back to its origin, rather than treating the graph as an unquestionable oracle.

---

**Q64. What is meant by "noise" in extracted graph data, and where does it come from?**
Noise means incorrect, low-quality, or irrelevant nodes/edges that sneak into the graph — often from extraction errors (the LLM misreading a sentence), ambiguous language, or genuinely low-quality source documents. Managing noise (through validation, confidence scores, or human review) is one of the biggest practical challenges in real Graph RAG projects.

---

**Q65. What is a "confidence score" on an extracted fact?**
It's a number (often produced by the extracting LLM or a separate scoring model) indicating how sure the system is that a given triple is actually correct — allowing downstream steps to prioritize high-confidence facts and flag or discard low-confidence ones.

---

**Q66. What is the difference between "ontology" and "schema"?**
They're closely related, but an ontology is usually the richer, more formal version — it doesn't just say *what types* of nodes/edges exist (which is the schema's job), but also defines the *rules and meaning* behind them, like "if A is a parent of B, then B cannot also be a parent of A." Think of schema as the form's field labels, and ontology as the full rulebook describing what those fields logically mean and how they interact.

---

**Q67. What is "graph-based summarization"?**
It's using the graph's structure (like clusters/communities) to produce summaries of large amounts of information — for example, summarizing "everything connected to Topic X" by walking its subgraph and asking the LLM to write a paragraph describing the key entities and relationships found, instead of summarizing raw, unstructured paragraphs directly.

---

**Q68. What is the role of an LLM *during* graph construction, versus its role during answering?**
During construction, the LLM acts as an "information extractor" — reading raw text and proposing structured facts (entities, relationships) to add to the graph. During answering, the LLM acts as a "writer/reasoner" — taking a retrieved subgraph plus the user's question and composing a natural-language answer. Same technology, two very different jobs within the pipeline.

---

**Q69. 🎯 Scenario: Your finance team asks why the "one-time knowledge graph build" line item is far more expensive than the "monthly querying" line item on your AI project's budget. How do you explain this?**
"Cost" here refers mainly to money and compute spent on LLM calls (since extraction, entity resolution, and summarization can involve many LLM calls per document) plus infrastructure for storing and querying the graph and any vector index. Building the graph upfront — especially with community summarization — tends to be the most expensive one-time step, while day-to-day querying afterward is comparatively cheap, which is exactly the pattern showing up on that budget line.

---

**Q70. What is "evaluation" of a Graph RAG system, and what does it typically measure?**
Evaluation means systematically testing whether the system gives correct, complete, and well-grounded answers — usually measured along axes like *faithfulness* (did the answer stick to retrieved facts, without inventing anything?), *relevance* (did retrieval find the right subgraph?), and *completeness* (did the answer cover everything the graph actually knew?). Good evaluation usually needs a curated set of test questions with known correct answers.

---

## Part 3 — Expert Level (Q71–Q100)
*Goal: the deeper design trade-offs, failure modes, and advanced techniques professionals wrestle with.*

---

**Q71. What is the fundamental trade-off between "open schema" and "closed schema" extraction in large-scale Graph RAG construction?**
A closed (predefined) schema constrains the LLM to only emit relationship types you've pre-approved (e.g., only "WORKS_AT," "FOUNDED," "ACQUIRED"), producing a clean, consistent graph that's easy to query reliably — but it can miss important relationships that don't fit the predefined list. An open schema lets the LLM invent whatever relationship label seems natural from the text, capturing far richer nuance — but produces messy near-duplicate labels ("works for," "employed by," "works at" all meaning the same thing), which then requires a relationship-normalization step to clean up before the graph is usable at scale.

🔁 **Follow-up: How do practitioners usually resolve this trade-off?**
A common middle ground is to start with open-schema extraction to see what naturally emerges from the data, then cluster/normalize the resulting relationship types (often using embeddings of the relation labels themselves) into a smaller, cleaner closed set, which becomes the schema going forward.

---

**Q72. Why does entity resolution become dramatically harder at enterprise scale, and what techniques address this?**
At small scale, you might have a few hundred entities and can eyeball duplicates. At enterprise scale (millions of entities), ambiguity explodes: is "J. Smith" in document A the same "John Smith" in document B, or a different person entirely? Techniques include blocking (only comparing entities that share some cheap-to-compute signature, to avoid comparing every pair — which would be computationally explosive), embedding-based similarity search to find candidate matches, LLM-based pairwise or clustered adjudication for ambiguous cases, and maintaining canonical entity IDs with alias lists rather than merging too aggressively (which risks incorrectly combining two different real people).

---

**Q73. What is "the blocking problem" in entity resolution, and why does it matter computationally?**
If you have N entities and naively compare every pair to check "are these the same?", you get roughly N²/2 comparisons — for a million entities, that's around 500 billion comparisons, computationally infeasible. Blocking solves this by first grouping entities into smaller candidate buckets (e.g., same first letter of name, same rough embedding neighborhood) and only comparing within each bucket, cutting the comparison count down by orders of magnitude while still catching almost all true duplicates.

---

**Q74. Why is naive full-graph traversal a bad retrieval strategy for large, densely connected graphs, and what is the "hairball problem"?**
In a dense, highly-connected real-world graph (think: a corporate graph where every employee is connected to the same "HR Policy" node, or a social graph with a few extremely popular hub nodes), a small number of hops can explode into touching millions of nodes almost immediately — this is sometimes informally called the "hairball problem," where the graph is so densely tangled that naive traversal returns an unmanageable, mostly-irrelevant mass instead of a focused answer. Solutions include hop-limited traversal with relevance-based pruning at each step, excluding known "super-hub" nodes from broad traversal, and relying more on pre-computed community summaries for broad questions instead of raw traversal.

---

**Q75. What is the difference between "global" GraphRAG-style community summarization and "local" ad-hoc subgraph retrieval, from a system-design perspective?**
Community summarization is done *offline, in advance*: the whole graph is clustered into communities (often hierarchically, coarse clusters containing finer sub-clusters), and an LLM writes a summary for each cluster once, up front — this is expensive to compute but cheap and fast to query later, and it's ideal for broad, thematic questions covering large swaths of the dataset. Local subgraph retrieval is done *online, per query* — walking outward from specific entities mentioned in the question — which is cheap to set up in advance but must do real traversal work at query time, and it's ideal for narrow, specific, entity-centered questions. Production systems often combine both: route "what are the themes" questions to community summaries, and "tell me about X" questions to local traversal.

---

**Q76. What is "query routing" in a Graph RAG system, and why is it necessary?**
Query routing is an upfront classification step that decides *which retrieval strategy* (local traversal, global community summaries, plain vector search, or a hybrid) is best suited to the incoming question, before actually running retrieval. It's necessary because no single retrieval strategy is optimal for every question type — using expensive global summarization for a simple "what's Bob's phone number" lookup wastes resources, while using narrow local traversal for "summarize the main risks across all reports" would miss the big picture entirely.

---

**Q77. What is "hallucinated relationship extraction," and why is it particularly dangerous in Graph RAG (compared to plain-text RAG)?**
This is when the LLM, during graph construction, invents a relationship that isn't actually supported by the source text — e.g., inferring "Company A ACQUIRED Company B" from a sentence that only said they "partnered." It's especially dangerous in Graph RAG because that invented edge becomes a *permanent, structural* part of the graph that future queries will traverse and trust as fact, silently poisoning every future answer that touches it — versus plain-text RAG, where a bad retrieval is a one-off mistake limited to that single answer, not baked into a persistent structure.

🔁 **Follow-up: How can teams detect and control this risk?**
By requiring the extractor to cite the exact source sentence for every proposed triple (so it's auditable), using a second LLM or human pass to verify high-impact or high-confidence-claim edges, attaching confidence scores and filtering low-confidence ones, and periodically running consistency checks (e.g., flagging edges that contradict other trusted edges).

---

**Q78. What is "graph contradiction," and how should a well-designed system handle it?**
Contradiction happens when two extracted facts conflict — for example, one document says "Company X's CEO is Alice" and another (older or simply wrong) document says "Company X's CEO is Bob." A naive graph would just store both edges and confuse any query touching that node. Well-designed systems handle this by attaching provenance and timestamps to every edge (so the system can prefer the most recent or most authoritative source), by explicitly modeling "conflicting claim" as its own relationship type rather than silently overwriting, or by surfacing the contradiction to a human reviewer rather than silently picking one.

---

**Q79. What is "multi-hop retrieval noise accumulation," and why does it grow non-linearly with hop count?**
At each hop of traversal, there's some chance of pulling in an irrelevant or loosely-related node. Because each new hop expands out from *all* nodes found in the previous hop (not just one), the number of candidate nodes — and therefore the amount of noise — tends to grow multiplicatively rather than by a fixed amount per hop. This means going from 2-hop to 3-hop retrieval can flood the context window with far more irrelevant material than the jump from 1-hop to 2-hop did, which is why most production systems cap traversal depth tightly (often 2–3 hops) and apply relevance filtering *between* each hop rather than only at the end.

---

**Q80. 🎯 Scenario: A legal firm's Graph RAG system, when asked "What precedents support our client's position?", occasionally cites a case that sounds relevant but was actually overturned years later. What underlying design flaw likely caused this, and how would you fix it?**
This points to a missing temporal/status model on the graph's edges — the system likely has a "CASE cites PRECEDENT" edge but no property capturing that the precedent was later "OVERTURNED_BY" a newer ruling, and no logic during retrieval or generation that checks for this status before presenting a precedent as valid. The fix is twofold: at the schema level, explicitly model case status and overturning relationships as first-class edges (so "overturned" precedents are a queryable fact, not an omission); at the retrieval/generation level, require the system to check and surface a precedent's current status whenever it's cited, and to actively favor or flag based on that status rather than treating "cited in some document" as equivalent to "still good law."

---

**Q81. What is "graph sparsification," and why might you deliberately want a sparser graph?**
Graph sparsification means intentionally removing lower-value edges (based on confidence score, edge frequency, or importance ranking) to keep the graph smaller and faster to query, while retaining the structurally and semantically important connections. You'd want this because an overly dense graph — full of every trivial, low-confidence, or redundant relationship the extractor found — slows down traversal, dilutes relevance ranking, and increases the "hairball problem" risk discussed earlier, without adding proportional value to answer quality.

---

**Q82. What is the difference between "extractive" and "abstractive" grounding when the LLM generates its final answer from a retrieved subgraph?**
Extractive grounding means the model's answer sticks very closely to the literal retrieved facts, largely restating them (safer, more verifiable, but can read as stilted or incomplete for nuanced questions). Abstractive grounding means the model synthesizes, paraphrases, and connects the retrieved facts into new, fluent prose (more natural and often more useful for complex questions) — but this synthesis step is exactly where subtle hallucination risk creeps back in, since the model is doing more "creative" work rather than pure restatement. Production systems often aim for a controlled middle ground: abstractive phrasing, but with each claim traceable back to a specific extractive source.

---

**Q83. What is "graph-aware chunk retrieval," and how does it differ from pure text-chunk RAG?**
Instead of retrieving text chunks purely by embedding similarity to the question (pure text-chunk RAG), graph-aware chunk retrieval first identifies the relevant entities/subgraph for the question, then retrieves the *specific text chunks linked to those exact graph nodes* — meaning retrieval is guided by verified structural relevance, not just superficial semantic similarity. This tends to catch relevant chunks that plain embedding search would miss (because the chunk's wording doesn't closely resemble the question, even though it's structurally the right source) and filters out chunks that merely sound similar but are actually about an unrelated entity with similar phrasing.

---

**Q84. What is "GNN" (Graph Neural Network), and how does it relate to (but differ from) Graph RAG?**
A GNN is a type of machine learning model specifically designed to learn patterns *directly from graph structure* — it learns by having each node repeatedly "absorb" information from its neighbors over several rounds, ending up with a rich numerical representation of each node that reflects both its own properties and its neighborhood's structure. This is a different technology than the LLM-centric Graph RAG pipelines discussed throughout this document — GNNs are typically used for structural prediction tasks (like predicting missing links, or classifying nodes) rather than for natural-language question answering — though research increasingly explores combining GNN-derived node representations with LLMs to give the language model a richer sense of graph structure than text-based summaries alone can provide.

🔁 **Follow-up: Why isn't a GNN simply used instead of an LLM for Graph RAG's generation step?**
Because a GNN outputs numerical representations or structural predictions, not fluent natural language — it has no ability to *write* a coherent English answer explaining its reasoning. GNNs and LLMs are complementary: a GNN can enrich the numerical understanding of graph structure, while the LLM remains responsible for the final natural-language explanation to the user.

---

**Q85. What is "graph-based query decomposition planning," and how does an agentic Graph RAG system use it?**
This is a more advanced version of query decomposition (Q61) where, instead of a fixed, pre-scripted breakdown, the system uses an LLM acting as a "planner" to dynamically decide — based on the specific question and what it discovers along the way — which entities to explore first, whether to expand further based on intermediate findings, and when it has gathered enough evidence to stop. This turns retrieval into an iterative, multi-step reasoning loop ("agentic" retrieval) rather than a single fixed-shape query, which is especially valuable for open-ended, exploratory questions where the right traversal path isn't knowable in advance.

---

**Q86. What is the "closed-world vs. open-world assumption," and why does it matter for how a Graph RAG system should phrase uncertain answers?**
Under a closed-world assumption, anything *not* explicitly stated in the graph is assumed false ("if it's not in the graph, it didn't happen"). Under an open-world assumption, the absence of a fact in the graph simply means it's *unknown*, not necessarily false ("it might be true, we just haven't recorded it"). This matters enormously for how a Graph RAG system should word its answers: a well-designed system operating under the (much safer, more realistic) open-world assumption should say "I found no record of X in the available data" rather than the stronger, riskier claim "X is not true" — because the graph's incompleteness is not the same as the real world's non-existence of a fact.

---

**Q87. What is "link prediction," and how might it be used within a Graph RAG pipeline (rather than just as a standalone graph ML task)?**
Link prediction is the task of estimating which *missing* edges probably should exist in a graph but weren't explicitly extracted or stated — for example, predicting that Company A likely has a supply relationship with Company C, based on the structural pattern that both are heavily connected to Company B in similar ways. Within a Graph RAG pipeline, link prediction can be used to surface plausible-but-unconfirmed connections to a human reviewer for verification (helping fill genuine gaps in extraction), but it should almost never be silently added to the graph as if it were a confirmed fact — doing so would blur the critical line between "extracted from real evidence" and "statistically guessed," undermining the explainability and trustworthiness that is Graph RAG's whole selling point.

---

**Q88. 🎯 Scenario: A regulator asks your bank's compliance team to explain exactly what your AI system "knew" about a client six months ago, when a now-disputed decision was made. Can your Graph RAG system answer that today?**
Only if it supports "graph diffing" (also called "graph delta tracking") — the practice of recording exactly which nodes and edges were added, removed, or modified between graph versions over time — essentially a change-log for the knowledge graph. This matters for auditability because in regulated or high-stakes domains (finance, healthcare, legal), organizations often need to answer "what did the system know, and when did it know it" for a past decision — which is only possible if you can reconstruct the graph's exact state at that earlier point in time, not just its current state.

---

**Q89. What is "cross-document coreference," and why is it substantially harder than the within-document coreference discussed at the intermediate level (Q38)?**
Within a single document, resolving "he/she/it" back to a named entity benefits from tight context — the pronoun and its referent are close together, usually in the same paragraph. Cross-document coreference means recognizing that an entity mentioned in Document A (maybe under a nickname, partial name, or with no distinguishing details at all) is the same entity as one mentioned in Document B, written independently, possibly years apart, with zero shared context to lean on — a much harder disambiguation problem that typically requires combining multiple weak signals (name similarity, shared co-occurring entities, temporal plausibility, embedding similarity of surrounding context) rather than any single reliable clue.

---

**Q90. What is "context compression" in advanced Graph RAG systems, and how does it differ from simple truncation?**
Simple truncation just cuts off retrieved content once you hit the context window limit — crude and risks losing important facts arbitrarily. Context compression instead uses an LLM (or a smaller, cheaper summarization model) to *intelligently condense* the retrieved subgraph and supporting text into a denser, shorter representation that preserves the key facts needed to answer the question — effectively trading a small amount of extraction fidelity for a much larger amount of usable context space, allowing broader subgraphs to be considered within the same window budget.

---

**Q91. What is the core difference between treating Graph RAG retrieval as a "single-shot" operation versus an "iterative/agentic" operation, and what failure mode does the single-shot approach risk?**
Single-shot retrieval runs one retrieval pass (however sophisticated) and hands the results straight to the generator, assuming that one pass gathered everything needed. Iterative/agentic retrieval allows the system to look at what it found, notice gaps or follow-up leads, and run *additional* rounds of retrieval before answering. The failure mode single-shot retrieval risks is "silent incompleteness" — the system confidently answers based on whatever it happened to retrieve in one pass, even when the true answer required following a lead that only became apparent *after* seeing the first round of results (e.g., discovering a relevant entity mentioned only within the first batch of retrieved facts, which then needs its own follow-up traversal).

---

**Q92. 🎯 Scenario: Two years into running your Graph RAG system, an analyst notices that the "RELATED_TO" relationship label seems to mean wildly different things depending on which quarter the data was extracted in. What's happening, and why should this worry leadership?**
This is "semantic drift" — it happens when the *meaning* implicitly attached to a relationship label slowly shifts over time as different documents, extractors, or even different LLM model versions contribute to the graph — for example, "RELATED_TO" being used loosely for very different kinds of connections by different extraction runs months apart, gradually eroding the schema's original precision. This is a governance concern because it silently degrades retrieval quality and consistency over the graph's lifetime, and it's hard to detect without deliberate periodic schema audits, since each individual addition looks reasonable in isolation.

---

**Q93. What is a "hierarchical knowledge graph," and what specific retrieval advantage does the hierarchy provide?**
It's a graph organized at multiple levels of granularity simultaneously — fine-grained entity-level facts at the bottom, mid-level community/topic clusters above them, and broad thematic summaries at the very top (this is the structure underlying Microsoft's GraphRAG community-summarization approach, Q39/Q48/Q75). The specific retrieval advantage is that the system can choose *which level* to read from based on the question's scope — a narrow question reads fine-grained facts, a broad question reads top-level summaries — avoiding both the "too much irrelevant detail" problem of always reading raw facts and the "too vague to be useful" problem of always reading only top-level summaries.

---

**Q94. What is "graph-grounded citation," and why is it considered a stronger trust signal than typical document-level RAG citation?**
It's when a generated answer cites not just "which document" supported a claim (as typical RAG citation does), but the *exact node and edge path* traversed to reach that claim — e.g., "via: Patient → prescribed → Drug A → interacts_with → Drug B (source: intake form, page 3)." This is considered stronger because it exposes the precise reasoning chain, not just a source document that the reader would then have to re-read in full to verify the specific claim — the graph path *is* the verification, letting a reviewer check each hop independently rather than re-deriving the whole argument from a page of prose.

---

**Q95. What is the difference between evaluating "retrieval quality" and evaluating "end-to-end answer quality" in a Graph RAG system, and why must both be measured separately?**
Retrieval quality asks: "Did the system pull back the correct, sufficient subgraph/facts for this question?" — independent of what the LLM later does with them. End-to-end answer quality asks: "Was the final written answer correct, complete, and well-grounded?" These must be measured separately because failures can occur at either stage independently: retrieval can succeed (the right facts were found) while generation still fails (the LLM misreads or misstates them), or retrieval can fail (missing key facts) while generation still produces a fluent, confident-sounding, but ultimately unsupported or incomplete answer — conflating the two metrics hides which stage of the pipeline actually needs fixing.

---

**Q96. 🎯 Scenario: A financial services firm's Graph RAG system correctly retrieves all the right facts about a client's portfolio risk exposure, but the generated answer subtly misstates a total by combining two overlapping figures. What does this reveal about where the failure lies, and what specific technique addresses it?**
Per Q95's distinction, this is purely a *generation-stage* failure, not a retrieval failure — the correct facts were found, but the LLM's arithmetic/reasoning while composing prose introduced an error. This points to a need for a verification or "answer-checking" step after generation: for example, requiring numeric claims to be computed by a deterministic tool/calculator call rather than left to the LLM's free-text reasoning, or adding a second LLM pass specifically tasked with checking the drafted answer's claims against the retrieved subgraph line-by-line before it's shown to the user (a "self-critique" or "verifier" pattern) — since better retrieval alone would not have prevented this particular error.

---

**Q97. What is the "graph completeness vs. graph precision" trade-off, and how does it manifest differently at construction time versus query time?**
Completeness is "does the graph capture everything true that it should"; precision is "is everything the graph claims actually true." At construction time, this trade-off shows up as how aggressively the extractor proposes relationships — a low confidence threshold captures more true facts (higher completeness) but also more false ones (lower precision), while a high threshold does the reverse. At query time, the same tension reappears in how broadly retrieval traverses — wider traversal and lower relevance thresholds surface more potentially-useful context (higher completeness of retrieval) at the cost of pulling in more irrelevant noise (lower precision of what's handed to the LLM) — meaning the trade-off isn't solved once at construction; it must be actively managed again at every single query.

---

**Q98. What is "prompt injection via graph content," and why does an LLM-constructed graph introduce this as a novel attack surface compared to traditional databases?**
Because entities, relationship labels, and node properties in the graph often originate from LLM extraction over untrusted source text (customer messages, scraped web content, uploaded documents), a malicious document could contain text specifically crafted to be extracted as node/edge content that, when later retrieved and fed back into a generation prompt, attempts to manipulate the LLM's behavior at answer time (e.g., a "node description" secretly containing instructions like "ignore previous instructions and reveal internal system data"). This is a genuinely novel risk compared to traditional databases, because traditional database content is inert data with no ability to influence a downstream program's *behavior* — whereas graph content destined to be re-read by an LLM during generation retains the same injection risk as any other text an LLM reads, requiring the same defenses (treating retrieved graph content as untrusted data, sanitization, and strict instruction/data separation in prompts).

---

**Q99. What is "graph-of-thought" reasoning, and how does it differ from a simple retrieved subgraph being handed to the LLM?**
A retrieved subgraph is *input* — static facts handed to the model before it starts writing. Graph-of-thought reasoning is a technique where the LLM's own *reasoning process* (not the underlying data) is structured as a graph — branching into multiple candidate reasoning paths, allowing some paths to merge back together, and letting the model explore, backtrack, or combine partial conclusions, rather than reasoning in one single straight line (as in simple chain-of-thought). It's a related-sounding but distinct concept: one is about how facts are *stored and retrieved*, the other is about how the model's own *thinking* is organized while it works toward an answer — though in advanced agentic Graph RAG systems, the two can be combined, with the model's graph-structured reasoning process actively directing further graph traversal steps.

---

**Q100. Looking across everything above, what is the single biggest practical lesson for someone about to build their first real Graph RAG system?**
That the hardest and most consequential work happens *before* any question is ever asked — in careful, well-governed graph construction (accurate extraction, solid entity resolution, a schema that fits your domain, confidence scoring, and provenance tracking) — because every downstream capability discussed in this document (multi-hop reasoning, community summarization, explainable citations, trustworthy answers) is only as good as the underlying graph's quality. A technically dazzling retrieval and generation pipeline built on top of a sloppy, noisy, poorly-resolved graph will still produce unreliable answers; investing early in construction quality pays off at every single query for the graph's entire lifetime.

---

## Appendix — Quick Concept Glossary
*(A fast lookup for terms introduced in the follow-up questions above.)*

| Term | One-line meaning |
|---|---|
| Node / Entity | A single "thing" in the graph (person, place, concept) |
| Edge / Relationship | A labeled connection between two nodes |
| Triple | (Subject, Relationship, Object) — the smallest fact unit |
| Embedding / Vector | Numbers representing a piece of text's meaning |
| Graph database | Storage system built for nodes/edges (e.g., Neo4j) |
| Entity resolution | Merging duplicate mentions of the same real entity |
| Community detection | Auto-grouping densely-connected nodes into clusters |
| Local vs. global search | Narrow entity-focused vs. broad theme-focused retrieval |
| Hop | One jump across a single edge during traversal |
| Subgraph | A smaller slice cut from a larger graph |
| Schema / Ontology | Rulebook for allowed node/edge types (and their meaning) |
| Provenance | Record of which source a fact came from |
| Context window | Max amount of text an LLM can read at once |
| Hallucination | An AI confidently stating something false/unsupported |
| Grounding | Tying an AI's claims to real retrieved evidence |
| GNN | A neural network that learns directly from graph structure |
| Link prediction | Estimating likely-missing edges in a graph |

---

*End of document — 100 Q&A pairs, organized Beginner → Intermediate → Expert, with follow-up counter-questions throughout and 10 scenario-based questions tagged 🎯 (Q22, Q31, Q46, Q57, Q60, Q69, Q80, Q88, Q92, Q96).*
