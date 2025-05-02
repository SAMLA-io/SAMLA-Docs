Performs a powerful hybrid search, seamlessly blending both semantic and lexical search techniques across all indexes within your organization’s Pinecone account. This dual approach harnesses the intelligence of semantic search—which interprets the meaning, context, and intent behind the query—alongside the precision of lexical search, which identifies exact keyword and phrase matches. By uniting these methods, the search delivers results that are not only comprehensive but also highly relevant, ensuring that no important document is overlooked.

- `POST /search`
    - Searches all your documents for both the meaning of your question and the exact words you use. This helps find the best matches.
    - Parameters:
        - `organization_id`: The unique identifier for your organization, ensuring the search is securely scoped to your data and maintaining strict separation between different organizations’ information.
        - `prompt`: The search query text entered by the user. This can range from a simple keyword to a complex question or phrase. For example, entering "Q3 marketing strategy outcomes" will retrieve documents related to your organization’s marketing strategies and results for the third quarter, whether the match is based on meaning or exact wording.
    - Returns an elegant array of search hits, each containing:
        - `id`: The unique identifier for the matched document, allowing for easy retrieval or reference in future actions.
        - `score`: A similarity score that reflects how closely each document aligns with your search query. Higher scores indicate a stronger match, helping you quickly pinpoint the most relevant information.
        - `fields`: A rich collection of the document’s content and metadata, such as title, author, creation date, and any custom fields defined by your organization. This contextual information empowers you to assess the relevance and importance of each result at a glance.

By artfully combining semantic understanding with lexical precision across multiple indexes, this endpoint elevates your search experience—making it intuitive, thorough, and remarkably effective at uncovering the information that matters most within your organization’s knowledge base.