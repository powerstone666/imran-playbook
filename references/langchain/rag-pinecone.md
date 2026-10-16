# LangChain RAG And Pinecone

Use this for RAG systems, embeddings, Pinecone, and vector search.

## RAG flow

```text
[PDF]
  |
[Load with PDFLoader or TextLoader]
  |
[Split text with RecursiveCharacterTextSplitter]
  |
[Embed docs with embedding model]
  |
[Upload to DB]
  |
[Take user query]
  |
[Embed query]
  |
[Search DB]
  |
[Return results to model]
```

## Chunking

- LangChain treats many file types as documents.
- Split documents to avoid large chunks in one query.
- Default useful values: `chunkSize: 1000`, `chunkOverlap: 200`.
- Embed documents with document embedding APIs.
- Embed queries separately with query embedding APIs.

## Pinecone inbuilt embedding

In this approach, pass raw chunks and let Pinecone embed them.

```ts
await pineconeIndex.upsertRecords({
  records: chunks.map((chunk, index) => ({
    id: `policy-chunk-${index}`,
    text: chunk.pageContent,
    source: chunk.metadata.source,
  })),
});
```

Search:

```ts
const searchResults = await pineconeIndex.searchRecords({
  query: {
    topK: 5,
    inputs: { text: input },
  },
  fields: ["text", "source"],
});
```

## Custom embedding

Use a custom embedding model when you need control. The embedding dimension must match the Pinecone index dimension.

```ts
const vectorStore = await PineconeStore.fromDocuments(chunks, embeddings, {
  pineconeIndex,
});
```

Search:

```ts
const results = await vectorStore.similaritySearch(input, 5);
```

Retrieve from existing index:

```ts
const vectorStore = await PineconeStore.fromExistingIndex(embeddings, {
  pineconeIndex,
  namespace: "resume",
});
```

## Search types

- `similaritySearch`: basic search; may return duplicates because overlapping chunks share keywords.
- `maxMarginalRelevanceSearch`: better production default when diversity matters.

```ts
const searchResults = await vectorStore.maxMarginalRelevanceSearch(query, {
  k: 5,
  fetchK: 20,
  lambda: 0.5,
});
```
